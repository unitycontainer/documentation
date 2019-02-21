# Dependency Injection with Unity
Using the Unity dependency injection container provides opportunities for you to more easily decouple components, business objects, and services you use in applications, and can simplify how you organize and architect these applications. This chapter provides overview of how Unity Container is initialized, used and disposed of in applications.



# Features
Instance
Factory
Type
Mapping

## Container

* Register interface
* type mapping
* additionally supported: 
  * registering service once, 
  * registration update, 
  * removing registration.
* Register user-defined delegate factory and register existing instance.
* Register implementation types from provided assemblies with automatically determined service types.
* Register with service key of arbitrary type, or register multiple non-keyed services.
* Register with resolution condition.
* Register with associated metadata object of arbitrary type.

* Resolve and ResolveMany.
  * Unknown service resolution: 
  * Optional automatic concrete types resolution

* Instance lifetime control or Reuse in DryIoc terms: 
  * Nested disposable scopes with optional names
  * Ambient scope context

* Supported out-of-the-box: Transient, Singleton, Scoped in multiple flavors, including scoped to specific service in object graph
* useParentReuse and use useDecorateeReuse option for injected dependencies
* Control reused objects behavior with preventDisposal and weaklyReferenced.
* Extensive Open-generics support: constraints, variance, complex nested, recurring generic definitions
* Constructor, and optional property and field injection.
* Static and Instance factory methods in addition to constructor. Factory method supports parameter injection the same way as constructor!
Injecting properties and fields into existing object.
Creating concrete object without registering it in Container but with injecting its parameters, properties, and fields.
Generic wrappers: 
Service collections: T[], IEnumerable<T>, LazyEnumerable<T>, and I(ReadOnly)Collection|List<T>.
Other: Lazy<T>, Func<T>, Meta<TMetadata, T> or Tuple<TMetadata, T>, KeyValuePair<TKey, T>, and user-defined wrappers.
Currying over constructor (or factory method) arguments: Func<TArg, T>, Func<TArg1, TArg2, T>, etc.
Nested wrappers: e.g. Tuple<SomeMetadata, Func<ISomeService>>[].
Composite pattern: Composite itself is excluded from result collection.
Decorator pattern.