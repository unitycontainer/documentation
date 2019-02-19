# Adding Unity to Your Application
Unity is designed to support a range of common scenarios for resolving instances of objects that, themselves, depend on other objects or services. However, you must first prepare your application to use Unity. The following procedure describes how to include the necessary assemblies and elements in your code.
## To prepare your application
Add a reference to the Unity package. You have a choice to reference Unity.Container and Unity.Abstractions individually or you could just reference Unity package and it will include both these assemblies as a single package.

(Optional) If you intend to use the configuration types when you create extensions for Unity, use the same procedure to set a reference to the Unity configuration package, named Unity.Configuration.

(Optional) If you intend to use the interception and policy injection features of Unity, use the same procedure to set a reference to the Unity interception package, named Unity.Interception.

## References
Using individual packages allows you to reference just Unity.Abstractions in your libraries and link Unity.Container only in your bootloeader project. This should allow you to update Unity.Container engine without recompiling any of the DLLs that use the container.
