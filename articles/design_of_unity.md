# Design of Unity
This topic describes the design goals, the architecture, and the design highlights of Unity. You do not have to understand the design to use Unity; however, this topic will help you to understand how it works and how it interacts with the underlying object builder subsystem.

## Design Goals
Unity was designed to achieve the following goals:
* Promote the principles of modular design through aggressive decoupling.
* Maximize testability when designing applications.
* Provide a fast and lightweight dependency injection container mechanism for creating new object instances and managing existing object instances.
* Expose a compact and intuitive API for developers to work with.
* Support a wide range of languages, and platforms.
* Allow attribute-driven injection for constructors, public properties, fields, and methods of target objects.
* Provide extensibility through container extensions.
* Provide the performance required in enterprise-level line of business (LOB) applications.

## Organization
Unity organized into set of two assemblies:
#### Unity.Abstractions
This assembly contains all public members required to use Unity container in applications. It defines [IUnityContainer](xref:Unity.IUnityContainer) interface as well as types and interfaces required to register, configure and resolve types and instances. Abstraction assembly contains following namespaces:
* [Unity](xref:Unity)
* [Unity.Injection](xref:Unity.Injection)
* [Unity.Lifetime](xref:Unity.Lifetime)
* [Unity.Policy](xref:Unity.Policy)
* [Unity.Resolution](xref:Unity.Resolution)
#### Unity.Container
This assembly implements Unity container's engine and exposes public members required to extend the container. 


This division is created to allow independence between declaration and implementation of container. 

