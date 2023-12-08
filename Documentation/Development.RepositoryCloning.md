 # Introduction
 * Now that our platform is ready, let us bring in the code to start development. Directly editing code on the cloud repository is allowed in Azure DevOps, but not a recommented way of developing Extensions.
* Instead Cloning the Repository and opening the code with Visual Studio Code gives the advantage of the compiler verifying the code which prohibts Syntax Mistakes from being saved in the repository
# Cloning Repository
* To Clone a Branch from Azure DevOps, Select any Branch from the Branch List\
![Alt text](/Image%20Archive/Branch%20List.png)
* Click on the Clone Button on the Right side of corner of the Screen\
![Alt text](/Image%20Archive/Clone%20Branch%20Button.png)
* Click on the Clone in VSCode Option to directly import the Code using Visual Studio Code\
![Alt text](/Image%20Archive/Clone%20with%20VS%20Code.png)
* Using the Windows Folder Select Popup, Find an appropriate location for storing the cloned Repository. Example `Project\ProjectName\Repos\`
* Change the Branch from `main` to the required branch by clicking on the branch name on the bottom right side of the screen in Visual Studio Code\
![Alt text](/Image%20Archive/Branch%20Change.png)
* Before Beginning Development, execute a `Fetch` Command which checks if any updates have happened to the Cloud Repository after it was Cloned.
# Creating a New Branch
* If no Branch was created for Developing the requirement at hand, create a new Branch and set the Source Branch as the Main or Master Branch in Azure DevOps
* Click on the `New Branch` Button to trigger the Prompt\
![Alt text](/Image%20Archive/Create%20New%20Branch.png)
* Name the Branch as per the rules specified in the [Branch Rules](/Documentation/BranchNaming.md) Document


***
[Previous Page](/Documentation/Development.Prerequisites.md)\
[Next Page](/Documentation/Development.CodingStandards.md)\
[Back to Index](/Documentation/Handbook/Index.md)