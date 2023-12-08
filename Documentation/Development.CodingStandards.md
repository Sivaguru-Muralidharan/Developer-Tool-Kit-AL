## General Tips
1. Remove unused Variables to save memory\
![Alt text](/Image%20Archive/Remove%20Variables.png)
2. Use Findset in Looping
3. Don't check too many condition in a single IF statement. Split the condition and use multilple if statements if required.
4. Use Case Statement instead of if conditions if there are multiple outcomes to check and write code for.
```
if Color = 'Orange' then //code
if Color = 'Red' then //code
if Color = 'Blue' then //code
```
Can be Reformatted into
```
Case
    Color of
        'Red':
            //code
        'Orange':
            //code
        'Blue':
            //code
end;
```
## Never Nester
* Becoming a never nestor is hard, but it can be nesting code can be reduced by exiting code if certain contions fail at some step.
* Upto 3 Levels of Nesting is generally accepted in Programming.
* It also improves Code Readability.
```
if RecordVar.Field1 = 'Text' then Begin
    if RecordVar.Field2 = 10 then begin
        //code
    End;
End;
```
Can be Reformatted as
```
if (RecordVar.field1 = 'Text') and (RecordVar.Field2 = 10) then begin
    //code
End;
```
While Reading code, this lets the user know that code is skipped in the function if the Filtered Record variable does not contain data, rather than the Reader having to analyze all code depending on the situation.

## Lazy Evaluation
While checking conditions and performing actions based on the response, try and exit the code if the condition fails. This also helps in avoid unncessary code Nests.
```
if Recordvar.Findset then Begin
    Rec.Field1 := 1;
    Rec.Validate(Field2,'Hi');
    //... 200 Lines Later
    Rec.Insert(true)
end;
```
Can be Reformatted as
```
if not Recordvar.Findset then 
    exit;
Rec.Field1 := 1;
Rec.Validate(Field2,'Hi');
//... 200 Lines Later
Rec.Insert(true)
```

***
__The Following Pages will deal with specifics and advanced topics in Development__\
__Please Skip to the next section if you are a Beginner__\
[Previous Page](/Documentation/Development.RepositoryCloning.md)\
[Next Page](/Documentation/Development.DependencyHandling.md)\
[Skip Advanced Topics](/Documentation/Development.CommitCode.md)\
[Back to Index](/Documentation/Handbook/Index.md)
