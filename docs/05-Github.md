## Github Integration

Version control helps software teams manage changes to source code over time. Version control software keeps track of every modification to the code in a special kind of database. If a mistake is made, developers can turn back the clock and compare earlier versions of the code to help fix the mistake while minimizing disruption to all team members. Version control systems have been around for a long time but continue to increase in popularity with data science workflows.

The RStudio IDE has integrated support for version control which would help us keep track of our changes and push them onto Github.

We'll now quickly look at how to setup a git version controlling environment within R Studio.

- **Create an account on github** : First you'll need to [create an account](https://github.com/join) on github.

- **Create a repository** : Once you're done creating an account, click on the `New Repository` option and create a repository there. Generally the name of the repository is the name of the project.

- **Download and install git locally** : Now you'll need to install git locally on your machine. You can download it from the [official git website](https://git-scm.com/downloads)

- **Update *Global Options* in R Studio** : Once you've installed git, navigate to the **Tools** --> **Global Options** --> **GIT/SVN** options and within the *Git Executable* provide the link to git executable file and of the SVN path.(by default it will be C:/Program Files/Git/bin/git.exe and C:/Users/**user_name**/Documents respectively)

- **Clone Github Repository** : Now within your filesystem, navigate to a new repository and type the following command

`git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git`

- **Initialize the current directory with a R Project** : In R Studio, navigate to the New Project option and choose the *Existing Directory* option to make the curret git directory as your project directory.

- **Check git origin** : Ensure that the name of the origin path is set correctly. Type the below command in cmd prompt.

`git remote show origin`

- **Make changes,commit and push** : Now you can try making changes into the repository by either adding new files or modifying the existing README file. To commit all the changes, type

`git add -A`
`git commit -m "A commit from my local computer"`
`git push`

At this point you'll be asked to enter your github username and password. Once you've entered that the changes which you've made in this commit will get pushed onto the github repository.



**Additional Resource**
- [Using Version Control with RStudio](https://support.rstudio.com/hc/en-us/articles/200532077-Version-Control-with-Git-and-SVN)

- [Happy Git and GitHub for the userR](http://happygitwithr.com/)
