---
tags:
  - architecture
  - design-patterns
  - ui-development
category: Architecture Conventions and Templates
related: MVC, WinForms and MAUI, Interfaces, Classes
---

# MVVM (Model - View - ViewModel)

MVVM is a UI architecture pattern where the **View** binds to a **ViewModel**, which exposes the data and commands the screen needs, while the **Model** holds the data and business rules. The key feature is **data binding**: the View updates automatically when ViewModel properties change, and user input flows back without manual event wiring. It is the standard pattern for .NET MAUI and WPF.

## The Three Roles

| Role | Responsibility | Knows about |
|------|----------------|-------------|
| **Model** | Data, business rules, services | Nothing about UI |
| **View** | Layout and visuals (XAML) | The ViewModel, only through bindings |
| **ViewModel** | UI state, formatted data, commands | The Model, but **not** the View |

The ViewModel never references UI controls. That makes it testable with plain unit tests.

## How Data Flows

```text
View (XAML) ◄── binding ──► ViewModel ──► Model / Services
   │                            ▲
   └── Command (button tap) ────┘
```

- **Properties** flow data from the ViewModel to the View.
- **Two-way bindings** push user input (text boxes, toggles) back into the ViewModel.
- **Commands** replace click event handlers.
- `INotifyPropertyChanged` tells the View when a property changed.

## Example (.NET MAUI)

```csharp
// ViewModel
public class CounterViewModel : INotifyPropertyChanged
{
    private int _count;

    public int Count
    {
        get => _count;
        set
        {
            _count = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(nameof(Count)));
        }
    }

    public ICommand IncrementCommand { get; }

    public CounterViewModel()
    {
        IncrementCommand = new Command(() => Count++);
    }

    public event PropertyChangedEventHandler? PropertyChanged;
}
```

```xml
<!-- View -->
<VerticalStackLayout>
    <Label Text="{Binding Count}" />
    <Button Text="Add" Command="{Binding IncrementCommand}" />
</VerticalStackLayout>
```

```csharp
// Code-behind only connects the View to its ViewModel
public MainPage()
{
    InitializeComponent();
    BindingContext = new CounterViewModel();
}
```

Libraries such as **CommunityToolkit.Mvvm** generate the property-changed and command boilerplate with attributes (`[ObservableProperty]`, `[RelayCommand]`).

## MVVM vs MVC

| Aspect | [[MVC]] | MVVM |
|--------|---------|------|
| Typical platform | Web (request/response) | Desktop/mobile (stateful UI) |
| Coordinator | Controller handles each request | ViewModel holds ongoing UI state |
| View updates | Re-render per request | Automatic through data binding |
| View ↔ coordinator link | Controller picks the View | View binds to the ViewModel |

## Advantages and Trade-offs

**Advantages**
- ViewModels are testable without a UI
- Designers and developers can work on View and logic separately
- Less event-handler code in code-behind

**Trade-offs**
- Boilerplate without a toolkit
- Binding errors can fail silently at runtime
- Overkill for very small screens

## Use when

- Building .NET MAUI, WPF, or other XAML-based apps
- Screens have state that changes often and must stay in sync with the UI
- You want UI logic covered by unit tests

## Related Concepts

- [[MVC]] - Request-based counterpart used on the web
- [[WinForms and MAUI]] - MAUI apps are commonly built with MVVM
- [[Interfaces]] - `INotifyPropertyChanged` and `ICommand` contracts
- [[Clean Code]] - ViewModels belong to the presentation layer
- [[SOLID Principles]] - Keeping UI and logic responsibilities separate
