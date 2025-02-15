---

title: Service proxy has been destroyed exceptions in log
description:
taxonomy:
    category: git-integration-for-jira-data-center

---

<!-- TROUBLESHOOTING -->

### Problem

Errors/failures in the Git Integration for Jira application are seen sporadically.

### Diagnosis

Jira admins will see a message similar to the one below in the Jira log -- `/application-logs/atlassian-jira.log`:

**Error:**

```java
2019-07-07 07:07:072,777 bigbrassband-gitplugin-RevisionIndexerImpl:thread - 0 ERROR      [c.b.j.g.s.indexer.revisions.RevisionIndexerImpl] Unable to index repository 'my-repository-example-name' (repoId: 777)
org.eclipse.gemini.blueprint.service.importer.ServiceProxyDestroyedException: service proxy has been destroyed
    at org.eclipse.gemini.blueprint.service.importer.support.internal.aop.ServiceDynamicInterceptor$ServiceLookUpCallback.doWithRetry(ServiceDynamicInterceptor.java:101)
    at org.eclipse.gemini.blueprint.service.importer.support.internal.support.RetryTemplate.execute(RetryTemplate.java:81)
    at org.eclipse.gemini.blueprint.service.importer.support.internal.aop.ServiceDynamicInterceptor.lookupService(ServiceDynamicInterceptor.java:427)
    at org.eclipse.gemini.blueprint.service.importer.support.internal.aop.ServiceDynamicInterceptor.getTarget(ServiceDynamicInterceptor.java:400)
    at org.eclipse.gemini.blueprint.service.importer.support.internal.aop.ServiceInvoker.invoke(ServiceInvoker.java:60)
    at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:185)
    at org.springframework.aop.support.DelegatingIntroductionInterceptor.doProceed(DelegatingIntroductionInterceptor.java:136)
    at org.springframework.aop.support.DelegatingIntroductionInterceptor.invoke(DelegatingIntroductionInterceptor.java:124)
    at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:185)
    at org.eclipse.gemini.blueprint.service.util.internal.aop.ServiceTCCLInterceptor.invokeUnprivileged(ServiceTCCLInterceptor.java:70)
    at org.eclipse.gemini.blueprint.service.util.internal.aop.ServiceTCCLInterceptor.invoke(ServiceTCCLInterceptor.java:53)
    at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:185)
    at org.eclipse.gemini.blueprint.service.importer.support.LocalBundleContextAdvice.invoke(LocalBundleContextAdvice.java:57)
    at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:185)
    at org.springframework.aop.support.DelegatingIntroductionInterceptor.doProceed(DelegatingIntroductionInterceptor.java:136)
    at org.springframework.aop.support.DelegatingIntroductionInterceptor.invoke(DelegatingIntroductionInterceptor.java:124)
    at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:185)
    at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:212)
    at com.sun.proxy.$Proxy2505.getAllTranslationsForPrefix(Unknown Source)
    at com.bigbrassband.jira.git.utils.I18nManager.getForPrefix(I18nManager.java:54)
    at com.bigbrassband.jira.git.utils.I18nManager.getText(I18nManager.java:62)
    at com.bigbrassband.jira.git.services.indexer.revisions.GitPluginIndexManagerImpl.handleUpdateError(GitPluginIndexManagerImpl.java:303)
    at com.bigbrassband.jira.git.services.indexer.revisions.GitPluginIndexManagerImpl.fetchImpl(GitPluginIndexManagerImpl.java:523)
    at com.bigbrassband.jira.git.services.indexer.revisions.GitPluginIndexManagerImpl.callFetch(GitPluginIndexManagerImpl.java:502)
    at com.bigbrassband.jira.git.services.indexer.revisions.GitPluginIndexManagerImpl.updateIndex(GitPluginIndexManagerImpl.java:339)
    at com.bigbrassband.jira.git.services.indexer.revisions.RevisionIndexerImpl$1.doRun(RevisionIndexerImpl.java:151)
    at com.bigbrassband.jira.git.services.indexer.revisions.QueueEntry.run(QueueEntry.java:82)
    at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
    at java.util.concurrent.FutureTask.run(FutureTask.java:266)
    at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
    at java.lang.Thread.run(Thread.java:748)
```

### Cause

On occasion - the Atlassian Universal Plugin Manager (UPM) will not stop threads from previous versions of the Git Integration for Jira app.

### Solution

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        No configuration or source code data is lost when uninstalling, disabling or cleaning up plugin folders. However - if you wish to export your settings prior to these change - use the <a href='/git-integration-for-jira-data-center/bulk-export-gij-self-managed'>Bulk Change export</a>.
    </div>
    </div>
</div>

**Update the** [**Atlassian Universal Plugin Manager**](https://marketplace.atlassian.com/apps/23915/atlassian-universal-plugin-manager) **("UPM") to the latest version prior to using the following solutions:**

#### Step 1: Re-enable app.

1.  Disable the _Git Integration for Jira_ app in **Manage apps**.

2.  Re-enable _Git Integration for Jira_ app.

3.  _Optional:_ Restart Jira.

4.  Reindex repositories.

5.  If symptoms persist, proceed to next step.

#### Step 2: Reinstall app.

1.  Update the Universal Plugin Manager (UPM) to the [**latest version**](https://marketplace.atlassian.com/apps/23915/atlassian-universal-plugin-manager?tab=versions) offered by Atlassian.

2.  Uninstall the _Git Integration for Jira_ app in **Manage apps**.

3.  Re-install _Git Integration for Jira_ app.

4.  _Optional:_ Restart Jira.

5.  Reindex repositories.

6.  If symptoms persist, proceed to next step.

#### Step 3: Clean up plugin folders.

1.  Stop Jira.

2.  Clean up [**plugin temp folders**](https://answers.atlassian.com/questions/7110972/can-we-clean-up-osgi-plugins-in-jira) fully or remove these files:

    *   `JIRA_INSTALL_FOLDER/temp/*_git_plugin-*.jar`

    *   `JIRA_HOME_FOLDER/plugins/.osgi-plugins/transformed-plugins/*_git_plugin-*.jar`

3.  Remove all versions of the **Git Integration for Jira** app from the `installed-plugins` folder except the [**latest version**](https://marketplace.atlassian.com/apps/4984/git-integration-for-jira?hosting=server&tab=versions):

    *   `JIRA_HOME_FOLDER/plugins/installed-plugins/*_git_plugin-*.jar`

4.  Start Jira.

5.  Reindex repositories.

6.  If symptoms persist, contact BigBrassBand Support.

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        <b>Contact Us</b><br>
        If you still have a question - reach out to our <a href='https://help.gitkraken.com/git-integration-for-jira-data-center/gij-self-hosted-contact-support/'>Support Desk</a> or email us at <a href='mailto:gijsupport@gitkraken.com'>gijsupport@gitkraken.com</a>.
    </div>
    </div>
</div>

&nbsp;

### More articles about troubleshooting, workarounds and solutions

[Why I am getting the error, “git-upload-pack not permitted”?](/git-integration-for-jira-data-center/why-i-am-getting-the-error-git-upload-pack-not-permitted-gij-self-managed/)

[Avoid OutOfMemory exceptions by configuring or memory allocation with Jira to accommodate large repositories](/git-integration-for-jira-data-center/avoid-outofmemory-exceptions-by-configuring-or-memory-allocation-with-jira-to-accommodate-large-repositories-gij-self-managed)

[Cannot auto-deploy some tracked repositories: Specified origin is incorrect or not supported](/git-integration-for-jira-data-center/Cannot-auto-deploy-some-tracked-repositories-gij-self-managed)

[Connection Reset when Accessing the Database](/git-integration-for-jira-data-center/Connection-reset-when-accessing-the-database-gij-self-managed)

["Dangerous use of multiple connections" error on local database](/git-integration-for-jira-data-center/Dangerous-use-of-multiple-connections-error-on-local-database-gij-self-managed)

[Duplicate entry 0 for key PRIMARY exceptions in log](/git-integration-for-jira-data-center/Duplicate-entry-0-for-key-PRIMARY-exceptions-in-log-gij-self-managed)

[Error while reindexing – Java heap space / Object too large, rejecting the pack](/git-integration-for-jira-data-center/Error-while-reindexing-Java-heap-space-Object-too-large,-rejecting-the-pack-gij-self-managed)

[Error creating git branches and also using NFS](/git-integration-for-jira-data-center/error-creating-git-branches-gitlabpropertiesnotinitializedexception-and-using-nfs-gij-self-managed)

[Fix performance issues for nested cloned repositories with enabled Git Service Permissions mode](/git-integration-for-jira-data-center/Fix-performance-issues-for-nested-cloned-repositories-with-enabled-secure-mode-gij-self-managed)

[Fixing reindex issues using Indexing Queue Viewer](/git-integration-for-jira-data-center/fixing-reindex-issues-using-indexing-queue-viewer)

[Gitolite integration: Why the Git integration app not see the master branch?](/git-integration-for-jira-data-center/Gitolite-integration--why-the-Git-integration-app-not-see-the-master-branch-gij-self-managed)

[Health Check: Database Collation](/git-integration-for-jira-data-center/Health-check--database-collation-gij-self-managed)

[Indexing error – Too many open files](/git-integration-for-jira-data-center/Indexing-error-Too-many-open-files-gij-self-managed)

[Installation fails when installing manually](/git-integration-for-jira-data-center/Installation-fails-when-installing-manually-gij-self-managed)

[Jira index error: IndexNotFoundException: no segments* file found](/git-integration-for-jira-data-center/Jira-index-error--IndexNotFoundException--no-segments-file-found)

[Malformed input or input contains unmappable characters](/git-integration-for-jira-data-center/Malformed-input-or-input-contains-unmappable-characters-gij-self-managed)

[Personal access token failing Azure DevOps integration with Not Authorized error](/git-integration-for-jira-data-center/Personal-access-token-failing-azure-devops-integration-with-Not-Authorized-error-gij-self-managed)

[Problems with shared home on Azure Storage](/git-integration-for-jira-data-center/Problems-with-shared-home-on-azure-storage-gij-self-managed)

[Pull request index error: org.json.JSONException](/git-integration-for-jira-data-center/Pull-request-index-error--JSONException-gij-self-managed)

[Repositories missing from Azure DevOps integration](/git-integration-for-jira-data-center/Repositories-missing-from-azure-devops-integration-gij-self-managed)

**"Service proxy has been destroyed" exceptions in log** (this page)

[SQLException 'Incorrect string value' in merge requests](/git-integration-for-jira-data-center/sqlexception-incorrect-string-value-in-merge-requests-gij-self-managed)

[SSH key file format is invalid](/git-integration-for-jira-data-center/ssh-key-file-format-is-invalid-gij-self-managed)

[TFS - Not authorized exception when Jira works thru proxy](/git-integration-for-jira-data-center/tfs-not-authorized-exception-when-jira-works-thru-proxy-gij-self-managed)

[Unexpected exception parsing XML document from URL error in log](/git-integration-for-jira-data-center/Unexpected-exception-parsing-XML-document-from-URL-error-in-log-gij-self-managed)

[Why don't I see the Create Branch or Pull Request features?](/git-integration-for-jira-data-center/why-dont-i-see-the-create-branch-or-pull-request-features-gij-self-managed)

[Your token has not been granted the required scopes](/git-integration-for-jira-data-center/Your-token-has-not-been-granted-the-required-scopes-gij-self-managed)

[When a GIJ license expires, it shows up as a session error to the user](/git-integration-for-jira-data-center/when-a-license-expires-a-session-error-is-shown-to-the-user-gij-self-managed)

[edDSA provider not supported WARN in logs](/git-integration-for-jira-data-center/edDSA-provider-not-supported-WARN-in-logs-gij-self-managed)

