# Dependency Handling Example
## Introduction
> This Example is only applicable for Object and Data Dependency.

Let us consider this `Workspace` in Visual Studio Code where I have setup 2 Extensions named `A` and `B`

![Workspace](../Image%20Archive/DataDependency.1.png)

Let us consider the `Test Codeunit` with Object ID `50200` has been declared in Extension `A` and use it in `CustomerCard` with Object ID `50200`
```
codeunit 50200 "Test Codeunit"
{
    procedure GetCustomerBalance(CustomerNo: Code[20]): Decimal
    var
        Customer: Record Customer;
    begin
        Customer.Get(CustomerNo);
        Customer.CalcSums(Balance);
        exit(Customer.Balance);
    end;
}

```
```
namespace DefaultPublisher.B;

using Microsoft.Sales.Customer;

pageextension 50200 CustomerCard extends "Customer Card"
{
    trigger OnOpenPage();
    var
        TestCodeunit: Codeunit "Test Codeunit";
    begin
        Message(Format(TestCodeunit.GetCustomerBalance(Rec."No.")));
    end;
}
```
## Let us Break the Code...
Let us break the code by making a signication change to the `GetCustomerBalance` Procedure Declared in the `Test Codeunit`.

```
codeunit 50200 "Test Codeunit"
{
    procedure GetCustomerBalance(CustomerRec: Record Customer): Decimal
    begin
        CustomerRec.CalcSums(Balance);
        exit(CustomerRec.Balance);
    end;
}

```
As you can see, the `Procedure`'s Parameter has changed from `CustomerNo` to `CustomerRec` which is of Record Datatype. This has caused the code in the `CustomerCard` Page Extension to fail.

![Alt text](../Image%20Archive/DataDependency.2.png)
![Alt text](../Image%20Archive/DataDependency.3.png)

As soon as the breaking change was made, using the `Procedure` in Extension `B` has indicated that there is an error. This is the easiest method to identify breaking changes which occur in one Extension but is reflected in another Extension.

## Let us Fix the Broken Code
There are 2 primary methods to solve the broken code issue. 

1. Solve issue at the `Source`, i.e, Revert the Code back to the old format accepting the `CustomerNo` of `Code[20]` Datatype
2. Solve issue at the `Fault`, i.e, Altering Code in the `CustomerCard` Page Extension to pass `Rec` as the parameter.

## Which is the Best Solution?
A formal Investigation has to be conducted before arriving at a conclusion. The Pros and Cons of Altering code should be noted and proper weightage should be given to each pro and con.

### Alter Code at Fault when...
1. The Code has to be changed or else the To-Be-Developed Code will not work
2. The Code which existed before was affecting performance
3. The Code which existed before was did not work correctly

### Alter Code at Source when...
1. The Code has been used in many different Extensions or referenced too many times to individually fix in all the referenced locations
2. The new code would break the original purpose of the code.
3. The new code would negatively affect performance.
4. The new code is not as per Coding Standards Generally Followed in Business central.
___
[Back To Top](#introduction)<Br>
[Back to Index](../Index.md)<Br>
[Previous Page](./Introduction.md)<Br>
[Next Page](./BehaviorDependencyHandlingExample.md)