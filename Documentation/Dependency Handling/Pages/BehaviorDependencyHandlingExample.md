# Behavior Dependency Handling
## What is a Behavior
A Combination of Input -> Process -> Output which is expected to give Output in a specific way is called a Behavior. 
## Example
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

Let us change the `Balance` Field used under the `CalcSums` to `Balance (LCY)` Field.
```
codeunit 50200 "Test Codeunit"
{
    procedure GetCustomerBalance(CustomerNo: Code[20]): Decimal
    var
        Customer: Record Customer;
    begin
        Customer.Get(CustomerNo);
        Customer.CalcSums("Balance (LCY)");
        exit(Customer."Balance (LCY)");
    end;
}
```
![Alt text](../Image%20Archive/DataDependency.4.png)

>⚠️It is clear that the `AL Compiler` does not find any breaking change in the `Workspace`.
Note that this can be very dangerous if there is code written using the `GetCustomerBalance` Procedure assuming that it uses the Data from the `Balance` Field of the `Customer` Table. 

## How to Identify Silent Code Breakage?
There is no straight forward way to identify Silent Code Breakage. The only way is to...\
1. Identify All Extension's Depending on Extension `A`.
2. Check if the `GetCustomerBalance` Procedure has been used in any of the Extensions.
3. Manually Verify if the newly changed code would negatively affect the `Behavior` of the Extension's Depending on Extension `A`.

## Let Us Fix Silent Code Breakage
### Alter Code at the Source
1. Declare a New Procedure in the `Test Codeunit` 
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
    procedure GetCustomerBalanceLCY(CustomerNo: Code[20]): Decimal
    var
        Customer: Record Customer;
    begin
        Customer.Get(CustomerNo);
        Customer.CalcSums("Balance (LCY)");
        exit(Customer."Balance (LCY)");
    end;
}
```
2. Alter the Procedure to handle both Requests and handle the Resulting Code Breakage as an Object Dependency as mentioned in the [DependencyHandlingExample](./DependencyHandlingExample.md) Page.
```
codeunit 50200 "Test Codeunit"
{
    procedure GetCustomerBalance(CustomerNo: Code[20]; isLCY : Boolean): Decimal
    var
        Customer: Record Customer;
    begin
        Customer.Get(CustomerNo);
        if isLCY then Begin
            Customer.CalcSums(Balance);
            exit(Customer.Balance);
        end
        else Begin
            Customer.CalcSums("Balance (LCY)");
            exit(Customer."Balance (LCY)");

        end;
    end;
}
```
>ℹ️ Opting for this method would ensure that the Newly Developed Code is functional along with the Dependent Extension's Stability.

### Changing the Dependent Extension's Code
>ℹ️ Note that this is a very expensive method and prone to risks such as leading to more Code Breakage. Extensive Regression testing has to be performed to prove that no Functionality is broken.

___
[Back To Top](#what-is-a-behavior)<Br>
[Back to Index](../Index.md)<Br>
[Previous Page](./DependencyHandlingExample.md)