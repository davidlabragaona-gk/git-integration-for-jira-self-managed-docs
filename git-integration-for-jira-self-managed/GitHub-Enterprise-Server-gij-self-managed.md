---

title: GitHub Enterprise Server
description:
taxonomy:
    category: git-integration-for-jira-data-center

---

<div class="bbb-callout bbb--tip">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        These instructions apply to self-hosted GitHub Enterprise Server.
    </div>
    </div>
</div>

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        For instructions to instances hosted on GitHub.com (Free, Team, Enterprise (including <a href='https://docs.github.com/en/enterprise-cloud@latest/admin/identity-and-access-management/managing-iam-with-enterprise-managed-users/about-enterprise-managed-users'></b>EMU</b></a> plans), please go to <a href='/git-integration-for-jira-data-center/github-gij-self-managed'>this page</a>.
    </div>
    </div>
</div>

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        Using <b>Jira Cloud</b>? <a href='/git-integration-for-jira-cloud/github-com-gij-cloud'>See the corresponding article</a>.
    </div>
    </div>
</div>

&nbsp;

<img src='/wp-content/uploads/gij-github-ent-server-banner-logo.png' width=510 height=59 style='max-width:100%;margin:25px 0 15px 0' />

&nbsp;

## Integrate GitHub Enterprise Server with Jira Data Center/Server

Quickly learn how to connect GitHub Enterprise Server git repositories via Git Integration for Jira Server.

**What's on this page:**
- [Integrate GitHub Enterprise Server with Jira Data Center/Server](#integrate-github-enterprise-server-with-jira-data-centerserver)
  - [Creating a personal access token](#creating-a-personal-access-token)
  - [Setting up GitHub Enterprise Server permissions](#setting-up-github-enterprise-server-permissions)
    - [Default repository permission\*\*](#default-repository-permission)
    - [Teams and collaborators](#teams-and-collaborators)
  - [Integration platform support](#integration-platform-support)
  - [Using Full feature integration](#using-full-feature-integration)
  - [Single repository (Manual integration)](#single-repository-manual-integration)
  - [Setting up GitHub web links](#setting-up-github-web-links)
  - [Viewing git commits in Jira Server](#viewing-git-commits-in-jira-server)
  - [Require User PAT settings for user access](#require-user-pat-settings-for-user-access)
  - [Working with branches and pull requests](#working-with-branches-and-pull-requests)
    - [Default branch](#default-branch)
    - [Creating branches](#creating-branches)
    - [Creating pull requests](#creating-pull-requests)
  - [How to enable GetRepositories log response from GitHub to the Jira log?](#how-to-enable-getrepositories-log-response-from-github-to-the-jira-log)
  - [More Integration Guides](#more-integration-guides)

&nbsp;
* * *
&nbsp;

<div class='embed-container embed-container--16-10'>
    <iframe width='709' height='443' src='https://fast.wistia.com/embed/iframe/75nvefgz66?videoFoam=true' frameborder='0' allowfullscreen ></iframe>
</div>

<div align='center' style='margin-top:10px'>
    <i>Right click <a href='https://bigbrassband.wistia.com/medias/75nvefgz66'><b>here</b></a> to open this video in a new browser tab for more viewing options.</i>
</div>

&nbsp;

### Creating a personal access token

<div class="bbb-callout bbb--alert">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        If two-factor authentication is enabled for your GitHub Enterprise Server account, you will need to create a PAT to access your git repositories. Enable two-factor authentication in your GitHub Enterprise Server account for increased security.
    </div>
    </div>
</div>

While instructions from GitHub works just fine, [follow this article](/git-integration-for-jira-data-center/creating-personal-access-tokens-gij-self-managed) for some specific instructions to get you started.

<b style='background-color:#E2FCEF; padding:1px 5px; color:#006745; border-radius:3px; margin: 0 5px; font-size: small;'>VERSION 4.27+</b><br>
There will be two new options now available in the GIJ General Settings. Enabling these settings requires an "extended" scope for your PATs.

![](/wp-content/uploads/gij-datacenter-git-pull-merge-req-group-gencfg-sel.png)

To utilize the new GitHub share PR events, we recommend that users must update their personal access token to have the following scopes:
* `read:discussion`
* `read:org`
* `read:user`
* `repo` (all)
* `user:email`

&nbsp;

### Setting up GitHub Enterprise Server permissions

We recommend using a "service user" in GitHub Enterprise _(example:_ `GitIntegrationforJira`_)_ to be used to integrate with Git Integration for Jira app. This dedicated "service user" will allow the GitHub Enterprise Server administrator to set permissions so the app clones only the desired repositories.

Assign GitHub Enterprise Server permissions for team members or collaborators to allow which resources are accessible for service users. This feature is only available in a GitHub Organization.

&nbsp;

#### Default repository permission**

1.  Login to your GitHub Enterprise Server account.

2.  Go to ![profile icon](/wp-content/uploads/gij-profile-icon.png) Profile ➜ **Settings**.

3.  Under _Organization settings_, click **Member Privileges**.

    ![](/wp-content/uploads/gij-github-default-repo-permission-c.png)
    *   Choose the default permission level for organization members.

    *   The default repository permission only applies to organization members and not to outside collaborators. If the default permission is set to _**None**_, organization members will need to be given access to repositories using the Teams or Collaborators methods (see below).

4.  **Save** the changes.


For more information, see **Access Permissions on GitHub »**.

&nbsp;

#### Teams and collaborators

To give a member additional access, they must be added to a team or make them collaborators on individual repositories.

<br>

**Set default repository permission for the current team:**

1.  Open an organization team. (_Your org ➜ Team ➜ scroll down to the bottom then click the desired team._)

2.  Click the **Repositories** tab.

    ![](/wp-content/uploads/gij-github-manage-repo-permission-tab-c.png)

3.  Set **Read**, **Write** or **Admin** repository access as desired.

<br>

**Assign members to a team on your GitHub repository:**

1.  Create a team in your GitHub Organization.

2.  Invite a member to add it into the team.  An email invitation is sent to that GitHub service user.

    ![](/wp-content/uploads/gij-add-members-to-team-c.png)

    The service user is then added to the team if the invitation has been accepted.

3.  Click the service user to manage permissions for this member to:

    *   Set desired **Role** for this member.

    *   Convert this member to outside collaborator.

    *   Give this member access to organization repositories.

    *   Remove this member from the team.

4.  Click **Manage access** to manage repository access for this member.


![](/wp-content/uploads/gij-manage-team-repo-permission.png)

<div class="bbb-callout bbb--note">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        While users have configured PAT for repository access, users in a GitHub Enterprise Server must at least have <b>Read</b> permissions. This allows them to view commits and smart commits, and browse repositories (if enabled) of connected GitHub Enterprise Server repositories inside Jira.
    </div>
    </div>
</div>

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        For repository managers, collaborators and commit authors, set these users to have <b>Write</b> permissions. This will allow them to view commits and smart commits, browse repositories and also enables them to create branches and pull requests to specified GitHub git repositories via developer panel of a Jira issue.
    </div>
    </div>
</div>

<div class="bbb-callout bbb--alert">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        The user PAT for "Require User PAT" setting should have <b>Write</b> permission. Otherwise, the user will not be able to use it for branch or pull request creation/deletion.
    </div>
    </div>
</div>

For more information on organization teams, see [**GitHub: Organizing Members into Teams »**](https://docs.github.com/en/organizations/organizing-members-into-teams).

For more information on inviting collaborators, see [**Inviting Collaborators to a Personal/Organization Repository »**](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-user-account/managing-access-to-your-personal-repositories/inviting-collaborators-to-a-personal-repository).

&nbsp;

### Integration platform support

GitHub supports the four most recent version releases. We follow this direction and the Git Integration for Jira app (GIJ) will also support these versions.

For previous versions, GIJ supports the following GHE versions:
*   GitHubEE 3.11 (Deprecation 2024-12-05)
*   GitHubEE 3.10 (Deprecation 2024-08-29)
*   GitHubEE 3.9 (Deprecation 2024-06-29)
*   GitHubEE 3.8 (Deprecation 2024-03-07)

GHE 3.8 supports authenticating with username and password. Therefore, GIJ will also do.

&nbsp;

### Using Full feature integration

This process requires an existing GitHub Enterprise account.

We recommend using the Add new integration panel to connect multiple repositories from your GitHub Enterprise Server account.

This setup uses full feature integration offering functions and features not found on single repository connections.

1.  On your Jira Server dashboard menu, go to Git ➜ **Manage repositories**. The git configuration page for connecting repositories is displayed.

2.  On the Add new integration panel, click **GitHub Enterprise**. The Add new integration Wizard is displayed.

    ![](/wp-content/uploads/gij-gitserver-42-connect-auto-ext-service-github-ent-svr-c.png)

    -  For the **Host URL**, enter the address of the GitHub Enterprise server.

    -  Enter the **Personal Access Token** in the provided box as required.

        _**Note:**_ For repository managers, collaborators or users that have enabled 2FA, enter username and the PAT as the password.

    -  Configuring the **Advanced** settings is optional. However, admins/power users may set how the project listing is displayed.

        ![](/wp-content/uploads/gij-gitserver-general-advanced-autoconnect-opt-c.png)

        -   **Custom API Path**  –  his is a relative path that starts with "/".  The maximum allowed length is 2000 characters or less. The integration will use the relative REST API path to retrieve the list of tracked repositories. The Custom API Path is called everytime the list of repositories is loaded, on a regular scheduled reindex and a manual reindex.

            For more examples, see article [Jira Server: Working with Custom API Path - GitHub Enterprise](/git-integration-for-jira-data-center/working-with-custom-api-path-gij-self-managed#githubcom-and-github-enterprise-examples).

        -   **JMESPath filter**  –  JMESPath is a query language for JSON used to filter API results and to limit which repositories are integrated. The maximum allowed length is 2000 characters or less.

            For help with writing expressions, please contact [support](mailto:gijsupport@gitkraken.com). Read about JMESPath expressions on their [website](http://jmespath.org).

            For some other examples, see [Working with JMESPath Filter in GitHub Enterprise](/git-integration-for-jira-data-center/gitHub-gitHub-enterprise-jmespath-filter-examples-gij-self-managed).

        -   **Fetch refspec**  –  Git refspecs contains patterns mapped as references from the remote to the local repository.
            For more information, see **Git Internals -- The Refspec**.

            -  The first two refspec options are required.
            -  The rest of the options are OPTIONAL:

                -  **Clone and index ref notes (refs/notes)** – This is a reference to `refs/notes/*` used for fetching. This option is enabled by default. This affects git notes which are not shown:

                    -  ...when `refs/notes` are disabled on connecting a repository.
                    -   ...when a new note comes when `refs/notes` is disabled.

                -  **Clone and index changes (refs/changes)** – This is a reference to `refs/changes/*` used for fetching.  This option is turned off by default.

                -  **Clone and index other refs** – This is a user-defined list of references used for fetching.  It is a comma-separated list with the format:

                    -   `+refs/refname1/*:refs/refname1/*`, `refs/refname2/*:refs/refname2/*`, ...

    While Custom API Path and JMESPath filter are mutually exclusive, you can use one, the other, both or neither.

3.  Click **Connect**.

4.  On the following screen, the Git Integration for Jira app will read all available repositories from your GitHub Enterprise Server account. Click **Import repositories**.

    *   Repositories that are added or removed from GitHub Enterprise Server will be likewise connected or disconnected from Jira Server.

    *   If your git url contains multiple repositories, it will be added as tracked repositories in the git configuration list. Otherwise, a git repository is added instead.

5.  After the import process, the **Settings** dialog is displayed:

    ![](/wp-content/uploads/gij-gitserver-github-autoconnect-settings-dlg-c.png)

    *   On the Integration Settings, setting the _**Require User PAT**_ option to `ON`, will require users to provide PAT specific for branch and merge requests _(via the developer panel on the Jira issue page)_. For more information on this feature, see [Integration Settings: Require User PAT](/git-integration-for-jira-data-center/require-personal-access-tokens-for-user-actions-create-branch-pull-request-gij-self-managed).

    *   Set **Smart commits** and **Repository Browser** to enable/disable these features.

    *   Set **Project Permissions** according to your organization's project association rules. For detailed information, see [Associating project permissions](/git-integration-for-jira-data-center/associating-project-permissions-gij-self-managed).

6.  Click **Finish** to complete this setup.


GitHub Enterprise Server repositories are now connected to Jira Server.

&nbsp;

### Single repository (Manual integration)

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        This section is for users who are using SSH connections or those who wanted to only connect a single specific repository.
    </div>
    </div>
</div>

This process requires an existing GitHub Enterprise Server git repository. Look for the git clone URL on the repository project page.

Choose between SSH or HTTPS. Use this information to connect the GitLab git repository to your Jira server via Git Integration for Jira app.

![](/wp-content/uploads/gij-github-repository-home.png)

1.  On your Jira dashboard menu, go to Git ➜ **Manage repositories**.

2.  Click **Connect to Git Repository** (_or click the Git icon on the Add new integration panel_) to open the Connect Wizard.

3.  Paste the URL from GitHub Enterprise Server web portal in the provided box.

4.  Continue to the next step by following the screen instructions.

5.  Click **Finish** to complete this process. 


The repository is now connected to Jira Server.

&nbsp;

### Setting up GitHub web links

The Git Integration for Jira app automatically configures web linking for GitHub Enterprise Server git repositories.

For single repository connections, web link setup is optional. However, git links will become available in Git Commits tab when configured.

For more information on this feature, see [Documentation: Web linking](/git-integration-for-jira-data-center/web-linking-gij-self-managed).

&nbsp;

### Viewing git commits in Jira Server

1.  Perform a git commit by adding the Jira issue key in the commit message. This will associate the commit to the mentioned Jira issue.

2.  Open the Jira issue.

3.  Scroll down to the _**Activity**_ panel then click the **Git Commits** tab.

4.  Click **View full commit** to view the code diff.


For more information about this feature, see [Documentation: Viewing commit code diffs](/git-integration-for-jira-data-center/viewing-commit-code-diffs-gij-self-managed).

&nbsp;

### Require User PAT settings for user access

For teams looking to maintain user attribution, Jira administrators can place a requirement where individual Jira users must provide personal access tokens to perform certain actions. This includes actions such as creating a branch or pull request in Jira using their git service account - rather than the integration account.

For more information, see [Require personal access tokens for user access](/git-integration-for-jira-data-center/require-personal-access-tokens-for-user-actions-create-branch-pull-request-gij-self-managed).

If the **Require User PAT option** is enabled in the **Integration Feature Settings** and a user PAT isn't configured yet for the selected repository via Repository Browser, a text label about setting up your PAT is displayed on the create branch and create pull/merge request dialogs.

Click this text label to open the Setup PAT dialog and paste your personal access token in the provided box. Click **Update**.

<img src='/wp-content/uploads/gij-gitserver-setup-pat-dlg.png' style='margin:25px auto;display:block;max-width:100%'/>

<div class="bbb-callout bbb--tip">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        Updating this dialog with a blank entry will remove the configured PAT for the current integration.
    </div>
    </div>
</div>

The Setup PAT dialog is also accessible via Repository Browser (dashboard menu Git ➜ **Repository browser**) ➜ Click the <img src='/wp-content/uploads/gij-edit-icon-dark.png' style='margin: 0 3px;' /> icon under _**Pers. Access**_ column.

&nbsp;

### Working with branches and pull requests

This process requires a GitHub Enterprise Server git repository and a PAT with `repo` scopes.

For GitHub Organization, the user must have the **Write** permissions and the `repo` PAT scopes.

&nbsp;

#### Default branch

Most git integrations allow changing of the default branch of the repository/project other than "master". This change is reflected in the **Repository Settings** of the Git Integration for Jira app on the next reindex. Auto-connected integrations support this feature where Git Integration for Jira app gets the default branch from almost all integrations and apply this setting at repository level.

<div class="bbb-callout bbb--alert">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        Main branch for repositories within an integration can only be changed on the git server.
    </div>
    </div>
</div>

&nbsp;

#### Creating branches

On your Jira Server, open a Jira issue. On the Jira developer panel under **Git Integration**, click **Create branch**. The following dialog is displayed.

<img src='/wp-content/uploads/gij-gitserver-create-branch-dlg.png' style='margin:25px auto;display:block;max-width:100%' /> 

**Pointers:**

1.  Select a **Repository** from the list.

    *  If there are several repositories with the same name, the listed GitHub repositories will have their names attached with a GitHub organization name. For example, `BigBrassBand/second-webhook-test-repo`.

    *  Use the search box to look for the specific repository that will be used.

2.  Choose a **Base branch**.

3.  Enter a **Branch name** or leave it as is (recommended).

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        The Git Integration for Jira Server app gets the default branch from almost all integrations. However, the exception is with Gerrit which always has 'master' as its default branch.
    </div>
    </div>
</div>

The newly-created branch is now listed in the developer panel under **Branches**. Perform a commit to the newly-created branch to be ready for merge.

&nbsp;

#### Creating pull requests

The pull request feature works the same as merge request. On your Jira Server, open the Jira issue where your previously created a branch. On the developer panel under **Git Integration**, click **Create pull request**. The following dialog is displayed.

<img src='/wp-content/uploads/gij-gitserver-create-pull-req-dlg.png' style='margin:25px auto;display:block;max-width:100%' />

**Pointers:**

1.  Select a **Repository** from the list.

    *  If there are several repositories with the same name, the listed GitHub repositories will have their names attached with a GitHub organization name. For example, `BigBrassBand/second-webhook-test-repo`.

    *  Use the search box to look for the specific repository that will be used.

2.  Choose the newly-created branch as the **Source branch**.

3.  Set _**master**_ as the **Target branch**.

4.  Enter a descriptive **Title** or leave it as is _(recommended)_.

<div class="bbb-callout bbb--tip">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        <b>Preview</b> allows you to see the comparison view of the current changes in the selected <b>Source branch</b> vs <b>Target branch</b> (<i>usually master</i>).
    </div>
    </div>
</div>

The pull request is listed on the developer panel of the Jira issue page.

The pull request is also ready for approval by the reviewers in your GitHub web portal.

&nbsp;

### How to enable GetRepositories log response from GitHub to the Jira log?

1.  Open ![](/wp-content/uploads/actions-icon.png) Jira System Administration then click **Logging and profiling** on the left sidebar.

2.  Under the Default loggers section, click **Configure….**

3.  Set the Package name to `com.bigbrassband.jira.git.services.integration`.

4.  Set Logging Level to **DEBUG**.

5.  Click **Add** to proceed.

<b style='background-color:#FFF1B6; padding:1px 5px; color:#172A4C; border-radius:3px; margin: 0 5px; font-size: small;'>IMPORTANT!</b> Remember to turn this setting off after you have obtained the log file for analysis.

&nbsp;

### More Integration Guides

[GitHub.com](/git-integration-for-jira-data-center/gitHub-gij-self-managed) (Git Integration for Jira Data Center/Server)

**GitHub Enterprise Server** (this page)

[GitHub App integration](/git-integration-for-jira-data-center/github-app-integration-gij-self-managed) (Git Integration for Jira Data Center/Server)

[GitLab.com](/git-integration-for-jira-data-center/gitLab-gij-self-managed) (Git Integration for Jira Data Center/Server)

[GitLab CE/EE](/git-integration-for-jira-data-center/gitLab-com-CE-EE-gijsm-gij-self-managed) (Git Integration for Jira Data Center/Server)

[Azure DevOps | Visual Studio Team Services (VSTS)](/git-integration-for-jira-data-center/azure-DevOps-Visual-Studio-Team-Services-(VSTS)-gij-self-managed) (Git Integration for Data Center/Jira Server)

[Azure DevOps Server | Team Foundation Services (TFS)](/git-integration-for-jira-data-center/azure-DevOps-Server-Team-Foundation-Services-(TFS)-gij-self-managed) (Git Integration for Jira Data Center/Server)

[AWS CodeCommit](/git-integration-for-jira-data-center/aws-codecommit-gij-self-managed) (Git Integration for Jira Data Center/Server)

[Gerrit](/git-integration-for-jira-data-center/gerrit-gij-self-managed) (Git Integration for Jira Data Center/Server)

[Bitbucket Server](/git-integration-for-jira-data-center/Bitbucket-Server-gij-self-managed) (Git Integration for Jira Data Center/Server)

[Bonobo](/git-integration-for-jira-data-center/bonobo-gij-self-managed) (Git Integration for Jira Data Center/Server)

[Windows Network | Server Share](/git-integration-for-jira-data-center/windows-Network-Server-Share-gij-self-managed) (Git Integration for Jira Data Center/Server)

[Tracked Folders](/git-integration-for-jira-data-center/tracked-Folders-gij-self-managed) (Git Integration for Jira Data Center/Server)

[**Back to:** Integration basics](/git-integration-for-jira-data-center/Integration-Basics-gij-self-managed) (Git Integration for Jira Data Center/Server)

