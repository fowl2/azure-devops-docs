---
title: Git and TFVC version control 
titleSuffix: Azure Repos
description: Choosing which version control to use in Azure Repos
ms.assetid: A4D7295A-22AB-4990-BE68-EF81A1C31F01
ms.technology: devops-code-tfvc
ms.author: apawast
author: apawast
ms.topic: conceptual
ms.date: 05/12/2017
monikerRange: '>= tfs-2015'
---



# Choosing the right version control for your project

#### Azure Repos | Azure DevOps Server 2019 | TFS 2018 | TFS 2017 | TFS 2015 | VS 2017 | VS 2015 | VS 2013

Whether your software project is large or small, using version control as soon as possible is a good idea. Azure Repos supports two types of version control: [Git](../../repos/git/gitquickstart.md)
and [Team Foundation Version Control](./overview.md) (TFVC).
 
<a name="tfvc_or_git_summary"></a>
## Which version control system should I use?
 
Git is the default version control provider for new projects. You should use Git for version control in your projects unless you have a specific need for centralized version control features in TFVC.  

You can use TFVC repos with Git in the same Project so it's easy to add TFVC later if you need centralized version control. To setup a new repo type for an existing project [use these instructions](../../repos/git/team-projects.md).

### Git (distributed)

Git is a distributed version control system. Each developer has a copy of the source repository on their dev machine. Developers can commit each set of changes on their dev machine and perform version control operations such as history and compare without a network connection. Branches are lightweight. When you need to switch contexts, you can create a private local branch. You can quickly switch from one branch to another to pivot among different variations of your codebase. Later, you can merge, publish, or dispose of the branch. 

>[!NOTE]
>Git in Visual Studio, Azure DevOps Services, and TFS is standard Git. You can use Visual Studio with third-party Git services, and you can also use third-party Git clients with TFS.
 
To learn more, see [Git and Azure Repos](../../repos/git/index.yml).

### TFVC (centralized)
 
Team Foundation Version Control (TFVC) is a centralized version control system. Typically, team members have only one version of each file on their dev machines. Historical data is maintained only on the server. Branches are path-based and created on the server.

TFVC has two [workflow models](decide-between-using-local-server-workspace.md):

  - **Server workspaces** - Before making changes, team members publicly check out files. Most operations require developers to be connected to the server. This system facilitates locking workflows. Other systems that work this way include Visual Source Safe, Perforce, and CVS. With server workspaces, you can scale up to very large codebases with millions of files per branch and large binary files.

  - **Local workspaces** - Each team member takes a copy of the latest version of the codebase with them and works offline as needed. Developers check in their changes and resolve conflicts as necessary. Another system that works this way is Subversion.

To learn more, see [TFVC overview](./overview.md)
 
<a name="tfvc_or_git_details"></a>

### Moving from TFVC to Git

If you have existing TFVC repos, you can migrate them to Git repos using the [git-tfs tool](https://github.com/git-tfs/git-tfs). The tool allows you to [migrate a TFVC repo to a Git repo](https://github.com/git-tfs/git-tfs/blob/master/doc/usecases/migrate_tfs_to_git.md) 
in just a couple of commands.

## Git and TFVC capabilities

Need more help to make a choice? These charts might help.

<table>
<thead>
<tr>
<td>Capability</td>
<td>TFVC</td>
<td>Git</td>
</tr>
</thead>
<tr>
<td>Changes</td>
<td><p>Team members can concurrently change files on their dev machines. You <a href="check-your-work-team-codebase.md" data-raw-source="[upload (check-in)](check-your-work-team-codebase.md)">upload (check-in)</a> changesets to the server when you create them. You can upload your changes at any time. However, you might be interrupted by <a href="resolve-team-foundation-version-control-conflicts.md" data-raw-source="[conflicts](resolve-team-foundation-version-control-conflicts.md)">conflicts</a>.</p>

<p>You can change the comment of a <a href="find-view-changesets.md" data-raw-source="[changeset](find-view-changesets.md)">changeset</a> after you check it in. You can link changesets to work items and associate them with completed builds.</p>
</td>
<td><p>Team members can concurrently change files on their dev machines. You create commits on your dev machine independently of contributing them to the team. When you&#39;re ready you must pull the latest commits before you upload (push) yours to the server. When you pull, you might be interrupted by conflicts.</p>

<p>You can amend the latest local commit. You cannot change older commits. You can link commits to work items and associate them with completed builds.</p>

<p>You can modify and combine local commits from the command prompt.</p></td>
</tr>
<tr>
<td>Branching</td>
<td>
<p>Path-based branches are used mostly as long-standing constructs to isolate risk of change among feature teams and releases. Team members typically set up an additional workspace for each branch they work on.</p>

<p>Changes in each branch are independent from each other, so you don&#39;t have to check them in before switching from one branch to another. Merging between sibling branches requires a baseless merging.
</p>

<p>You can get visualizations of your branch structures and where your changesets have been merged.</p>

<p>See <a href="use-branches-isolate-risk-team-foundation-version-control.md" data-raw-source="[Use branches to isolate risk in Team Foundation Version Control](use-branches-isolate-risk-team-foundation-version-control.md)">Use branches to isolate risk in Team Foundation Version Control</a>.</p>
</td>
<td><p>Branching is lightweight and path independent. Many developers create a branch for each new feature they are coding, sometimes on a daily basis. You can quickly switch from one branch to another to pivot among different variations of your codebase. You can create branches that exist only on your dev machine and share them if and when you&#39;re ready. </p>

<p>You must commit, branch, stash, or undo changes before switching branches. Merging is simple and independent of the commit that the branch is based on.</p>

<p>You can compare branches to see which commits exist on which branches.</p>

<p>See <a href="/azure/devops/repos/git/branches?view=azure-devops&amp;tabs=visual-studio#use-branches-to-manage-development" data-raw-source="[Use Git branches to switch contexts, suspend work, and isolate risk](/azure/devops/repos/git/branches?view=azure-devops&amp;tabs=visual-studio#use-branches-to-manage-development)">Use Git branches to switch contexts, suspend work, and isolate risk</a>.</p>
</td>
</tr>
<tr>
<td>Conflict resolution</td>
<td>You might have to <a href="resolve-team-foundation-version-control-conflicts.md" data-raw-source="[resolve conflicts](resolve-team-foundation-version-control-conflicts.md)">resolve conflicts</a> when you get, check in, merge, or unshelve. You can resolve all types of conflicts in Visual Studio.</td>
<td>You might have to resolve conflicts when you pull or merge. You can resolve content conflicts in Visual Studio or from the command prompt.</td>
</tr>
<tr>
<td>File storage</td>
<td>You can check in large binary files. You might also want to use <a href="https://go.microsoft.com/fwlink/?LinkId=246165" data-raw-source="[NuGet](https://go.microsoft.com/fwlink/?LinkId=246165)">NuGet</a> in combination or as an alternative.</td>
<td>You can check in small binary files as you would regular files. When working with large binary files, use <a href="https://devblogs.microsoft.com/devops/announcing-git-lfs-on-all-vso-git-repos/" data-raw-source="[Git-LFS](https://devblogs.microsoft.com/devops/announcing-git-lfs-on-all-vso-git-repos/)">Git-LFS</a> to store your large binary files in Azure Repos.</td>
</tr>
<tr>
<td>History</td>
<td>File history is not replicated on the client dev machine and so can be viewed only when you&#39;re connected to the server. You can <a href="get-history-item.md" data-raw-source="[view history](get-history-item.md)">view history</a> in Visual Studio and on the web portal. You can annotate files to see who changed a line, and when they changed it.</td>
<td>File history is replicated on the client dev machine and can be viewed even when not connected to the server. You can view history in Visual Studio and on the web portal. You can annotate files to see who changed a line, and when they changed it.
</td>
</tr>
<tr>
<td>Tag your files</td>
<td>You can <a href="use-labels-take-snapshot-your-files.md" data-raw-source="[apply labels](use-labels-take-snapshot-your-files.md)">apply labels</a> to a version of one or more files from either Visual Studio or the command prompt. Each file can have label applied to a different version.</td> 
<td>You can apply tags from the command prompt to individual commits. View tags in the Visual Studio history window.
</td>
</tr>
<tr>
<td>Roll back changes</td>
<td>You can <a href="roll-back-changesets.md" data-raw-source="[roll back one or more changesets](roll-back-changesets.md)">roll back one or more changesets</a></td>
<td>You can revert a commit.
</td>
</tr>
<tr>
<td>Scale</td>
<td>You can work on small or very large scale projects using <a href="decide-between-using-local-server-workspace.md#local">local workspaces</a>. Supports massive scale (millions of files per branch and large binary files) projects using <a href="decide-between-using-local-server-workspace.md#when-might-i-need-to-use-a-server-workspace" data-raw-source="[server workspaces](decide-between-using-local-server-workspace.md#when-might-i-need-to-use-a-server-workspace)">server workspaces</a>.</td>
<td>You can quickly begin small projects. You can scale up to very large projects, but you have to plan ahead to modularize your codebase. You can create multiple repositories in a project.
</td>
</tr>
</table>


### Server 

<table>
<thead>
<tr>
<td>Capability</td>
<td>TFVC</td>
<td>Git</td>
</tr>
</thead>
<tr>
<td>Server</td>
<td>Azure DevOps Services, TFS</td>
<td>Azure DevOps Services, TFS and Git third-party services</td>
</tr>
<tr>
<td>Alerts</td>
<td>Team members can <a href="check-your-work-team-codebase.md#subscribe-to-alerts" data-raw-source="[receive email alerts when check-ins occur](check-your-work-team-codebase.md#subscribe-to-alerts)">receive email alerts when check-ins occur</a>.
</td>
<td>Team members can receive email alerts when commits are pushed to the server. 
</td>
</tr>
<tr>
<td>Auditability</td>
<td>Because your team checks in all their work into a centralized system, you can identify which user checked in a <a href="find-view-changesets.md" data-raw-source="[changeset](find-view-changesets.md)">changeset</a> and use <a href="compare-files.md" data-raw-source="[compare](compare-files.md)">compare</a> to see what they changed. Looking at a file, you can <a href="view-file-changes-using-annotate.md" data-raw-source="[annotate](view-file-changes-using-annotate.md)">annotate</a> it to identify who changed a block of code, and when they did it.</td>
<td>You can identify which user pushed a commit. (Anyone can claim any identity as the author or committer.) You can identify when changes were made what was changed using history, compare, and annotate.</td>
</tr>
<tr>
<td>Builds (automated by TFBuild)</td>
<td>You can use all <a href="../../pipelines/overview.md" data-raw-source="[TFBuild](../../pipelines/overview.md)">TFBuild</a> capabilities to build any combination of content you want within the project collection.</td>
<td>You can use most TFBuild capabilities to build one project at a time, and one or more repositories at a time.
</td>
</tr>
<tr>
<td>Code reviews</td>
<td>Yes; see <a href="share-your-code-in-tfvc-vs.md" data-raw-source="[Day in the life of an devops Developer: Suspend work, fix a bug, and conduct a code review](share-your-code-in-tfvc-vs.md)">Day in the life of an devops Developer: Suspend work, fix a bug, and conduct a code review</a>. For more lightweight discussions, you can also comment on and send email about a changeset from the web portal.
</td>
<td>Yes; see <a href="../../repos/git/pull-requests.md" data-raw-source="[Conduct a pull request](../../repos/git/pull-requests.md)">Conduct a pull request</a>. For more lightweight discussions, you can also comment on and send email about a commit from the web portal.
</td>
</tr>
<tr><td>Files</td>
<td><p>Each project contains all files under a single root path (for example: <strong>$/FabrikamTFVC</strong>). You can <a href="../../organizations/security/permissions.md" data-raw-source="[apply permissions](../../organizations/security/permissions.md)">apply permissions</a> at the file level. You can <a href="lock-unlock-folders-files.md" data-raw-source="[lock files](lock-unlock-folders-files.md)">lock files</a>.</p>

<p>You can browse your files on the web portal and using <a href="use-source-control-explorer-manage-files-under-version-control.md" data-raw-source="[Source Control Explorer](use-source-control-explorer-manage-files-under-version-control.md)">Source Control Explorer</a> in Visual Studio.</p>

<p>Your project exists on only one server.</p>
</td>
<td>
<p>Each project can contain one or more Git repositories and each Git repository can contain one or more branches. The most granular permissions you can apply are to a repository or a branch. Files cannot be locked.</p>
<p>You can browse your files on the web portal.</p>
<p>You can push commits to multiple remote repositories (for example to both your project repository and to your web site hosted on Windows Azure.</p>
</td>
</tr>
<tr>
<td>Quality gates</td>
<td>You can use CI builds, gated check-in builds and check-in policies.</td>
<td>You can use CI builds and gated check-in builds through <a href="../../repos/git/branch-policies.md" data-raw-source="[branch policies](../../repos/git/branch-policies.md)">branch policies</a>.
</td>
</tr>
</table>



 
### Client

<table>
<thead>
<tr>
<td>Capability</td>
<td>TFVC</td>
<td>Git</td>
</tr>
</thead>
<tr>
<td>Client software</td>
<td> Visual Studio, Eclipse (with <a href="https://msdn.microsoft.com/library/gg413285%28v=vs.140%29.aspx" data-raw-source="[Team Explorer Everywhere](https://msdn.microsoft.com/library/gg413285%28v=vs.140%29.aspx)">Team Explorer Everywhere</a>)</td>
<td>Visual Studio, Eclipse, and other third-party tools</td>
</tr>
<tr>
<td>Files</td>
<td>You can browse your files using <a href="use-source-control-explorer-manage-files-under-version-control.md" data-raw-source="[Source Control Explorer](use-source-control-explorer-manage-files-under-version-control.md)">Source Control Explorer</a> in Visual Studio, or using Windows File Explorer or the <a href="use-team-foundation-version-control-commands.md" data-raw-source="[command prompt](use-team-foundation-version-control-commands.md)">command prompt</a>.</td>
<td>You can browse your files using Windows File Explorer or the command prompt. 
</td>
</tr>
<tr>
<td>Manage work on your dev machine</td>
<td><a href="develop-code-manage-pending-changes.md#use-the-pending-changes-page-to-manage-your-work" data-raw-source="[Pending changes](develop-code-manage-pending-changes.md#use-the-pending-changes-page-to-manage-your-work)">Pending changes</a> and <a href="develop-code-manage-pending-changes.md#use-the-my-work-page-to-manage-your-work" data-raw-source="[my work](develop-code-manage-pending-changes.md#use-the-my-work-page-to-manage-your-work)">my work</a> pages.</td>
<td>Changes, commits, and branches pages.</td>
</tr>
<tr>
<td>Suspend your work</td>
<td>You can <a href="suspend-your-work-manage-your-shelvesets.md" data-raw-source="[suspend from my work page or shelve your changes](suspend-your-work-manage-your-shelvesets.md)">suspend from my work page or shelve your changes</a>.</td>
<td>You can create a branch from (from Visual Studio or the command prompt) or stash (from the command prompt)</td>
</tr>
<tr>
<td>User interface</td>
<td>
<ul>
 <li><strong>Visual Studio:</strong> Offers all commonly used features and many advanced features.</li>
 <li><strong>TFS web portal:</strong> Can browse, comment, annotate, and see history of the codebase.</li>
 <li><strong>TF Command prompt:</strong> Installed with Visual Studio. Used for advanced, administrative, and other less common tasks.</li> 
</ul>
</td>
<td>
<ul>
 <li><strong>Visual Studio:</strong> Offers many commonly used features. Features for some common tasks are not yet available.</li>
 <li><strong>TFS web portal:</strong> Can browse, comment, annotate, and see history of the codebase.</li>
 <li><strong>Third-party command prompt:</strong> You can install it from Visual Studio. Used for some common and many less common tasks.</li>
</ul>
</td>
</tr>
<tr>
<td>Visual Studio compatibility</td>
<td>You can use all supported <a href="https://docs.microsoft.com/azure/devops/server/requirements" data-raw-source="[previous versions of Visual Studio](https://docs.microsoft.com/azure/devops/server/requirements)">previous versions of Visual Studio</a>.</td>
<td><p>Git is built in with Visual Studio 2017, 2015, and 2013.</p>
<p>You can also use Visual Studio 2012 Update 4 (you must also install <a href="https://go.microsoft.com/fwlink/?LinkID=275845" data-raw-source="[Visual Studio Tools for Git](https://go.microsoft.com/fwlink/?LinkID=275845)">Visual Studio Tools for Git</a>).</p></td>
</tr>
<tr>
<td>Web portal</td>
<td>You can browse your codebase (including branches), view history, annotate and comment on changesets and shelvesets, and perform other tasks such as ad hoc downloading of selected parts of your codebase as a .zip file.</td>
<td>You can browse your codebase, view history, compare branches, annotate and comment on commits, and perform other tasks such as ad hoc downloading of selected parts of your codebase as a .zip file.</td>
</tr>
</table>


### Integration and migration

<table>
<thead>
<tr>
<td>Capability</td>
<td>TFVC</td>
<td>Git</td>
</tr>
</thead>

<tr>
<td>Migration path</td>
<td><a href="https://github.com/git-tfs/git-tfs" data-raw-source="[Git-TFS](https://github.com/git-tfs/git-tfs)">Git-TFS</a></td>
<td><a href="https://github.com/git-tfs/git-tfs" data-raw-source="[Git-TFS](https://github.com/git-tfs/git-tfs)">Git-TFS</a></td>
</tr>
</table>
