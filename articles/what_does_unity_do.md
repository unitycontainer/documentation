# What Does Unity Do?


By using dependency injection frameworks and inversion of control mechanisms, you can generate and assemble instances of custom classes and objects that can contain dependent object instances and settings. The following sections explain the ways that you can use Unity, and the features it provides:

* The Types of Objects Unity Can Create
* Registering Existing Types and Object Instances
* Managing the Lifetime of Objects
* Specifying Values for Injection
* Populating and Injecting Arrays, Including Generic Arrays
* Intercepting Calls to Objects

## The Types of Objects Unity Can Create
You can use the Unity container to generate instances of any object that has a public constructor (in other words, objects that you can create using the new operator), without registering a mapping for that type with the container. When you call the Resolve method and specify the default instance of a type that is not registered, the container simply calls the constructor for that type and returns the result.

Unity exposes a method named RegisterType that you can use to register types and mappings with the container. It also provides a Resolve method that causes the container to build an instance of the type you specify. The lifetime of the object it builds corresponds to the lifetime you specify in the parameters of the method. If you do not specify a value for the lifetime, the container creates a new instance on each call to Resolve. For more information see Registering Types and Type Mappings.
## Registering Existing Types and Object Instances
Unity exposes a method named RegisterInstance that you can use to register existing instances with the container. When you call the Resolve method, the container returns the existing instance during that lifetime. If you do not specify a value for the lifetime, the instance has a container-controlled lifetime, which means that it effectively becomes a singleton instance. For more information see Creating Instance Registrations.
## Managing the Lifetime of Objects
Unity allows you to choose the lifetime of objects that it creates. By default, Unity creates a new instance of a type each time you resolve that type. However, you can use a lifetime manager to specify a different lifetime for resolved instances. For example, you can specify that Unity should maintain only a single instance (effectively, a singleton). It will create a new instance only if there is no existing instance. If there is an existing instance, it will return a reference to this instead. There are also other lifetime managers you can use. For example, you can use a lifetime manager that holds only a weak reference to objects so that the creating process can dispose them, or a lifetime manager that maintains a separate single instance of an object on each separate thread that resolves it.

You can specify the lifetime manager to use when you register a type, a type mapping, or an existing object using design-time configuration, as shown in Specifying Types in the Configuration File or, alternatively, you can use run-time code to add a registration to the container that specifies the lifetime manager you want to use, as shown in Registering Types and Type Mappings and Creating Instance Registrations.
## Configuring Types for Injection into Constructors, Methods, and Properties
Unity enables you to use techniques such as constructor injection, property injection, and method call injection to generate and assemble instances of objects complete with all dependent objects and settings. For more information see Specifying Values for Injection and Registering Injected Parameter and Property Values.
## Example Application Code for Constructor Injection
As an example of constructor injection, if a class that you instantiate using the Resolve method of the Unity container has a constructor that defines one or more dependencies on other classes, the Unity container automatically creates the dependent object instance specified in the parameters of the constructor. For example, the following code shows a class named CustomerService that has a dependency on a class named LoggingService.
```C#
public class CustomerService
{
  public CustomerService(LoggingService myServiceInstance)
  {
    // work with the dependent instance
    myServiceInstance.WriteToLog("SomeValue");
  }
}
```
At run time, developers create an instance of the CustomerService class using the Resolve method of the container, which causes it to inject an instance of the concrete class LoggingService within the scope of the CustomerService class.
```C#
IUnityContainer uContainer = new UnityContainer();
CustomerService myInstance = uContainer.Resolve<CustomerService>();
```
## Example Application Code for Property (Setter) Injection
In addition to constructor injection, described earlier, Unity supports property and method call injection. The following code demonstrates property injection. A class named ProductService exposes as a property a reference to an instance of another class named SupplierData (not defined in the following code). Unity does not automatically set properties as part of creating an instance; you must explicitly configure the container to do so. One way to do this is to apply the Dependency attribute to the property declaration, as shown in the following code.
```C#
public class ProductService
{
  private SupplierData supplier;

  [Dependency]
  public SupplierData SupplierDetails
  {
    get { return supplier; }
    set { supplier = value; }
  }
}
```
Now, creating an instance of the ProductService class using Unity automatically generates an instance of the SupplierData class and sets it as the value of the SupplierDetails property of the ProductService class.
## Populating and Injecting Arrays, Including Generic Arrays
You can define arrays, including arrays of generic types, and Unity will inject the array into your classes at run time. You can specify the members of an array, or have Unity populate the array automatically by resolving all of the matching types defined in your configuration. You can then use the populated arrays as types to resolve directly, or to set the values of constructor and method parameters and properties. Arrays can be defined in configuration files or by adding the definitions to the container at run time using code.
For details and examples, see the sections on arrays in the following topics:
* Configuring Injected Parameter and Property Values
* Registering Injected Parameter and Property Values
* Registering Generic Parameters and Types
## Intercepting Calls to Objects
The best types in object oriented systems are ones that have a single responsibility. But as systems grow, other concerns tend to creep in. System monitoring, such as logging, event counters, parameter validation, and exception handling are just some examples of areas where this is common. These cross-cutting concerns often require large amounts of repetive code throughout the application and if your design choice changes, for example you change your logging framework, then the logging calls must be changed in many places throughout the code set.

Interception is a technique that enables you to add code that will run before and after a method call on a target object. The call is intercepted and additional processing can happen. When you perform this coding process manually, you are following what is commonly known as the decorator pattern. Writing decorators requires that the types in question be designed for it in the beginning, and requires a different decorator type for each type you are decorating.

The Unity interception system creates the decorators automatically. This allows you to easily reuse code that implements these cross-cutting concerns with minimal, if any, attention to what types the cross-cutting concerns will be applied to.
## Example Application Code
The following example configures the container at run time for interception of the type TypeToIntercept by using a VirtualMethodInterceptor interceptor with an interception behavior, ABehavior, and an additional interface to be implemented.
```C#
IUnityContainer container = new UnityContainer();
container.AddNewExtension<Interception>();
container.RegisterType<TypeToIntercept>(
        new Interceptor<VirtualMethodInterceptor>(),
        new InterceptionBehavior<ABehavior>(),
        new AdditionalInterface<IOtherInterface>());
```
You could then resolve an instance by using the following call:
```C#
TypeToIntercept instance = container.Resolve<TypeToIntercept>();
```
Now when calling methods on an instance, the code in the ABehavior class will be executed before and after any call to the instance.
