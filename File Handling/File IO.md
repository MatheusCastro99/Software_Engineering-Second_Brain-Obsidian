---
tags:
  - file-handling
  - csharp
  - io
category: File Handling
related: Error Handling, Variables and Data Types
---

# File IO

File IO (Input/Output) enables reading from and writing to files on disk. C# provides multiple approaches from simple to advanced.

## Key Principles

✓ **Always close files** - Free resources (use `using`)
✓ **Use relative paths** - Avoid hard-coded full paths
✗ **Never hard-code paths** - Make code portable
✗ **Ignore errors silently** - Log and handle exceptions

## Simple File Operations

### Reading Files

```csharp
using System.IO;

// Read entire file at once
string content = File.ReadAllText("data.txt");

// Read all lines
string[] lines = File.ReadAllLines("data.txt");
foreach (string line in lines)
{
    Console.WriteLine(line);
}

// Read all bytes
byte[] bytes = File.ReadAllBytes("image.png");
```

### Writing Files

```csharp
// Write text (overwrites existing)
File.WriteAllText("output.txt", "Hello World");

// Write lines
string[] lines = { "Line 1", "Line 2", "Line 3" };
File.WriteAllLines("output.txt", lines);

// Append text (adds to end)
File.AppendAllText("log.txt", "New log entry\n");
```

## StreamReader and StreamWriter

**For larger files or line-by-line processing**

### StreamReader (Reading)

```csharp
try
{
    // Open file for reading
    using (StreamReader reader = new("data.txt"))
    {
        string line;
        while ((line = reader.ReadLine()) != null)
        {
            Console.WriteLine(line);
        }
    } // File automatically closed
}
catch (FileNotFoundException ex)
{
    Console.WriteLine($"File not found: {ex.Message}");
}
```

### StreamWriter (Writing)

```csharp
try
{
    using (StreamWriter writer = new("output.txt"))
    {
        writer.WriteLine("Line 1");
        writer.WriteLine("Line 2");
        // Automatically flushed and closed
    }
}
catch (IOException ex)
{
    Console.WriteLine($"Error writing file: {ex.Message}");
}
```

## Working with Paths

**Always use Path class for portability**

```csharp
using System.IO;

// Bad: Hard-coded path
string path = "C:\\Users\\Documents\\data.txt"; // Windows only
string path = "/home/user/documents/data.txt";  // Linux only

// Good: Use Path class
string folderPath = Path.Combine(Environment.GetFolderPath(
    Environment.SpecialFolder.MyDocuments), "data.txt");
// Works on any OS

// Get parts of path
string fileName = Path.GetFileName("C:\\Users\\docs\\file.txt"); // "file.txt"
string directory = Path.GetDirectoryName(folderPath); // Parent folder
string extension = Path.GetExtension("file.txt"); // ".txt"
string nameOnly = Path.GetFileNameWithoutExtension("file.txt"); // "file"

// Combine paths
string fullPath = Path.Combine(folderPath, fileName);
```

## File Existence Check

```csharp
// Check file exists
if (File.Exists("data.txt"))
{
    string content = File.ReadAllText("data.txt");
}
else
{
    Console.WriteLine("File not found");
}

// Check directory exists
if (Directory.Exists("backups"))
{
    // ...
}
```

## Directory Operations

```csharp
using System.IO;

// Create directory
Directory.CreateDirectory("backups");

// Get files in directory
string[] files = Directory.GetFiles("data");
foreach (string file in files)
{
    Console.WriteLine(file);
}

// Get all files recursively
string[] allFiles = Directory.GetFiles("data", "*", 
    SearchOption.AllDirectories);

// Delete directory (must be empty)
Directory.Delete("temp");

// Delete with contents
Directory.Delete("temp", recursive: true);
```

## Reading/Writing Specific Formats

### CSV Files

```csharp
// Simple CSV reading
var lines = File.ReadAllLines("data.csv");
foreach (string line in lines)
{
    string[] values = line.Split(',');
    string name = values[0];
    string email = values[1];
}

// Writing CSV
using (StreamWriter writer = new("output.csv"))
{
    writer.WriteLine("Name,Email");
    writer.WriteLine("Alice,alice@example.com");
    writer.WriteLine("Bob,bob@example.com");
}
```

### JSON Files

```csharp
using System.Text.Json;

// Read JSON
string json = File.ReadAllText("config.json");
var config = JsonSerializer.Deserialize<Dictionary<string, string>>(json);

// Write JSON
var data = new { Name = "Alice", Age = 30 };
string json = JsonSerializer.Serialize(data);
File.WriteAllText("output.json", json);
```

## Best Practices

✓ **Always use `using`** - Ensures file closure
✓ **Use Path.Combine** - Portable path construction
✓ **Check File.Exists** - Avoid FileNotFoundException
✓ **Handle IOException** - Disk full, permissions, etc.
✓ **Use relative paths** - Application directory relative
✗ **Hard-code paths** - Not portable
✗ **Ignore exceptions** - Always log/handle
✗ **Leave files open** - Always close/dispose

```csharp
// Good pattern
try
{
    string dataPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "data.txt");
    if (!File.Exists(dataPath))
    {
        Console.WriteLine("Data file not found");
        return;
    }
    
    using (StreamReader reader = new(dataPath))
    {
        // Process file
    }
}
catch (IOException ex)
{
    Console.WriteLine($"File error: {ex.Message}");
}
```

## Related Concepts

- [[Error Handling]] - Handle file operation exceptions
- [[Variables and Data Types]] - Reading/writing data types