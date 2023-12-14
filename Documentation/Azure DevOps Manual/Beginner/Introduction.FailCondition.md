# What if the Developer Makes a Mistake?
In the latest New Button Update to Instagram, a major bug in code made the settings button unusable. The only option to restore the functionality to the users as soon as possible is to revert the latest change to the Source Code.

![Alt text](../Image%20Archive/Beginner.Introduction.FailCondition.1.png)

Using the Revert Option Provided in the Completed Pull Request Page, the old source code can be restored.

![Alt text](../Image%20Archive/Beginner.Introduction.FailCondition.2.png)

A Temporary Branch is created to hold the old source code which is then merged back into the main branch effective reversing the changes made.

![Alt text](../Image%20Archive/Beginner.Introduction.FailCondition.3.png)

The Newly created Branch is immediately pulled into the main branch with a new pull request. The same procedure to finalize and complete a pull request is done.

This is the Reverted Source Code.
```
Import Dependency as Dependency
Import This as This
Import That as That

Model()
View()
Controllder()

def Controller():
    print("Connect DB")

def Model():
    DB = db.connect($Path)

def View():
    Header()
    Body()
    Footer()

def Body():
    FactBox()
    Data()
    Urls()
    Buttons()
    Advertisements()

Publish(Main.py)
```
___
[Back to Top](#what-if-the-developer-makes-a-mistake)\
[Previous Page](./Introduction.md)\
[Next Page]()\
[Back to Index](../index.md)