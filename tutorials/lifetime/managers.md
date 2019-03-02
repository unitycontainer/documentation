# Lifetime Managers
Out of the box Unity supports eight lifetime managers. These managers allow various scenarios of lifetime management for resolved objects and should satisfy most of everyday requirements. As everything with Unity, any of these managers could be extended or new managers could be created to cover specific needs. These are the managers Unity comes with:

## [Transient](xref:Unity.Lifetime.TransientLifetimeManager)
This is a default lifetime manager in Unity Container. If you do not specify any lifetime managers during registration, Unity will use this one implicitly. The default behavior of this manager is to create new instance of registered type on every resolution. 

It is recommended to omit this type of managers from registrations and let Unity assume default, it is hardly worth it to create instance of the manager which will be discarded during registration anyway.

## [Singleton](xref:Unity.Lifetime.SingletonLifetimeManager)
This lifetime manager creates globally unique singleton. No matter where it is registered (child or root container) it is always stored with the root container and becomes globally available in entire scope tree.

Any Unity container tree (parent and all the children) is guaranteed to have only one singleton for the registered type and overriding registration on root or any child container with singleton manager will override it everywhere.

This lifetime manager could be used on any types of registration, Type, Instance, or Factory. For more information see tutorial.

## Per Container
## Per Container Transient
## Hierarchical
## External
## Per Thread
## Per Resolve


https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff660872(v%3dpandp.20)