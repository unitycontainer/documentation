---
uid: Tutorial.Injection.Constructor.Selection
title: Constructor Selection
---

# Constructor Selection

Selecting a constructor is the first step in creating a resolution pipeline. Unity supports various constructor selection methods. It can be configured to execute any accessible constructor with the following exceptions:

* `static` constructors are not supported
* `private` and `protected` constructors are not accessible
* Constructors with `ref` and `out` parameters are not supported

## Constructor Selection Algorithms

Selection is done in the following order:

### Automatic Selection

Automatic Selection is a default method of selecting constructors. It will be used if no constructor is injected or annotated.

By default Unity uses 'smart' algorithm to select constructor. It sorts all accessible constructors by number of parameters in ascending order and goes from most complex to the default, checking if it can satisfy its parameters. The container selects the first constructor it can create and executes it.

> [!WARNING]
> Unity will not check for ambiguities unless `Diagnostic` extension is installed.

> [!TIP]
> Legacy selection algorithm which selects the most complex constructor could be enabled by installing `Legacy` extension. It will replace and disable 'smart' selection.

### Constructor Annotation

Constructor annotated with [InjectionConstructor](xref:Unity.InjectionConstructorAttribute) overrides automatic selection. For more information see <xref:Tutorial.Annotation.Constructor>

> [!WARNING]
> Multiple constructor annotation is not supported.

### Constructor injection

Constructor configured for invocation during registration has highest priority. It will override other selection methods and will always execute configured constructor.



#### Default Constructor

No parameters

#### Selection By Parameter Types

Constructor has not name so only parameter types distinguish one from another.