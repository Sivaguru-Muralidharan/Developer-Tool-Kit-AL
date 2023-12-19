# Handle Data Dependency with APIs
## Setup
1. Publish Extension `A` with `Test Table` and a `Page` for the `Test Table`
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
```
page 50200 "Test Page List"
{
    ApplicationArea = All;
    Caption = 'Test Page List';
    PageType = List;
    SourceTable = "Test Table";
    UsageCategory = Administration;

    layout
    {
        area(content)
        {
            repeater(General)
            {
                field(ID; Rec.ID)
                {
                    ToolTip = 'Specifies the value of the ID field.';
                }
                field(Name; Rec.Name)
                {
                    ToolTip = 'Specifies the value of the Name field.';
                }
            }
        }
    }
}
```
2. Publish the Page as a WebService. and copy the ODataV4 URL

![Alt text](../Image%20Archive/DataDependency.13.png)

3. Prepare Extension `B` with the Following object. Use the URL copied from the Webservice in your Code.
```
namespace DefaultPublisher.B;

using Microsoft.Sales.Customer;
using System.Text;
using System.Utilities;
using System.Reflection;

pageextension 50200 CustomerCard extends "Customer Card"
{
    trigger OnOpenPage();
    var
        Response: Text;
    begin
        if GetTestDataWithAPI(Response) then
            Message(Response)
        else
            Message('Extension A not Found')
    end;
    local procedure GetTestDataWithAPI(var Response: Text): Boolean
    var
        HttpClient: HttpClient;
        HttpResponse: HttpResponseMessage;
        URL: Text;
        AuthString: Text;
        TypeHelper: Codeunit "Type Helper";
        Base64: Codeunit "Base64 Convert";
    begin
        URL := 'http://bc230:7048/BC/ODataV4/Company(''CRONUS%20International%20Ltd.'')/TestPageList';
        AuthString := STRSUBSTNO('%1:%2', 'ADMIN', '*****');
        AuthString := Base64.ToBase64(AuthString);
        AuthString := STRSUBSTNO('Basic %1', AuthString);
        HttpClient.DefaultRequestHeaders().Add('Authorization', AuthString);
        IF HttpClient.Get(URL, HttpResponse) then
            HttpResponse.Content.ReadAs(Response);
        if Response <> '' then
            exit(true)
        else
            exit(false);
    end;
}
```
>Quick Explanation<Br>
>The HTTPClient Object is used to send the Request with the URL<Br>
>The HTTPResponse Object is used to Receive the Response
>Base64 Convert Codeunit is used to convert the Credentials required to access the data

4. Open Customer Card Page and View the Data

![Alt text](../Image%20Archive/DataDependency.11.png)

### What would happen if we Uninstall Extension A?
5. Uninstall Extension `A` using Extension Management

![Alt text](../Image%20Archive/DataDependency.7.png)

6. Extension `A` is uninstalled without Uninstalling Extension `B`

![Alt text](../Image%20Archive/DataDependency.8.png)

7. Open Customer Card. The Custom Message is Displayed

![Alt text](../Image%20Archive/DataDependency.12.png)

## Advantages of Using API
* Extensions can be made with Disconnected Architecture and improve Modularity in an Eco System.

## Disadvantages of Using API
* The API URL has to be made modular or it will not work in all the Environments
* The API Response has to be processed and consumed which would take time.
* The WebService Should be Published and Active
* During Analysis of [Behavior Dependency Analysis](./BehaviorDependencyHandlingExample.md), Searching for Usage of Table with Table name would not work. The Search has to be done with the APIs EntityName or EntitySetName

___
[Previous Page](./HowToRemoveDataDependency.md)