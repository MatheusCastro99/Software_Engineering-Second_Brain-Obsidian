---
tags:
  - ui-development
  - csharp
  - frameworks
category: UI Development
related: Classes, OOP Fundamentals, Methods
---

# WinForms and MAUI

Both are frameworks for building desktop and mobile UIs in C#, but they have different philosophies and use cases.

## WinForms (Windows Forms)

### Characteristics
- **Platform** - Windows desktop only
- **Paradigm** - Imperative/event-driven
- **Maturity** - Mature, stable, established
- **Learning Curve** - Easier for beginners
- **Performance** - Lightweight and fast

### Architecture: Event-Driven

```csharp
public partial class MainForm : Form
{
    private Button submitButton;
    private TextBox inputBox;
    
    public MainForm()
    {
        InitializeComponent();
        
        // Create UI elements imperative way
        submitButton = new Button
        {
            Text = "Submit",
            Left = 10,
            Top = 10,
            Width = 100
        };
        
        // Wire up event handlers
        submitButton.Click += SubmitButton_Click;
        
        this.Controls.Add(submitButton);
    }
    
    private void SubmitButton_Click(object sender, EventArgs e)
    {
        string input = inputBox.Text;
        MessageBox.Show($"You entered: {input}");
    }
}
```

### Key Components
- **Form** - Window container
- **Controls** - UI elements (Button, TextBox, Label, etc.)
- **Events** - Click, TextChanged, Load, FormClosing, etc.
- **Designer** - Drag-and-drop UI builder in Visual Studio

### Workflow

1. **Design UI** - Drag controls onto form designer
2. **Handle Events** - Double-click control to create event handler
3. **Write Logic** - Code runs when event fires
4. **Test** - Run application

### Best For
- Legacy Windows applications
- Enterprise desktop software
- Simple desktop tools
- When Windows-only is acceptable

### Limitations
- Windows only (not cross-platform)
- No native mobile support
- Older look and feel
- Not suited for modern web integration

## MAUI (Multi-platform App UI)

### Characteristics
- **Platform** - Windows, macOS, iOS, Android, Linux (write once, run many)
- **Paradigm** - Declarative/XAML-based
- **Maturity** - Modern, evolving
- **Learning Curve** - Steeper (requires understanding XAML)
- **Performance** - Good, native rendering

### Architecture: Declarative with XAML

```xml
<!-- MainPage.xaml -->
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    Title="My App">
    
    <VerticalStackLayout Padding="30" Spacing="10">
        <Label Text="Enter your name:"
            FontSize="18"
            FontAttributes="Bold" />
        
        <Entry x:Name="NameEntry"
            Placeholder="Your name" />
        
        <Button Text="Submit"
            Clicked="OnSubmitClicked" />
    </VerticalStackLayout>
    
</ContentPage>
```

```csharp
// MainPage.xaml.cs
public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
    }
    
    private void OnSubmitClicked(object sender, EventArgs e)
    {
        string name = NameEntry.Text;
        DisplayAlert("Welcome", $"Hello, {name}!", "OK");
    }
}
```

### Key Components
- **XAML** - XML-based markup for UI (declarative)
- **Code-Behind** - C# logic file
- **Layouts** - VerticalStackLayout, HorizontalStackLayout, Grid, etc.
- **Controls** - Button, Label, Entry (cross-platform)
- **Bindings** - Data binding for reactive UIs

### Workflow

1. **Define UI** - Write XAML markup
2. **Create Models** - Data structures
3. **Implement Logic** - C# code-behind
4. **Bind Data** - Connect UI to data
5. **Test** - Run on multiple platforms

### Cross-Platform Targeting

```csharp
// Same code, different platforms
var text = MainThread.IsMainThread ? "UI thread" : "Background thread";

#if WINDOWS
    // Windows-specific code
#elif ANDROID
    // Android-specific code
#elif IOS
    // iOS-specific code
#endif
```

### Best For
- Multi-platform applications
- Mobile-first development
- Modern UI with bindings
- Cloud-connected apps
- Cross-device applications (phone, tablet, desktop)

## Comparison

| Aspect | WinForms | MAUI |
|--------|----------|------|
| **Platforms** | Windows only | Windows, Mac, iOS, Android, Linux |
| **Paradigm** | Imperative | Declarative (XAML) |
| **Learning** | Easier | More concepts |
| **Performance** | Excellent | Good |
| **Maintenance** | Stable | Evolving |
| **Mobile** | Not supported | Native support |
| **Modern Look** | Basic | Modern designs |
| **Maturity** | Very mature | Growing |
| **Enterprise** | Established | Emerging |

## When to Choose

### Choose WinForms When:
- Desktop-only is acceptable
- Building traditional Windows software
- Rapid simple desktop tools
- Team already knows WinForms

### Choose MAUI When:
- Need cross-platform support
- Targeting mobile platforms
- Building modern applications
- Single codebase for multiple platforms
- Team willing to learn XAML

## Data Binding in MAUI

```csharp
// ViewModel (MVVM pattern)
public class UserViewModel : INotifyPropertyChanged
{
    private string name;
    public string Name
    {
        get => name;
        set
        {
            if (name != value)
            {
                name = value;
                OnPropertyChanged();
            }
        }
    }
    
    public event PropertyChangedEventHandler PropertyChanged;
    
    protected void OnPropertyChanged([CallerMemberName] string name = null)
        => PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(name));
}
```

```xml
<!-- XAML binding -->
<Entry Text="{Binding Name}" />
<Label Text="{Binding Name}" />
```

## Related Concepts

- [[Classes]] - UI components are classes
- [[OOP Fundamentals]] - Inheritance in UI frameworks
- [[Methods]] - Event handlers and bindings