# Adding Unity to Your Application
Unity is designed to support a range of common scenarios for resolving instances of objects that, themselves, depend on other objects or services. However, you must first prepare your application to use Unity. The following procedure describes how to include the necessary assemblies and elements in your code.
## To prepare your application
Add a reference to the Unity package. In Visual Studio, right-click your project node in Solution Explorer, and then click Add Reference. Click the Browse tab and find the location of the Microsoft.Practices.Unity.dll assembly. Select the assembly, and then click OK to add the reference.

(Optional) If you intend to use the configuration types when you create extensions for Unity, use the same procedure to set a reference to the Unity configuration assembly, named Microsoft.Practices.Unity.Configuration.dll.

(Optional) If you intend to use the interception and policy injection features of Unity, use the same procedure to set a reference to the Unity interception assembly, named Microsoft.Practices.Unity.Interception.dll.

(Optional) If you intend to use the configuration types for the interception and policy injection features of Unity, use the same procedure to set a reference to the Unity interception configuration assembly, named Microsoft.Practices.Unity.Interception.Configuration.dll.

(Optional) To use elements from Unity without fully qualifying the element reference, add the following using statements (C#) or Imports statements (Visual Basic) to the top of your source code file as required.
```C#
using Unity;
```
(Optional) If you are using the IServiceLocator interface, add a reference to the service location binary Microsoft.Practices.ServiceLocation.dll. Visual Studio may automatically copy this file to your bin directory when it compiles, but you do not need to include it unless you are explicitly using the UnityServiceLocatorAdapter class.

Add your application code. For more information about how you can use Unity in your own applications, see What Does Unity Do?