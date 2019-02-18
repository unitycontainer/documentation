# Lifetime Managers
Unity uses lifetime managers to control lifetime of objects it creates. It includes several lifetime managers that you can use directly in your code, but you can also create your own lifetime managers to implement specific lifetime scenarios. 
## TransientLifetimeManager
For this lifetime manager Unity creates and returns a new instance of the requested type for each call to the **Resolve** method. This lifetime manager is used by default for all types registered using the **RegisterType** method where no specific manager has been provided. When registering transient types it is not necessary to pass instance of ``TransientLifetimeManager`` to the registration.
Example:
```C#
RegisterType<Service>();
RegisterType<IService, Service>();
```
## ContainerControlledTransientManager
For this lifetime manager Unity creates and returns a new instance of the requested type for each call to the **Resolve** method. This lifetime manager is similar to **TransientManager** with the only difference that it holds reference to each created disposable instance and disposes these when container is disposed.
This manager is useful when used in session based designs with child container associated with the session. 
## ContainerControlledLifetimeManager
This manager registers an existing or resolved object as a singleton instance in the container the object of instance are registered. For this lifetime manager Unity returns the same instance of the registered type or object each time you call the **Resolve** method or when the dependency mechanism injects instances into other classes. This lifetime manager effectively implements a singleton behavior for objects. Unity uses this lifetime manager by default for the **RegisterInstance** method if different lifetime manager was not specified. 

If you want singleton behavior for an object that Unity will create when you specify a type mapping in configuration or when you use the **RegisterType** method, you must explicitly specify this lifetime manager.

If you registered a type mapping using configuration or using the **RegisterType** method, Unity creates a new instance of the registered type during the first call to the **Resolve** method or when the dependency mechanism injects instances into other classes. Subsequent requests return the same instance.

If you registered an existing instance of an object using the **RegisterInstance** method, the container returns the same instance for all calls to **Resolve** or when the dependency mechanism injects instances into other classes, provided that one of the following is true:

- You have specified a container-controlled lifetime manager
- You have used the default lifetime manager while registering instance

Singleton is visible in the container it was registered and all children of that container. The singleton could be overridden in child containers.
```C#
RegisterType<Service>(new ContainerControlledLifetimeManager());           <-- Service is a singleton
RegisterType<IService, Service>(new ContainerControlledLifetimeManager()); <-- IService is a singleton
RegisterInstance(new OtherService());                                      <-- OtherService is a singleton
```
## SingletonLifetimeManager
The **SingletonLifetimeManager** lifetime manager creates globally available singletons. No matter where it is registered (any child container) it is always stored in root container and globally available in children tree.
Any Unity container tree (parent and all the children) is guaranteed to have only one global singleton for the registered type and overriding registration on root or any child container will override it everywhere.
## ExternallyControlledLifetimeManager. 
The **ExternallyControlledLifetimeManager** type provides generic support for externally managed lifetimes. This lifetime manager allows you to register type mappings and existing objects with the container so that it maintains only a weak reference to the instance it registers or creates when you call the **Resolve** method or when the dependency mechanism injects instances into other classes based on attributes or constructor parameters within that class. This allows other code to maintain the object in memory or dispose it and enables you to maintain control of the lifetime of existing objects or allow some other mechanism to control the lifetime. Using the **ExternallyControlledLifetimeManager** enables you to create your own custom lifetime managers for specific scenarios. Unity returns the same instance of the registered type or object each time you call the **Resolve** method or when the dependency mechanism injects instances into other classes. However, since the container does not hold onto a strong reference to the object after it creates it, the garbage collector can dispose of the object if no other code is holding a strong reference to it.
## HierarchicalLifetimeManager. 
For this lifetime manager, as for the **ContainerControlledLifetimeManager**, Unity returns the same instance of the registered type or object each time you call the **Resolve** method or when the dependency mechanism injects instances into other classes. The distinction is that when there are child containers, each child resolves its own instance of the object and does not share one with the parent. When resolving in the parent, the behavior is like a container controlled lifetime; when resolving the parent and the child you have different instances with each acting as a container-controlled lifetime. If you have multiple children, each will resolve its own instance.
```C#
RegisterType<Service>(new HierarchicalLifetimeManager());                <-- Service is a per child singleton
RegisterType<IService, Service>(new HierarchicalLifetimeManager());      <-- IService is a per child singleton
RegisterInstance(new OtherService(), new HierarchicalLifetimeManager()); <-- OtherService is a per child singleton
```
## PerResolveLifetimeManager. 
For this lifetime manager the behavior is like a **TransientLifetimeManager**, but also provides a signal to the default build plan, marking the type so that instances are reused across the build-up object graph. In the case of recursion, the singleton behavior applies where the object has been registered with the **PerResolveLifetimeManager**.
## PerThreadLifetimeManager. 
For this lifetime manager Unity returns, on a per-thread basis, the same instance of the registered type or object each time you call the **Resolve** method or when the dependency mechanism injects instances into other classes. This lifetime manager effectively implements a singleton behavior for objects on a per-thread basis. **PerThreadLifetimeManager** returns different objects from the container for each thread.

If you registered a type mapping using configuration or using the **RegisterType** method, Unity creates a new instance of the registered type the first time the type is resolved in a specified thread, either to answer a call to the **Resolve** method for the registered type or to fulfill a dependency while resolving a different type. Subsequent resolutions on the same thread return the same instance.
