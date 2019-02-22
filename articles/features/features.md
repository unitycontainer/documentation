# Dependency Injection with Unity
Using the Unity dependency injection container provides opportunities for you to more easily decouple components, business objects, and services you use in applications, and can simplify how you organize and architect these applications. This chapter provides overview of how Unity Container is initialized, used and disposed of in applications.



# Features

### Registration
* No registration required for simple POCO types
* Registration/updates at any time (no builder required)
* Supports registration metadata
* Supports generic types
* Register existing objects 
* Custom Type factories
* Type mappings
  * Register as a `Type`
  * Supports `Type` polymorphism
  * Register as an implemented interface
  * Multiple interfaces of the same `Type`
* Register Type
  * Constructor selection
    * Constructor marked by attribute
    * 'Smart' constructor selection
      * Longest constructor Unity can satisfy with parameters (dynamic)
      * Legacy longest constructor (Extension)
    * Specific constructor (Injection Member)
      * By types of parameters
      * By injected members
      * By provided values
  * Initializing properties
    * Marked with attribute
    * Injected during registration (Injection Member)
  * Initializing fields
    * Marked with attribute
    * Injected during registration (Injection Member)
  * Calling methods on the object
    * Marked with attribute
    * Injected during registration (Injection Member)
      * By types of parameters
      * By injected members
      * By provided values

### Existing Registrations
* Lists registrations of the container
* Supports registration hierarchies

### Check if `Type` is registered
* Fast and efficient algorithm


### Initialization of existing objects (BuildUp)
* Performs initialization on already created objects
* Follows the same pattern as create (Resolve) object
* Compatible with Activator and Compiled pipelines
* Initializes Properties and Fields
* Calls methods and injects parameters

### Create Instances (Resolve)
* Injects constructor with parameters
* Initializes Properties and Fields
* Calls methods and injects parameters
* Supports Activator pipelines
* Creates optimized (compiled) pipelines
* Seamlessly resolves registered instances or creates new objects
* Built-in support for deferred resolution
  * `Func<T>` 
  * `Lazy<T>` 
* Built-in support for collections
  * `T[]`
  * `IEnumerable<T>`
* Automatic concrete types resolution
* Dependency injection
  * Required
  * Optional
  * Supports Default parameters
  * Injects with resolved parameters
  * Injects with registered values
  * Supports parameter overrides
* Open-generics types
  * constraints
  * variance
  * nested
  * recurring generic definitions

### Manages lifetime of objects
* Transient
* Singleton
* Per Container
* Per Container Transient
* Hierarchical
* External
* Per Thread
* Per Resolve
* Other (Extension)

### Create child (Scoped) containers
* Creates disposable child containers (scopes)

### Extensible
* Validation
* Legacy behavior
* Configuration
* Interception
* Other