

# Development
## Extensions for AL Programming
* All basic and necessary extenions can be found by searching `AL` in the extension marketplace and Installing the `AL Extension Pack` Created by Waldo
![Alt text](image.png)
## Commit Code
### Why Code is Committed?
* As a Rule of Thumb, When working with Multiple Developers on a Project or Support Ticket, End of Day Commit `EODC` should be followed.
* Regardless of the status of Development, All code must be committed to the Branch to avoid Loss of Code.
### How to Commit Code?
* Committing Code follows some standard Procedures which must be followed to ensure a stable and Developer Friendly Repository
* A Commit Message is the most important part of committing. The Message can handle Multiple Lines, but only the First line is displayed as a Title in Azure DevOps and GitHub.
* Keep the limit for max characters typed in a single line to 50 Characters.
* Do not Bulk Commit Code as it may lead to confusing Commit Messages and will Make Rolling back on a Commit more difficult.
## Dependency Handling
* When working with Extensions with Other Extensions Depending on it, Making or Breaking Code is not far away from each other.
* Changes made in One Extension may reflect badly in its Dependent Extensions.
* There are 2 ways to handle Dependent Extensions. [Manual Method](#manual-method) and the [Automatic Method](#automatic-method)
* Let us assume that the worst has happened and our code change in the Main Extension is breaking the code in the Dependent App. There are 2 ways to handle this issue.
* The first would be to simply make alterations to the code in the Main Extension such that the Code in the Dependent Extension is left unaffected.
* The second method is to make necessary changes in the Dependent Extension to fix the broken code. 
* If the second method is followed, then the Dependent Extension would also have to be considered a Main app and would have to carefully handled in Deployment. Both Apps must be published one after the other depending on the Dependency Relationship between the two.
### Manual Method
* Develop the Main Extension and perform the Build Action with an updated Version Number
* Copy the .app File of the Main Extension and Paste it into the .alpackages folder of the Dependent Extension.
* Open the app.json File of the Dependent Extension and update the Dependencies Section with the correct version of the Main app.
* Perform a Developer Reload if Necessary for the AL compiler to check and notify if any code is broken.
### Automatic Method
* Visual Studio code offers a powerful feature that helps the AL Compiler check for any broken code in dependent extensions in real-time development.
* Add Both the Main and the Dependent Extension as Workspace Folders and continue Development.
* Visual Studio Code will notify immediately if any code change made in Main Extension is breaking code in the Dependent App.

