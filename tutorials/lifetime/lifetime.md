---
uid: Tutorial.Lifetime.Overview
title: Lifetime Management
---

# Lifetime

The Unity container manages the lifetime of objects based on a [Lifetime Manager](xref:Unity.Lifetime) you specify when you register the type. If you do not specify anything for your type registration Unity uses transient lifetime manager.

When you register a type in configuration, or by using the ``RegisterType`` method and do not explicitly specify lifetime manager, the default behavior is for the container to use a transient lifetime manager. It creates a new instance of the registered, mapped, or requested type each time you call the Resolve method or when the dependency mechanism injects instances into other classes. The container does not store a reference to the object.

Unity uses specific types that inherit from the ``LifetimeManager`` base class (collectively referred to as lifetime managers) to control how it stores references to object instances and how the container disposes of these instances.

When you register an existing object using the ``RegisterInstance`` method, the default behavior is for the container to take over management of the lifetime of the object you pass to this method using the ``ContainerControlledLifetimeManager``. This means that container maintains strong reference to the object and at the end of the container lifetime, the existing object is disposed.

## How registering lifetime works

Unity uses concepts of **Registered** type and **MappedTo** type. Depending if registration is a mapping or just single type registration Unity behaves differently

### Single type registration

When type is registered like this:

```C#
RegisterType<SomeType>(new ContainerControlledLifetimeManager());
```

everything is simple. Registered type is ``SomeType`` and Unity will resolve it as container controlled singleton.

### Mapping registration

This is the most common scenario for dependency injection using Unity. It involves registering a mapping between types such as an interface or a base class and a corresponding concrete class that implements or inherits from it.
When type is registered as a mapping:

```C#
RegisterType<IService, SomeType>();
```

**Registered** type (used to be called **From** type) is always the first in the sequence, in this case `IService`. Registration like this tells Unity that when `IService` is requested it should resolve it as ``SomeType`` and return as `IService`.
When next time you call ``Resolve<IService>()`` Unity performs following tasks:

- Checks if ``SomeType`` is registered and if yes, resolves that registration
- If ``SomeType`` is not registered Unity creates it and returns to the caller

In the example above ``SomeType`` is registered as a container controlled singleton, so it will always resolve the same instance.

In this example:

```C#
RegisterType<IService, Service>();
```

registered type ``IService`` is mapped to type ``Service``. No lifetime manager is provided so every time ``IService`` is created Unity constructs a new ``Service`` object and returns it as ``IService`` to the caller.

Now, if you want to assign a lifetime to this registration like this:

```C#
RegisterType<IService, Service>(new ContainerControlledLifetimeManager());
```

it tells Unity to resolve ``IService`` as usual and store result in ``ContainerControlledLifetimeManager``. So next time you call ``Resolve<IService>`` Unity will locate registration for ``IService`` and check if associated ``ContainerControlledLifetimeManager`` has instance already stored in it. If yes, it will simply return that instance.