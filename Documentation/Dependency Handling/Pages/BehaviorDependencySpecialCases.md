# Behavior Dependency Special Cases
## Case 1 - Two Extensions Developed in Different Branches
Let us consider this `Workspace` in Visual Studio Code where I have setup 2 Extensions named `A` and `B`

![Workspace](../Image%20Archive/DataDependency.1.png)

Note that I have 2 other Branches named `Feature_A` and `Feature_B` where Different Developers are Developing in Different Branches using Extensions `A` and `B`.

![Alt text](../Image%20Archive/DataDependency.5.png)

### Developer A Perspective
If Behavior Checking is performed by `Developer A` working on Branch `Feature_A`, this is the code they would be checking...

```
//Cod50200.TestCodeunit.al

codeunit 50200 "Test Codeunit"
{
    procedure GetCustomerBalanceLCY(CustomerNo: Code[20]): Decimal
    var
        Customer: Record Customer;
    begin
        Customer.Get(CustomerNo);
        Customer.CalcSums("Balance");
        exit(Customer."Balance");
    end;
}

//Pag-Ext50200.CustomerCard.al

namespace DefaultPublisher.B;

using Microsoft.Sales.Customer;

pageextension 50200 CustomerCard extends "Customer Card"
{
    trigger OnOpenPage();
    var
        TestCodeunit: Codeunit "Test Codeunit";
    begin
        Message(Format(TestCodeunit.GetCustomerBalanceLCY(Rec."No.")));
    end;
}
```
`Developer A` Concludes that Behavior Dependency Exists but no Functionality is Broken
### Developer B Perspecitve
If Behavior Checking is performed by `Developer B` working on Branch `Feature_B`, this is the code they would be checking...
```
//Cod50200.TestCodeunit.al

codeunit 50200 "Test Codeunit"
{
    procedure GetCustomerBalanceLCY(CustomerNo: Code[20]): Decimal
    var
        Customer: Record Customer;
    begin
        Customer.Get(CustomerNo);
        Customer.CalcSums("Balance (LCY)");
        exit(Customer."Balance (LCY)");
    end;
}
//Pag-Ext50200.CustomerCard.al

namespace DefaultPublisher.B;

using Microsoft.Sales.Customer;

pageextension 50200 CustomerCard extends "Customer Card"
{
    trigger OnOpenPage();
    var
        TestCodeunit: Codeunit "Test Codeunit";
    begin
        Message(Format(TestCodeunit.GetCustomerBalanceLCY(Rec."No.")));
        if TestCodeunit.GetCustomerBalanceLCY(Rec."No.") < 200 then
            Message('Balance Too Low');
    end;
}
```
`Developer B` Concludes that Behavior Dependency Exists but no Functionality is Broken

### Summary
The Code sample from 2 different branches prove that `Behavior Dependency` exists, but neither break Functionality, but in reality...

* `Developer A` has changed the `GetCustomerBalanceLCY` to use the `Balance` field instead of the original `Balancy (LCY)`.
* `Developer B` has changed the Page Extension `CustomerCard` to display a message by checking the `Balance (LCY)` field's Value.
* When Both Branches are merged into the `main` Branch or the `Release` Branch later, they would realize that `Developer A`'s changes would break the Functionality developed by `Developer B`.

### How to Avoid this Scenario?
Best Practice is for Both Developers to identify the Dependent Code During Design Phase and mutually agree to a plan like the [Code Sample](./BehaviorDependencyHandlingExample.md/#alter-code-at-the-source) Provided. This is called Impact Analysis.

### How to Identify Issue During Development?
1. Creating a new Branch named `Test_ExtAandBDependency` and pull both `Feature_A` and `Feature_B` branch into it.
2. Use Visual Studio Code `Workspace` and add both Extensions `A` and `B` to the `Workspace.`
3. Check all Instances where the `GetCustomerBalanceLCY` Procedure has been used in Extension `B`.
4. Use the `References` Functionality provided in Visual Studio Code to identify all References of the Procedure.

### How to Fix?
Refer the [Let Us Fix Silent Code Breakage](./BehaviorDependencyHandlingExample.md/#let-us-fix-silent-code-breakage) Section of the <B>Behavior Dependency</B> Page
___
[Back To Top](#behavior-dependency-special-cases)<Br>
[Back to Index](../Index.md)<Br>
[Previous Page](./BehaviorDependencyHandlingExample.md)<Br>
[Next Page](./HowToRemoveDataDependency.md)