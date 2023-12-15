# Introduction
Business Central Version's Following AL Programming can only extend the functionalities by using Extensions.
These Extensions are coded using AL Programming Language and are bundled into Packages with the `.app` Format
## What is Dependency Handling?
When There are multiple extensions being deployed into Business Central, sometimes one Extension may depend on another extension. proper usage and maintenance of these Extensions and their Dependencies is known as Dependency Handling

## Types of Dependencies
There are majorly 3 Types of Dependencies in Business Central
### Data Dependency
Data Dependency arises when we need data from a specific Table which is declared and published in a different Extension. 

>Example: We have 2 Apps named `A` and `B`. If the Table is declared in `A` and `B` wants to use the data for some calculations, then it would mean that App `B` is Dependent on `A` for Data.

### Object Dependency
Object Dependency Arises when we need to use any Object Declared in a different Extension. This would include the usage of
* Codeunits
* Reports
* Pages
* Tables
* XmlPorts\
and more...

>Example: We have 2 Apps named `A` and `B`. If a Report is declared in `A` and `B` wants to use the Report for as a part of its code, then it would mean that App `B` is Dependent on `A` for Data.

### Behavior Dependency
The Best way to explain Behavior Dependency is to use the Procedures.
Method Dependency is a specific type of Object Dependency where a `Procedure` declared in a different extension needs to be called in our extension.


>Example: We have 2 Extension named `A` and `B`. If the Procedure is declared in a codeunit in Extension `A` and `B` wants to use the Procedure for some calculations, then it would mean that Extension `B` is Dependent on `A` for the `Procedure`.

>⚠️ Procedures Take Certain Input, Process it and return a specific Output. The collection of a specific Input, Process and Output is called a Behavior. When any code changes the `Process` part, it effectively changes the behavior. This may result in Non Breaking Change which would affect the `Output` which may break `Functionality`.
## Summary
In All the Above mentioned cases, it would Technically Mean that
> |Extension|Dependency Extension|
> |--|--|
> |B|A|
```
//app.json File of App B
{
    "id": "900cbbd9-55a6-4529-80d4-edcb61d351b8",
    "name": "B",
    "publisher": "Default publisher",
    "version": "1.0.0.0",
    "dependencies": [
    {
        "appId": "46cd71e1-70c4-4974-8e87-64e8354c3f43",
        "name": "A",
        "publisher": "Default publisher",
        "version": "1.0.0.0"
    }],
}
```

When Downloading Symbols for working on Extension `B`, The `.alpackages` folder will have the sybol for Extension `A`.
> ⚠️ Without the presence of Extension `A`'s Symbol, Writing code with by using Extension `A`'s Objects, Data or Procedures will result in Errors and will not allow Extension `B` to be compiled for Deployment.

___
[Back To Top](#introduction)<Br>
[Back to Index](../Index.md)<Br>
[Next Page](./DependencyHandlingExample.md)