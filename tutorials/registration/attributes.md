# Using Injection Attributes
One of the most useful and powerful techniques when using Unity is to take advantage of dependency injection for the parameters of class constructors and methods, and for the values of properties. This approach allows you to resolve and populate the entire hierarchy of objects used in your application based on type registrations and mappings defined in the container, with the subsequent advantages this offers.

You can specify constructor, property, and method call injection information in configuration or by adding registrations to the container at run time. You can also apply attributes to members of your classes. When you resolve these classes through the container, Unity will generate instances of the dependent objects and wire up the target class with these instances.

Unity performs constructor injection automatically on resolved classes, choosing the most complex constructor and populating any parameters for which you do not provide values when it constructs the object. You can also specify which constructor Unity should use to construct the object. For more information, see Annotating Objects for Constructor Injection.

Property and method call injection do not occur automatically unless you have registered injection types in the container at design time or run time. If you have not registered injection types in the container, you can add attributes to the members of your resolved class to force injection of dependent objects when the target class is resolved. For more information, see Annotating Objects for Property (Setter) Injection and Annotating Objects for Method Call Injection.

https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff660875(v%3dpandp.20)