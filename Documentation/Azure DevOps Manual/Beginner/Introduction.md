# Introduction
## What is Azure DevOps?
Azure DevOps is a Cloud Storage Solution which offers Source Code Version Control and General Operations commnly used for Projects
### What is Version Control?
Let us take Instagram as an example. At any given point in time there will be a version of the app published in Google Play Store or App Store to the Public. This app would have some specific code which makes the app behave in the intended way.

When a new User Interface is planned and is to be developed, the developer would take a copy of the currently published app's Source code. The Developer then makes a few changes to the code and is submitting the code for review. 

If all testcases and reviews pass with flying colors, the Code is then published. The moment the new User Interface code is published, it would become the primary source code.

And if a Developer wants to make changes to the chat system, they would copy the newly updated source code with the User Interface Changes. This cycle would go on and on till the end of time or as we know it... The End Of Internet 🤣

This is known as source code version control, where until the newly developed code is published, the previous source code stays intact.

### What if the Developer Screws up?
Let us assume that when the Developer made some changes to the UI in Instagram, they removed a button by mistake and it went unnoticed. When complaints start flooding in from Instagram Users, that the Settings Button got removed, immediately the latest Released Code is checked and the Developer Realizes their Mistake. Due to the critical nature of the issue, releasing a fix for the problem would take too long, then next best thing to do is to Rollback the Latest Release.

<B>What is RollBack?</B>
Since Instagram Developers were smart enough to use DevOps, The older app's source code was still saved and they were able to reverse the New Update to release the older app back to the public. This process would have been very difficult to do if the Older App's Source Code was lost.

## DevOps in Action
The Source code is stored in the Instagram repository's Main Branch in Azure DevOps.\
![Image1](<../Image Archive/Beginner.Introduction.1.png>)

Assume that this is the Source Code For Instagram:
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
When the Developer Wants to add new Code, They would create a copy of the Source code, a.k.a Create a new Branch using the main branch as Source.\
![Image2](../Image%20Archive/Beginner.Introduction.2.png)

Assume that this is the source code for the new code
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
    NewLikeButton() #New Code Added
    Advertisements()

Publish(Main.py)
```

After Updating the new code in the newly created branch, this would be the result when comparing main Branch and the New Branch.\
![Alt text](../Image%20Archive/Beginner.Introduction.3.png)

When the new code is approved and released to the public, the new code would be moved from the new branch to the Main Branch. This makes the code official and final.
> This process is performed by using the help of Pull Requests, where the source code from New Branch is pulled into the Main branch.

![Alt text](../Image%20Archive/Beginner.Introduction.4.png)

Clicking on the Create Button on the Top Right would merge the code from both branches and save it in the Main branch

![Alt text](../Image%20Archive/Beginner.Introduction.5.png)

Clicking on the Complete Button Would begin the Merging Process

![Alt text](../Image%20Archive/Beginner.Introduction.6.png)

Ticking the Delete Option would delete the New Branch when the merge is complete.
This Would be the source code after completing the Pull request.
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
    NewLikeButton()
    Advertisements()

Publish(Main.py)
```
___
[Back to Top](#introduction)\
[Previous Page](../index.md)\
[Next Page](Introduction.FailCondition.md)\
[Back to Index](../index.md)