---
uid: Tutorial.Annotation.Constructor
title: Annotating Type for Constructor Injection
---

# Selecting Constructor

To select constructors you create through the Unity container, you can use the following three techniques:

* [Automatic Constructor Injection](xref:Tutorial.Selection.Constructor). With this technique, you allow the Unity container to select a constructor and to satisfy any constructor dependencies defined in parameters of the constructor automatically. For more information see <xref:Tutorial.Selection.Constructor>.

* [Constructor Injection using explicit registration](xref:Tutorial.Injection.Constructor). With this technique, you register the [Type](xref:System.Type) and apply an [Injection Constructor Member](xref:Unity.Injection.InjectionConstructor) that specifies the dependencies to the registration. For more information see <xref:Tutorial.Injection.Constructor>

* **Annotated Constructor Injection**. With this technique, you apply attributes to the class constructor(s) that specify the injection configuration.

## Annotated Constructor Injection

Constructor Injection with Attribute Annotation allows you to apply attributes to the class' constructor designating it for dependency injection. When creating the class, Unity will always (unless explicitly overwritten in Registration) use that constructor. You only need to use this technique when there is more than one constructor in the target type.

### Annotating a Constructor

When a target class contains more than one constructor and the automatic algorithm does not provide desired selection, you may use the [InjectionConstructor](xref:Unity.InjectionConstructorAttribute) attribute to specify the constructor you wish to use for injection.

Consider the following [Type](xref:System.Type):

[!code-csharp [class Service](../../src/SpecificationTests/src/Constructor/Attribute/Setup.cs#class_service)]

In this example type `Service` contains four public constructors. Three of these constructors have one parameter each. A [Type](xref:System.Type) like this creates an ambiguity that Unity could not resolve by itself.

> [!WARNING]
> During resolution, the container will pick the first encountered constructor it could satisfy with dependencies and will use it. In the example above, it could be any of the three constructors with one parameter.

> [!NOTE]
> If Diagnostic is enabled Unity will throw an exception reporting ambiguous constructors.

Normally, Unity would select the third constructor with three parameters, but by annotating the second constructor with the attribute you force Unity to use it during resolution.

### Overriding constructor selection

Attribute annotated types are not required to be registered with the Unity container to participate in dependency injection. At runtime, Unity will use reflection to discover all required information to create objects of that type.

Sometimes you might be required to use attribute annotated type in a way not intended by the original designer. For example, if you want to create type `Service` from the example above using a different constructor. You may do so by registering the type with the container and passing [InjectionConstructor](xref:Unity.Injection.InjectionConstructor) injection member to registration method:

```cs
c.RegisterType<MyObject>("Special", Invoke.Constructor() )
```

In this example, you create a registration for type `Service` with name `"Special"` and instruct Unity to select default constructor. When registration has explicitly defined by injection member constructor, Unity will ignore [InjectionConstructor](xref:Unity.InjectionConstructorAttribute) attribute and use injected constructor instead.
