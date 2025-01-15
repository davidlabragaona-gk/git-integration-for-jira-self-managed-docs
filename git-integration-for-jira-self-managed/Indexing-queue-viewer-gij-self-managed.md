---

title: Indexing queue viewer
description:
taxonomy:
    category: git-integration-for-jira-data-center

---

<!-- FEATURES -->

<b style='background-color:#E2FCEF; padding:1px 5px; color:#006745; border-radius:3px; margin: 0 5px; font-size: small;'>NEW FEATURE</b>

![](/wp-content/uploads/gij-gitserver-gitmgr-indexing-queue-viewer-new.png)

&nbsp;

### Introduction

Indexing is a very large part of Git Integration for Jira app. This indexing feature displays various task entries, allowing you to easily view upcoming and ongoing tasks such as repository indexing and garbage collection.

![](/wp-content/uploads/gij-gitserver-indexing-queue-viewer-show-indexer-data.png)

The Indexing queue viewer displays detailed information such as:

*   when was the indexing started
*   when was the indexing finished
*   how much time it took the indexing to complete
*   ID of the task
*   on which node the indexing was processed <b style='background-color:#EAE5FE; padding:1px 5px; color:#412C92; border-radius:3px; margin: 0 5px; font-size: small;'>DATA CENTER</b>

&nbsp;

### Highlights

Offering ease of use and scope of features, the Indexing queue viewer:

*   provides users greater visibility into what's happening with your repositories and system resources.

*   shows detailed information about the tasks - which node it was processed on, start time, finish time, processing time, task id, and more (mentioned above).

*   allows users to see which tasks are in the queue, find specific tasks by history, and filter tasks by specific parameters.

&nbsp;

### Access location

This feature can be accessed via the Jira dashboard menu Git ➜ **Indexing queue**.

![](/wp-content/uploads/gij-gitserver-indexing-queue-mgr-loc-01.png)

&nbsp;

### Indexing queue dashboard

![](/wp-content/uploads/gij-gitserver-indexing-queue-viewer-dashboard.png)

The dashboard displays the current number of processing tasks and tasks in the queue.

Click **Clear queue** to free up the current queue of all tasks with <b style='background-color:#DEE0E5; padding:1px 5px; color:#44516C; border-radius:3px; margin: 0 5px; font-size: small;'>QUEUED</b> status.

Take into consideration that this action...

*   only removes tasks in **QUEUED** status.
*   does not cancel tasks in **INDEXING** status.
*   does not clear the CANCELED status. A task with CANCELED status will stay like that indefinitely until subsequent reindex.

![](/wp-content/uploads/gij-gitserver-indexing-queue-viewer-gencfg-dashboard-c.png)

To the right of the dashboard is the Settings view panel. which shows information related to the general settings for scheduled indexing, garbage collection, etc.

Click **Edit** to go directly to the General settings page.

&nbsp;

### Filters and search

Just below the dashboard are controls for view filters. This section allow users to control which information is displayed on the screen.

![](/wp-content/uploads/gij-gitserver-dc-indexing-queue-group-of-data-filters.png)

These includes:

*   filter by _**status**_
*   filter by _**trigger**_
*   filter by _**type of operation**_
*   filter by _**node**_
*   filter by _**repository ID**_
*   filter by _**task ID**_
*   filter by _**parent task ID**_
*   filter by _**name**_ – case-sensitive:
    *   For ‘_**repository: Name**_’ -- this is a name comprising a group and a repository name.
    *   For '_**integration: Name**_' -- this is the name of the connected integration.

&nbsp;

#### Filter: Status

![](/wp-content/uploads/gij-gitserver-indexing-queue-viewer-status-all.png)

Filter the task list by clicking on the **Status** dropdown and selecting a category:

*   **All** – Displays the data for every Status category. **This is the default selection for the Status filter.**

*   **Queued** -- Displays tasks having <b style='background-color:#DEE0E5; padding:1px 5px; color:#44516C; border-radius:3px; margin: 0 5px; font-size: small;'>QUEUED</b> status. This indicates that the indexing tasks are still waiting in line to be processed or are still unfinished.

*   **Indexing** -- Displays tasks having <b style='background-color:#DEEAFE; padding:1px 5px; color:#0C42A3; border-radius:3px; margin: 0 5px; font-size: small;'>INDEXING</b> status. This indicates that the indexing task is already running.

*   **Indexed** -- Displays tasks having <b style='background-color:#E2FCEF; padding:1px 5px; color:#006745; border-radius:3px; margin: 0 5px; font-size: small;'>INDEXED</b> status. This indicates that the indexing task has finished.

*   **Error** -- Displays tasks having <b style='background-color:#FFEBE6; padding:1px 5px; color:#C02909; border-radius:3px; margin: 0 5px; font-size: small;'>ERROR</b> status. This indicates that the indexing task has encountered an error. Go to **...** Actions ➜ **View log** to see the error(s).

*   <b style='background-color:#E2FCEF; padding:1px 5px; color:#006745; border-radius:3px; margin: 0 5px; font-size: small;'>VERSION 4.23</b> **Canceled** -- Displays tasks having <b style='background-color:#FFF1B6; padding:1px 5px; color:#172A4C; border-radius:3px; margin: 0 5px; font-size: small;'>CANCELED</b> status. This indicates that the indexing task has been cancelled...
    *   manually -- triggered by a user action (admins)
    *   forcefully -- triggered because of an error
    *   automatically -- triggered because the repository/integration disabled

    For detailed information on canceling reindex, see [Cancel indexing: Revision indexing](/git-integration-for-jira-data-center/Cancel-indexing-revision-indexing-gij-self-managed).

&nbsp;

#### Filter: Trigger

![](/wp-content/uploads/gij-gitserver-indexing-queue-viewer-trigger-all.png)

Filters the task list by clicking on the **Trigger** dropdown and selecting a category:

*   **All** – Displays the data for every Trigger category.

*   **Manual** -- Displays tasks that was triggered manually. This includes user-triggered events such as:

    *   reindex repositories/integrations/reindex all

    *   reset all/reset repository

    *   reindex triggered by bulk import

    *   reindex triggered by Reindex REST API

    *   reindex triggered by an update of repository

*   **Webhook** -- Displays tasks triggered by webhook. Indexing triggered by webhooks fall on this category. For related information, see [Webhook indexing explainer](/git-integration-for-jira-cloud/webhook-indexing-explainer-gij-cloud).

*   **Scheduled** -- Displays tasks triggered by scheduled jobs. For more information, see [Scheduler jobs](/git-integration-for-jira-data-center/scheduled-jobs-gij-self-managed).

*   App activity -- Displays reindex tasks triggered by:

    *   a branch creation/deletion

    *   a manipulation with pull request

    *   a change of commit issue association

    *   a repository update, e.g. by a change of main branch

*   **Initial indexing** -- Displays tasks triggered by initial indexing. Initial indexing is performed by the Git Integration for Jira app on the first successful connection of the git service integration.

&nbsp;

#### Filter: Type of operation

![](/wp-content/uploads/gij-gitserver-indexing-queue-viewer-reindex-type-ops.png)

Filters the view by clicking on the **Type of operation** dropdown and selecting a category:

*   **All** –- Displays the data for every Type of operation category.

*   **Reindex** –- Displays tasks related to indexing.

*   **Garbage Collection** -– Displays tasks related to Garbage Collection.

*   **Remove repository** –- Displays tasks related to removal of a repository.

&nbsp;

#### Filter: Node

<b style='background-color:#EAE5FE; padding:1px 5px; color:#412C92; border-radius:3px; margin: 0 5px; font-size: small;'>DATA CENTER</b>

![](/wp-content/uploads/gij-gitdc-indexing-queue-filter-nodes.png)

Filters the view by clicking on the **Node** dropdown and selecting a category:

*   **All** –- Displays the data for every Node in the cluster.

*   **Node\[1…\] - Node\[n\]** –- Displays tasks and data only for the specified node in the cluster.

&nbsp;

#### Using search to filter specific items to view

To the right of the view filter options, users can use the search bar to query for specific tasks and the indexing list view will be updated accordingly. Note that filtering by name is case-sensitive.

<div class="bbb-callout bbb--tip">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        Search text criteria can be combined by repository ID, task ID, parent task ID and name – in one field.
    </div>
    </div>
</div>

&nbsp;

### Sorting

Sorting allows users to arrange tasks by categories such as status, trigger, and type of operation.

The default sort order applies the following rule:

1.  INDEXING – **first**

2.  QUEUED tasks (*see details below*):

    a.  raised to the top manually

    b.  reindex triggered manually:

        *   ![](/wp-content/uploads/actions-icon.png) Actions ➜ Reindex repositories/integrations or Reindex all

        *   ![](/wp-content/uploads/actions-icon.png) Actions ➜ Reset all/Reset repository

        *   via Bulk Import

        *   via Reindex REST API

        *   via an update from changes in the repository

    c.  triggered by webhooks

    d.  triggered by scheduled job

    e.  ![](/wp-content/uploads/actions-icon.png) Actions ➜ Remove repository/integration

    f.  Garbage Collection tasks

3.  FINISHED – **last**

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        <b>Summary of the sorting order</b><br>
        <ol style='margin-bottom:0px !important'>
            <li>The first few rows are tasks being currently processed and sorted by <b>Start time</b> in <u>ascending</u> order.</li>
            <li>Then, the queued tasks which are sorted in the order – they will be processed from the queue.</li>
            <li>And the last rows – are completed tasks sorted by <b>Finish time</b> in <u>descending</u> order.</li>
        </ol>
    </div>
    </div>
</div>

&nbsp;

### Cancel indexing

<b style='background-color:#E2FCEF; padding:1px 5px; color:#006745; border-radius:3px; margin: 0 5px; font-size: small;'>VERSION 4.23+</b>

This feature allows Jira administrators to interrupt the indexing process once it has been queued or has already started. It will suspend the indexing process and can be resumed with subsequent reindex later on.

As of GIJ v4.27.1+, the pull/merge request reindex can be manually cancelled via Indexing queue viewer.

For any selected queue task that is still processing or in progress, click on **...** (Actions) ➜ **Cancel**.

![](/wp-content/uploads/gij-gitserverdc-indexing-queue-cancel-reindex-action.png)



For a more detailed information about this feature, see [Cancel indexing](/git-integration-for-jira-data-center/Cancel-indexing-revision-indexing-gij-self-managed).

<div class="bbb-callout bbb--alert">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        The Git Integration for Jira app <b>Cancel indexing</b> feature does not work with Jira self-managed instances earlier than version 8.12.
    </div>
    </div>
</div>

&nbsp;

### Viewing logs

![](/wp-content/uploads/gij-gitserver-indexing-queue-viewer-actions-menu.png)

The 'indexing status' is displayed in the indexing log dialog that appears during manual reindex. The View log information from the **Indexing Queue Viewer** is similar to the logs that can be viewed in the Manage integration screen.

![](/wp-content/uploads/gij-gitserver-reindex-log-error.png)

For encountered errors when indexing, open the logs via Actions ➜ View log. Copy the message log and submit this to us thru [gijsupport@gitkraken.com](mailto:gijsupport@gitkraken.com) or via [Support portal](/git-integration-for-jira-data-center/gij-self-hosted-contact-support/) for analysis. For the above example error, there are several factors that caused this error – the Git service is down, no internet connection, the webhook has changed or the personal access token has expired.

<div class="bbb-callout bbb--alert">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        The Git Integration for Jira app <b>View log</b> feature does not work with Jira self-managed instances earlier than version 8.12.
    </div>
    </div>
</div>

&nbsp;

### Moving list items to top

Move the selected queue item to the top of the list (most recent). To do this click **...** (Action) ➜ **Move to top**. This will make it easy to monitor the selected item's behavior such as indexing status and viewing its indexing process logs.

&nbsp;

### Indexing queue list

On the next indexing run, the finished tasks for some repository are removed from the queue. This is regardless of the reindex trigger whether scheduled, webhook or manual. The max age for old finished tasks is 1 hour (see below).

The indexing queue does not remove the task from the queue when any of the following conditions is true:

*   this task is the last one of this type for this integration/repository

*   this task is not older than 1 hour from now

For removed integrations/repositories, the pending queued tasks related to removal are deleted from the indexing queue list. Note that the Cancel action is not supported on delete operations.

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        <b style='background-color:#EAE5FE; padding:1px 5px; color:#412C92; border-radius:3px; margin: 0 5px 5px 0; font-size: small;'>DATA CENTER</b><br>
        The indexing queue can spread the indexing work across several nodes. Thus, the most volume of the indexing tasks will be performed on a multi-node Jira. We recommend using a 4-node configuration.
    </div>
    </div>
</div>

&nbsp;

### View indexing details

![](/wp-content/uploads/gij-gitserver-indexing-queue-viewer-show-indexer-data.png)

On the left of the first column, click the **\>** symbol to expand the detailed view of the index task in the queue.

#### Finish time

In this column, the amount of time from when the task has finished indexing is shown.

#### Integration name

This column displays the name of the integrations where indexing tasks has been performed.

#### Repository name

This column displays the name of the repositories where indexing tasks has been performed. Also displayed is the organization (GitHub) or group (GitLab) name before the repository name indicating it’s under that org or group.

#### Type of operation

The type of operation states what kind of indexing was triggered:

*   Reindex
*   Webhook
*   Scheduled
*   Manual
*   Garbage collection
*   Remove

#### Delay

This column shows _**No delay**_ for indexed items that were processed immediately after the previous one. Also displayed are the amount of time when the indexing has finished for the tasks.

#### Trigger

This column shows what kind of operation triggered the reindex for this task.

#### Status

This column shows the indexing status of the task in the list.

#### Refresh function

At the bottom-left portion of the indexing queue viewer, click the ![](/wp-content/uploads/gij-refresh-icon.png) **Refresh** icon to refresh the queue list view.

#### Pagination

At the bottom-right portion of the indexing queue viewer, use the page controls to navigate across the task page list.

&nbsp;

### Data center node indexing

The Indexing queue viewer page correctly displays the number of current indexing tasks according to the specified number of threads, such as:

*   Current number of indexing threads which defines the number of indexing threads on current node
*   Current number of processing tasks which defines the number of all processing tasks on all nodes
*   Number of tasks with  status which corresponds to the number of threads; multiplied by the number of nodes involved in indexing.

Tasks with <b style='background-color:#DEEAFE; padding:1px 5px; color:#0C42A3; border-radius:3px; margin: 0 3px 0px 3px; font-size: small;'>INDEXING</b> status can also be marked for cancelling.

The <b style='background-color:#DEE0E5; padding:1px 5px; color:#44516C; border-radius:3px; margin: 0 3px 0px 3px; font-size: small;'>QUEUED</b> tasks can also be removed from the indexing queue.

The GC tasks can be completed if the indexing queue is empty.

&nbsp;

### See more Git Integration for Jira app features

[Manager permissions](/git-integration-for-jira-data-center/manager-permissions-gij-self-managed) (Git Integration for Jira Data Center)

[Cancel indexing](/git-integration-for-jira-data-center/cancel-indexing-revision-indexing-gij-self-managed/) (Git Integration for Jira Data Center)

[Pull request filters](/git-integration-for-jira-data-center/pull-request-filters-gij-self-managed/) (Git Integration for Jira Data Center)

[Tag filters](/git-integration-for-jira-data-center/tag-filters-gij-self-managed/) (Git Integration for Jira Data Center)

**Indexing queue viewer** (this page)

[Deep linking feature](/git-integration-for-jira-data-center/deeplinking-feature-gij-self-managed/) (Git Integration for Jira Data Center)

[GitHub App integration](/git-integration-for-jira-data-center/github-app-integration-gij-self-managed/) (Git Integration for Jira Data Center)

[Git Integration + ScriptRunner](/git-integration-for-jira-data-center/gij-plus-scriptrunner-gij-self-managed/) (Git Integration for Jira Data Center)

[Git Integration + Jira Automation](/git-integration-for-jira-data-center/git-integration-plus-jira-automation-gij-self-managed/) (Git Integration for Jira Data Center)

[Enforced git permissions for Jira users – Features](/git-integration-for-jira-data-center/enforced-git-permissions-for-jira-users-gij-self-managed/) (Git Integration for Jira Data Center)

[Shared reindex queue between DC nodes](/git-integration-for-jira-data-center/shared-reindex-queue-between-dc-nodes-gij-self-managed/) (Git Integration for Jira Data Center)

[Smart commits overview](/git-integration-for-jira-data-center/smart-commits-overview-gij-self-managed/) (Git Integration for Jira Data Center)

[Associate Pull/Merge Requests to Issues Based on Commits](/git-integration-for-jira-data-center/associate-pull-merge-requests-to-issues-based-on-commits-gij-self-managed/) (Git Integration for Jira Data Center)

[Creating branches](/git-integration-for-jira-data-center/creating-branches-gij-self-managed/) (Git Integration for Jira Data Center)

[Creating pull/merge requests](/git-integration-for-jira-data-center/creating-pull-merge-requests-gij-self-managed/) (Git Integration for Jira Data Center)

[Issue Git integration panel – Features](/git-integration-for-jira-data-center/issue-git-integration-panel-gij-self-managed/) (Git Integration for Jira Data Center)

