# Design of Unity
This topic describes the design goals, the architecture, and the design highlights of Unity. You do not have to understand the design to use Unity; however, this topic will help you to understand how it works and how it interacts with the underlying object builder subsystem.

## Design Goals
Unity was designed to achieve the following goals:
* Promote the principles of modular design through aggressive decoupling.
* Maximize testability when designing applications.
* Provide a fast and lightweight dependency injection platform for creating new as well as managing existing objects.
* Expose a compact and intuitive API for developers to work with.
* Support a wide range of languages, and platforms.
* Allow attribute-driven injection for constructors, properties, fields, and methods.
* Provide extensibility through container extensions.
* Provide stability required in enterprise-level line of business (LOB) applications.

## Packaging
To allow maximum decoupling between declarative part and implementation Unity split into two assemblies: [Unity.Abstractions](https://www.nuget.org/packages/Unity.Abstractions/) and [Unity.Container](https://www.nuget.org/packages/Unity.Container/)

#### [Unity.Abstractions](https://www.nuget.org/packages/Unity.Abstractions/)
This assembly contains all public member declarations required to use Unity container in applications. It defines [IUnityContainer](xref:Unity.IUnityContainer) interface as well as types and interfaces used to register, configure and resolve types and instances. Abstraction assembly contains following namespaces:
* [Unity](xref:Unity)
* [Unity.Injection](xref:Unity.Injection)
* [Unity.Lifetime](xref:Unity.Lifetime)
* [Unity.Policy](xref:Unity.Policy)
* [Unity.Resolution](xref:Unity.Resolution)

#### [Unity.Container](https://www.nuget.org/packages/Unity.Container/)
This assembly implements Unity container's engine and exposes public members required to extend the container. 

#### [Unity](https://www.nuget.org/packages/Unity/)
This is a convenience package containing both [Unity.Abstractions](https://www.nuget.org/packages/Unity/) as well as [Unity.Container](https://www.nuget.org/packages/Unity/) assemblies. This package is distributed for these who do now wish to separate declarations and implementation.

### More Information
For more information about using packages inside applications see [Application Design](application_design.md) concepts with Unity.
