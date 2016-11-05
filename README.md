AutoHotkey.Interop
==================

This project is a basic wrapper around [HotKeyIt's AHKDLL](https://github.com/HotKeyIt/ahkdll) (aka **AutoHotkey_H**) for .Net Projects.

This was made to be intended to use as is, without needing to register any of the com components or any other special deployment tasks. The required (AutoHotkey_H) AutoHotkey.dll file can be deployed via XCOPY. The application can automatically deploy the required AutoHotkey.dll file if it is missing, as it stores a copy as an embeded resource.

All the thanks goes to HotKeyIt's work 

Usage & Examples
====================
To use, just include my DLL and it will deploy any files that are missing if needed.


```cs
//execute any raw ahk code
AutoHotkeyEngine.ExecRaw("MsgBox, Hello World!");

//create new hotkeys
AutoHotkeyEngine.ExecRaw("^a::Send, Hello World");

//programmatically set variables
AutoHotkeyEngine.SetVar("x", "1");
AutoHotkeyEngine.SetVar("y", "4");

//execute statements
AutoHotkeyEngine.ExecRaw("z:=x+y");

//return variables back from ahk
string zValue = AutoHotkeyEngine.GetVar("z");
Console.WriteLine("Value of z is {0}", zValue); // "Value of z is 5"

//Load a library or exec scripts in a file
AutoHotkeyEngine.LoadFile("functions.ahk");

//execute a specific function (found in functions.ahk), with 2 parameters
AutoHotkeyEngine.ExecFunction("MyFunction", "Hello", "World");

//execute a label 
AutoHotkeyEngine.ExecLabel("DOSTUFF");

//create a new function
string sayHelloFunction = "SayHello(name) \r\n { \r\n MsgBox, Hello %name% \r\n return \r\n }";
AutoHotkeyEngine.ExecRaw(sayHelloFunction);

//execute's newly made function\
AutoHotkeyEngine.ExecRaw(@"SayHello(""Mario"") ");


//execute a function (in functions.ahk) that adds 5 and return results
var add5Results = AutoHotkeyEngine.Eval("Add5( 5 )");
Console.WriteLine("Eval: Result of 5 with Add5 func is {0}", add5Results);

//you can also return results with the ExecFunction 
add5Results = AutoHotkeyEngine.ExecFunction("Add5", "5");
Console.WriteLine("ExecFunction: Result of 5 with Add5 func is {0}", add5Results);

```




Links
=============

[HotKeyIt's AutoHotkey_H Github Repository](https://github.com/HotKeyIt/ahkdll)  
[AutoHotKey_H Dll Documentation](http://www.autohotkey.net/~HotKeyIt/AutoHotkey/files/AutoHotkey-dll-txt.html)  




