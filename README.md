# Csharp_ParallelProgramming_Sample1_CreatingAndStartingTasks

0.Include the Threading.Task library:

```csharp
using System.Threading.Tasks;
```

1.Two ways of using tasks:
```csharp
//Creates and Starts a task. 
//We call the method "Write", and we send to this method the paramter "bar".
Task.Factory.StartNew(Write, "bar"); 
```
```csharp
//Creates a task; use Start() to fire it.
//We call the method "Write", and we send to this method the paramter "bar".
Task t = new Task(Write, "foo");
t.Start();
```
or
```csharp
Task t = new Task(() => Write('?'));
```
or
```csharp
Task.Factory.StartNew(() =>
{
   Write('-');
});
```

2.Tasks take an optional 'object' argument.
```csharp
Task.Factory.StartNew(x => { foo(x) }, arg);
```

3.To return values, use ```Task<T>``` instead of Task. 
```csharp
string text1 = "testing", text2 = "this";
var task1 = new Task<int>(TextLength, text1);
task1.Start();
```

4.To get the return value use t.Result (this waits until task is complete).

```csharp
string text1 = "testing", text2 = "this";
var task1 = new Task<int>(TextLength, text1);
task1.Start();
var task2 = Task.Factory.StartNew(TextLength, text2);
// getting the result is a blocking operation!
Console.WriteLine($"Length of '{text1}' is {task1.Result}.");
Console.WriteLine($"Length of '{text2}' is {task2.Result}.");
```

5.Use Task.CurrentId to identify individual tasks.
```csharp
public static int TextLength(object o)
{
   Console.WriteLine($"\nTask with id {Task.CurrentId} processing object '{o}'...");
   return o.ToString().Length;
}
```
