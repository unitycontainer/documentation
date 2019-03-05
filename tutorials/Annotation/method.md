---
uid: Tutorial.Annotation.Method
---

# Annotating types for Method invocation

Method invocation is an optional step you can add to the created object's initialization. Any accessible method could be invoked, provided Unity can satisfy all the parameters with appropriate values.

## Method Invocation

To enable method invocation during object initialization you could apply [InjectionMethod](xref:Unity.InjectionMethodAttribute) attribute to the method you want to be executed.

```cs
public class Service
{
    ...
    private void PreInitialize(...)
    {
        ...
    }

    [InjectionMethod]
    public void Initialize(...)
    {
        ...
    }

    public void PostInitialize(...)
    {
        ...
    }
}
```

In example above attribute [InjectionMethod](xref:Unity.InjectionMethodAttribute) is applied to method `Initialize(...)` and the method will be executed immediately after the object is created.

## Multiple Method Invocation

Unity does not place any restrictions on how many methods of the class will be invoked during the initialization. You could mark any and all methods with the attribute and Unity will execute them all:

```cs
public class Service
{
    ...

    [InjectionMethod]
    public void PreInitialize(...)
    {
        ...
    }

    [InjectionMethod]
    public void Initialize(...)
    {
        ...
    }

    [InjectionMethod]
    public void PostInitialize(...)
    {
        ...
    }
}
```

## Annotating `private` and `protected` methods

Although it is technically possible to call `private` and `protected` methods of the class, Unity does not support this feature. This restriction is implemented to impose consistency with accessibility principles of `C#` language.

Unity will ignore attributes on non accessible methods.

```cs
public class Service
{
    ...

    [InjectionMethod]
    protected void ProtectedMethod(...)
    {
        ...
    }
}
```

In example above method `ProtectedMethod(...)` will not be called.

If [Unity Diagnostic](xref:Tutorial.Unity.Diagnostic) is enabled, the container will throw an exception when it encounters such an annotation. For more information see  [Unity Diagnostic](xref:Tutorial.Unity.Diagnostic).