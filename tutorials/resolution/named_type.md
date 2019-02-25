# Resolving an Object by Type and Registration Name
Unity provides a method named Resolve that you can use to resolve an object by type, and optionally by providing a registration name. Registrations that specify a name are referred to as named registrations. This topic describes how to use the Resolve method to resolve types and mappings registered as named registrations. For information about resolving default registrations, see [Resolving an Object by Type](type.md).

## The Resolve Method Overloads for Named Registrations
The following table describes the overloads of the Resolve method that return instances of objects based on named registrations and mappings with the container. The API for the Unity container contains both generic and non-generic overloads of this method so that you can use it with languages that do not support the generics syntax.
| Method | Description |
| :----- | ----- |
| `Resolve<T>(string name)` | Returns an instance of the type registered with the container as the type T and with the specified name. Names are case sensitive. |
| `Resolve(Type t, string name)` | Returns an instance of the type registered with the container as the type t and with the specified name. Names are case sensitive. |
| | |

## Using the Resolve Method with Named Registrations
If you need to create multiple registrations for the same type, you can specify a name to differentiate each registration. Then, to retrieve an object of the appropriate type, you specify the name and the registered type. Typically you will register a type mapping between an interface and a concrete type that implements it, or between a base class and a concrete type that inherits it.

## Resolving Generic Types by Name
You can also resolve generic types by name, just as you do with non-generic types.

You cannot resolve unbound generic types. When an instance is created by Unity, concrete type arguments replace all of the generic type parameters. For more information see [Resolving Generic Types](generics.md)