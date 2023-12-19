# Handle Data Dependency With RecRef and FieldRef
## Setup
1. Publish Extension `A` with the Table Required.
```
table 50200 "Test Table"
{
    Caption = 'Test Table';
    DataClassification = CustomerContent;

    fields
    {
        field(1; ID; Integer)
        {
            Caption = 'ID';
        }
        field(2; Name; Text[50])
        {
            Caption = 'Name';
        }
    }
    keys
    {
        key(PK; ID)
        {
            Clustered = true;
        }
    }
}
```
2. Prepare Extension `B` with the following Object
```
namespace DefaultPublisher.B;

using Microsoft.Sales.Customer;

pageextension 50200 CustomerCard extends "Customer Card"
{
    trigger OnOpenPage();
    var
        RecRef: RecordRef;
    begin
        RecRef.open(50200);
        Message(RecRef.Name);
    end;
}
```
> Note that the Object ID has been directly called instead of the Name of the Object. This Object ID is only checked at runtime and not during Compile Time

3. Publish Extension `B`

4. Upon Opening the `Customer Card`, the Name of the Table is Displayed

![Alt text](../Image%20Archive/DataDependency.6.png)

## What would happen if we Uninstall Extension A?
5. Uninstall Extension `A` using Extension Management

![Alt text](../Image%20Archive/DataDependency.7.png)

6. Extension `A` is uninstalled without Uninstalling Extension `B`

![Alt text](../Image%20Archive/DataDependency.8.png)

7. Try Opening the Customer Card Again. A runtime error occurs or the session might crash as Table `50200` does not exist in the database.

![Alt text](../Image%20Archive/DataDependency.9.png)

## Let's Solve the RunTime Issue...

1. Edit Extension B in Visual Studio Code. Add a Try Function and Handle the Runtime issue

```
namespace DefaultPublisher.B;

using Microsoft.Sales.Customer;

pageextension 50200 CustomerCard extends "Customer Card"
{
    trigger OnOpenPage();
    begin
        if not GetTestTable() then
            Message('Table Not Found. Check if Extension A is Installed');
    end;

    [TryFunction]
    local procedure GetTestTable()
    var
        RecRef: RecordRef;
    begin
        RecRef.open(50200);
        Message(RecRef.Name);
    end;
}
```
2. Publish the App and Open the `Customer Card`. The runtime issue is handled with a custom Message.

![Alt text](../Image%20Archive/DataDependency.10.png)

## Advantages of using Using RecordRef and FieldRef
* Extensions can be made with Disconnected Architecture and improve Modularity in an Eco System.

## Disadvantages of using RecordRef and FieldRef
* If the Object ID of the Source Table is changed, it might lead to wrong data being consumed.
* During Analysis of [Behavior Dependency Analysis](./BehaviorDependencyHandlingExample.md), Searching for Usage of Table with Table name would not work. The Search has to be done with Object ID.

___
[Previous Page](./HowToRemoveDataDependency.md)