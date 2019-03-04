---
uid: Tutorial.Annotation.Constructor
---

# Annotating Objects for Constructor Injection

When classes are created, Unity provides following mechanisms to properly select and execute constructors:

* **[Automatic Injection](xref:Tutorial.Selection.Constructor)**. With this technique, you allow the Unity container to select the constructor and satisfy any dependencies defined in parameters of the constructor automatically. It will select most complex constructor it can satisfy with dependencies.

* **[Constructor Injection](xref:Tutorial.Injection.Constructor)**. With this technique, you provide [InjectionConstructor](xref:Unity.Injection.InjectionConstructor) injection member during registration of the type or the type mapping. This mechanism allows you to pick different constructor for each [Type Mapping](xref:Tutorial.Registration.Mapping) or each named registration you create.

* **[Constructor Injection Using an Attribute Annotation](xref:Tutorial.Annotation.Constructor#constructor-injection-using-an-attribute-annotation)**. With this technique, you apply attribute to the class constructor designating that constructor for dependency injection. When creating the class, Unity will always (unless explicitly overwritten) use that constructor. You only need to use this technique when there is more than one constructor in the target class.

## Constructor Injection Using an Attribute Annotation

When a target class contains more than one constructor and automatic selection process does not provide desired selection, you may use the [InjectionConstructor](xref:Unity.InjectionConstructorAttribute) attribute to specify the constructor you wish to use for injection.

Following example demonstrates this technique:

```cs
public class MyObject
{
  public MyObject(SomeOtherClass myObjA)
  {
    ...
  }

  [InjectionConstructor]
  public MyObject(MyDependentClass myObjB, string id)
  {
    ...
  }

  public MyObject(MyDependentClass myObjB, string id, ILogger logger)
  {
    ...
  }
}
```

In this example type `MyObject` contains three public constructors. Normally, Unity would select third constructor with three parameters, but by annotating second constructor with the attribute you force Unity to use it during resolution.

## Overriding constructor selection

Attribute annotated types are not required to be registered with the Unity container to participate in dependency injection. At runtime Unity will use reflection to discover all required information to create objects of that type.

Sometimes you might be required to use attribute annotated type in a way not intended by original designer. For example if you want to create type `MyObject` from example above using different constructor. You may do so by registering the type with the container and passing [InjectionConstructor](Unity.Injection.InjectionConstructor) injection member to registration method:

```cs
c.RegisterType<MyObject>("Special Case", 
                         Invoke.Constructor(typeof(SomeOtherClass)))
```

In this example you create registration for type `MyObject` with name `"Special Case"` and instruct Unity to select constructor that takes one parameter of type `SomeOtherClass`. When registration has explicitly defined by injection member constructor, Unity will ignore [InjectionConstructor](xref:Unity.InjectionConstructorAttribute) attribute and use injected constructor instead.

For more information see [Constructor Selection](xref:Tutorial.Selection.Constructor)