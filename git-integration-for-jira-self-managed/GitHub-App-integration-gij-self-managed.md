---

title: GitHub App integration
description:
taxonomy:
    category: git-integration-for-jira-data-center

---

GitHub offers a variety of integration options, including: API, OAuth, and more recently GitHub Apps. There are a number of benefits to using GitHub app over OAuth:

*   GitHub apps are by nature an organization installation. A separate GitHub account or service user is not required.

*   Because GitHub apps require GitHub administrator authorization, we can rely on the GitHub app having administrator permissions.

*   Determine repository access at the organization or repository level for the integration

*   GitHub apps have a higher rate limit than OAuth.

For more details, see the [GitHub Apps article](https://docs.github.com/en/developers/apps/getting-started-with-apps/differences-between-github-apps-and-oauth-apps).

&nbsp;

### New integration options

Two new integration options are added into the Add new integration wizard Connect screen:

1.  GitHub App (GitHub.com and GitHub Enterprise Cloud)

2.  GitHub Enterprise App (GitHub Enterprise Server)

There are two terms:

*   **GitHub Application (GHA)** – GHA itself is a set of authorization information. It is created in some GitHub organization during the first step of connecting a GHA integration with the Git Integration for Jira app.  

*   **Installation of a GitHub Application** –  To get access to repositories inside the organization, an admin has to install the GHA in the organization. During the installation of GHA, the administrator selects the scope that will be available for this installation of this GHA. It is the second step of connecting a GHA integration.

&nbsp;

### Permissions

<div class="bbb-callout bbb--alert">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        You must be an organization owner or have admin permissions in a repository to install/uninstall a GitHub App on an organization. If a GitHub App is installed in a repository and requires organization permissions, the organization owner must approve the application.
    </div>
    </div>
</div>

Check GitHub Apps permission for your organization:

1.  On your GitHub web portal, go to your organization ➜ **Settings** tab.

2.  On the sidebar, click Developer settings ➜ **GitHub Apps**.

![](/wp-content/uploads/gij-github-app-org-setting-GHA-c.png)

&nbsp;

### Pre-requisites

<b style='background-color:#FFF1B6; padding:1px 5px; color:#172A4C; border-radius:3px; margin: 0 3px; font-size: small;padding:2px 7px'>IMPORTANT!</b>

*   As an initial configuration requirement, admins need to install the GHA in an organization. After this setup, only then that Jira instance can read the repositories with Git Integration for Jira app.

*   Establishing a connection using GHA is a two-way process. This requires the Jira instance, where the GHA integration is connected, be accessible remotely from the GitHub server. Make the IP of the Jira instance accessible from the internet as well as add this IP address to the GitHub.com allow list.

&nbsp;

### Limitations

*   Only one GHA installation is allowed on each GitHub organization. This is because the GHA itself is created each time on the first step of connecting a GHA integration and prevents the reuse of an existing GHA for installing in another organization.

*   The **Cancel** function on the scope selection page does not do anything and GIJ have no control and cannot affect its behavior. When a user installs a GHA created manually, clicking **Cancel** redirects back to the GHA page.

*   We advise users against renaming their GHAs. GIJ uses this name for identifying the GHA. However, the GitHub server does not return information about the application rename event. Thus, GIJ has no way to receive any information about the new name. As the result, the `your GitHub app` link on the **Remove integration** page will return a 404 page error if a GHA is renamed.

&nbsp;

### Integrate to a GitHub App

1.  On your Jira dashboard menu, go to Git ➜ **Manage repositories**.

    ![](/wp-content/uploads/gij-dashboard-git-menu-repo-manager-c.png)

2.  On the Add new integration panel, click **GitHub**.

3.  With GIJ version 4.6+ and later, the GitHub App integration feature is added to the External service list.

    ![](/wp-content/uploads/gij-github-integration-external-host-selection-c.png)

4.  Pick the integration that conforms to your configuration:

    *   GitHub.com and GitHub Enterprise Cloud

    *   GitHub Enterprise Server

5.  Enter **Organization name**.

    ![](/wp-content/uploads/gij-github-app-integration-ready-connect-c.png)

    For GHA on GitHub Enterprise Server external service, enter **Host URL** and **Organization name**.

6.  Click **Connect** to continue.

    ![](/wp-content/uploads/gij-github-app-integration-settings-userpat-c.png)

7.  On the Settings screen, the _**Require user PAT**_ setting is enabled and cannot be changed because it is directly affected by the _**Enforce Git service permissions**_ setting in the **General settings** page. For the GHA feature, the user’s PAT is not mandatory since it can interact with the Git server using the GHA access token.

8.  Click **Connect** to start configuring this GitHub App integration.

    The Git Integration for Jira app will perform this task automatically. Provide login credentials if prompted.

9.  On the following screen, enter a **descriptive name** for the new GitHub App. _(Changing this name later on will have a negative impact on the GHA integration)_

    ![](/wp-content/uploads/gij-github-app-create-GHA-github-name-c.png)

10. Click **Create GitHub App…** to proceed.

    ![](/wp-content/uploads/gij-github-app-repository-selector-screen-c.png)

11. Choose:

    *   **All repositories** – to connect all repositories from this organization.

    *   **Only select repositories** – lets you select a specific repository for this setup.

12. Click **Install** to complete this process.

The GitHub App integration is now displayed in the Git repositories configuration list.

&nbsp;

### Post-install notes

The GHA is created automatically by Git Integration for Jira app. For any related questions, please contact [gijsupport@gitkraken.com](mailto:gijsupport@gitkraken.com.)

*   You can reconfigure connected repositories in the Edit integration connection settings page for this GHA integration ( ![](/wp-content/uploads/actions-icon.png)_Actions_).

    ![](/wp-content/uploads/gij-github-app-edit-integration-connection-cfg-c.png)

*   Make sure that the following properties must not be changed for this GHA integration:
    *   **GitHub App name**
    *   Post installation
    *   Webhook attributes
    *   Private keys
    *   Any settings on the Permissions and Events page
    *   Any settings on the installation page

*   Admins can restrict repositories using the JMESpath filter to avoid a case when a user tries to connect thousands of heavy repositories resulting in decreased Jira performance.

*   A GHA installation can be suspended in two ways:
    *   **_From the owner side_** -- Press **Suspend** on the Integration Connection settings for the selected integration via GIJ actions. <b style='background-color:#FFF1B6; padding:1px 5px; color:#172A4C; border-radius:3px; margin: 0 3px; font-size: small;padding:2px 7px'>RECOMMENDED</b>
    *   **_From the user side_** -- Press **Suspend** on the GitHub portal for the GHA installation. <b style='background-color:#DEE0E5; padding:1px 5px; color:#44516C; border-radius:3px; margin: 0 3px; font-size: small;padding:2px 7px'>NOT RECOMMENDED</b>

*   It is possible to re-issue a PEM key for a GHA on the GitHub server side. However, the only way to update the PEM key of a connected GHA integration is via [Bulk Import](/git-integration-for-jira-data-center/import-existing-repositories-via-bulk-change-gij-self-managed/). Bulk export the GHA integration and then paste the entire PEM key enclosed in double quotes into the .tsv file (to preserve line esc chars).

*   A GHA must be deleted by its owner. If several users have access to Repository Management, only one of them can actually remove the app from the Git server after the GHA integration is removed.

&nbsp;

### Using alternative URL for GitHub Apps

<b style='background-color:#EAE5FE; padding:1px 5px; color:#412C92; border-radius:3px; margin: 0 5px; font-size: small;'>NEW FEATURE</b>
<b style='background-color:#E2FCEF; padding:1px 5px; color:#006745; border-radius:3px; margin: 0 5px; font-size: small;'>VERSION 4.27+</b>

The alternative URL will allow GitHub Apps to be configured to make them sending webhooks directly to that URL instead of Jira. In this case, an alternative URL points to a proxy server which stays between GitHub and Jira. This will allow webhook events to be redirected to the alternative URL when Jira is inaccessible from internet, behind a firewall or is running locally.

Setup a new GHA integration by using an alternative URL instead of the original Jira base URL.For now, it can only be called via REST API:

**url**
`http://${originalJiraBaseUrl}/rest/gitplugin/1.0/global-settings`

**method**
POST

**content-type**
application/json

**parameter(s)**
`{"altJiraBaseUrl": "${alternativeJiraUrlAsString}"}`

For example, let's assume you want to run a Jira standalone instance locally and try or test a GitHub App integration type. In this case, set up the following:

1.  The Jira itself which may be accessible from your local instance. For example:<br>
`http://localhost:2990`.

2.  The ngrok utility as a proxy on the same machine to forward all incoming requests from the Internet to the local Jira. For instance, it has `https://my.ngrok.com` as a publicly available URL, which redirects all requests on to `http://localhost:2990`.

3.  With Git Integration for Jira app, set up an alternative URL by doing the following call:

    ```bash
    curl -X POST http://localhost:2990/jira/rest/gitplugin/1.0/global-settings \\
    --user admin \\
    -H "Content-Type: application/json" \\
    -d '{"altJiraBaseUrl": "https://my.ngrok.com/jira"}'
    ```

In order to clean up the `altJiraBaseUrl` property, just set up it to empty string `{"altJiraBaseUrl": ""}`.

&nbsp;

### Troubleshooting GHA integrations

#### GitHub App integration stuck installation state

A GHA integration may get stuck in <b style='background-color:#0C42A3; padding:1px 5px; color:#DEEAFE; border-radius:3px; margin: 0 3px; font-size: small;padding:2px 7px'>INSTALLING</b> status. At the moment, we found three cases when it may happen:

| Case | What happened | What the user can do to remove the integration |
| :--- | :--- | :--- |
| **1** | The integration is waiting for response from a GitHub server | Wait till the GitHub server responds |
| **2** | The GHA was not installed during connecting of the integration | Install the GHA and then remove the integration as usual |
| **3** | The GHA was removed from the GitHub server | Nothing |

If GitHub App integration is stuck on **Installing** status, use the **Remove integration** action to remove such integration.

![](/wp-content/uploads/gij-gitserver-github-app-install-prog-remove-action.png)

However, removing GHA integrations this way (in cases #1 and #2) will leave an unconnected/lost GHA on the GitHub server. As all data for connecting are stored in the integration, there is no way to connect an existing GHA to a new integration. On the other hand, the admin of the GitHub server can remove such lost GHA manually.

For case #3, while this case is very rare, the integration will remain in the Manage Git integration list. The Jira admin can remove the integration using the **Remove integration** action.

#### No displayed Pull Requests for GHA Enterprise integration on the Jira issue page

When creating a new connection to GitHub-app, Git Integration for Jira pp requests additional information about the Issues with at least a `Read-only` access level.

This issue refers on after adding or updating pull requests for a GitHub App Enterprise integration, the pull request information is not displayed in the Git integration panel on the Jira issue page.

This behavior affects GitHub Enterprise Edition (EE) versions ranging from (v2.22) to (v3.12). The GitHub.com version does not exhibit this issue. To address this, just assign read and write permissions for pull requests. For PAT scopes, include `Pull requests:read` as minimum requirement and add Pull requests:write to be able to create PRs from Jira Git integration panel.

<div class="bbb-callout bbb--alert">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        To those who have upgraded to GHE v3.13+, this issue is not present anymore; so skip the steps below.
    </div>
    </div>
</div>

For those who are experiencing problems with already existing applications and are still using older versions of GHE, follow these steps:

1.  On your GHE portal dashboard, go to **User profile** ➜ **Your organizations**.

2.  On the organizations list, select an org to manage by clicking on **Settings**.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-select-org-settings.png)

3.  On the sidebar under Third-party Access, click on **GitHub Apps**.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-sidebar-gha.png)

4.  Under Installed GitHub Apps, click **Configure** for the selected GHA.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-configure-gha.png)

5.  Click **App settings** for this GitHub App.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-app-cfg.png)

6.  On the App settings page, click the **Permissions &amp; Events** tab on the sidebar.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-app-permissions.png)

7.  On the Permissions page, click on **Repository permissions**.

8.  On the following page, scroll down to **Issues** then click on the **Access** dropdown.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-permissions-issues-dropdown.png)

9.  On the access level dropdown list, click **Read-only**.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-permissions-issues-dd-readonly.png)

10. Click **Save changes** to apply the setting.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-permissions-issues-save.png)

11. If there's an incoming authorization request, refresh the Installed GitHub Apps page, then click **Review request** for the GitHub App that has pending permission request.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-permissions-review-request.png)

12. On the GHA requesting page, click **Accept new permissions**.

    ![](/wp-content/uploads/gij-datacenter-gha-enterprise-permissions-accept.png)

This should move the installation progress on the Manage integrations page of the Git Integration for Jira app.

&nbsp;

### More Integration Guides

[GitHub.com](/git-integration-for-jira-data-center/github-gij-self-managed) (Git Integration for Jira Data Center/Server)

[GitHub Enterprise Server](/git-integration-for-jira-data-center/gitHub-Enterprise-Server-gij-self-managed) (Git Integration for Jira Data Center/Server)

**GitHub App integration** (this page)

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

---

### More Git Integration for Jira app features

See the [Features section](/git-integration-for-jira-data-center/features-gij-self-managed) to learn more about Git Integration for Jira app features.

