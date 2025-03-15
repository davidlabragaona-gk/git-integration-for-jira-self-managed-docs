---

title: App Support
description:
taxonomy:
    category: git-integration-for-jira-data-center

---

The Git Integration for Jira app (GIJ) currently supports the following Jira versions:

| **GIJ version** | **Supported Jira versions** |
| :--- | :--- |
| 5.1.1+ | Jira Data Center 10.0.0 - 10.4.1 |
| 4.28.6 | Jira Data Center 9.4.30 - 9.17.5 |
| 4.28.5 | Jira Data Center 8.13.27 - 9.17.5 |
| 4.24.2 | Jira Server 8.12.3 - 9.12.18\*<br>Jira Data Center 8.12.3 - 9.12.18 |

\* _Jira server extended license support until Feb 15, 2025._

<div class="bbb-callout bbb--error">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        <b>UPDATE</b><br>
        Starting Git Integration for Jira v4.0+ app, support for Jira 7 is entirely dropped.<br>
        Starting Git Integration for Jira v4.12+ app, we are dropping support for Java 8.0-8.11.
        The last Jira Server release is v9.12+.
    </div>
    </div>
</div>

We are committed to provide you with an efficient and reliable support. Scroll down to see helpful tips to get started.

&nbsp;

### JDK compatibility

Any of the GIJ 4.x.x versions are compatible with JDK 17.
Any of the GIJ 5.x.x versions are ONLY compatible with JDK 17.

&nbsp;

### Jira Server platform end of life support

<div class="bbb-callout bbb--alert">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        Starting from version 9.13, Jira Software now exclusively supports Data Center licenses. If you attempt to upgrade to release 9.13 or any subsequent version with your Server license, Jira will be unable to start and you will be required to revert back to the previous version.<br>
        <div style="margin-top:5px;margin-bottom:-10px;">If you prefer to continue using a Server license, you have the option of upgrading to Jira Software version 9.12 or an earlier release.</div>
    </div>
    </div>
</div>

Atlassian's end of life support for the Jira Server platform has ended. Please plan ahead on migrating your Jira Server to Cloud or Data Center starting now.

This process is simple and manageable:

*   Before you migrate, upgrade Git Integration for Jira app to the latest version.
*   Back your data for migration.
*   Plan your migration path.

See the following topics from Atlassian for migration:

*   [Migrating Jira applications to another server](https://confluence.atlassian.com/adminjiraserver073/migrating-jira-applications-to-another-server-861253107.html)

*   [Migrating from Jira Server to Jira Cloud](https://www.atlassian.com/migration/plan/cloud-guide)

*   [Migrating from Jira Server to Jira Data Center](https://confluence.atlassian.com/enterprise/migrate-from-server-to-data-center-953127136.html)

&nbsp;

### Migrating to Jira 9/10

Administrators should deselect the "Reverse commit tab sort order" option in General settings when Jira 8 is migrated to Jira 9. If this is a new Jira 9/10 installation then nothing is required.

After upgrading from Jira 8 to Jira 9/10, administrators must re-create all indexes using the "Reset index" Action command for all repositories or integrations.

For detailed information, see [Migrating from Jira 8 to Jira 9/10](/git-integration-for-jira-data-center/migrating-jira7-to-jira9-gij-self-managed).

For more information on upgrading to Jira 10+, see [Jira 10 upgrade notes](https://confluence.atlassian.com/display/JIRASOFTWARE/Jira+Software+10.0.x+upgrade+notes).

&nbsp;

### Quick Installation Video

No changes necessary to your Git server. This Jira app acts as a regular Git client.

Using Atlassian's marketplace system, a Jira administrator can install the Git Integration for Jira app without ever leaving the web browser.

<div class='embed-container embed-container--16-9'>
    <iframe width='709' height='443' src='https://fast.wistia.com/embed/iframe/lr0jp6ntfd?videoFoam=true' frameborder='0' allowfullscreen ></iframe>
</div>

<div align='center' style='margin-top:10px'>
    <i>Right click <a href='https://bigbrassband.wistia.com/medias/lr0jp6ntfd'><b>here</b></a> to open this video in a new browser tab for more viewing options.</i><br>
    Watch the complete installation of the Git Integration Plugin for Jira app from scratch (2 minutes).
</div>

&nbsp;

### Viewing Reindex Logs

Go to the Manage Git Repositories page, click the **Actions** ![](/wp-content/uploads/actions-icon.png) icon then **View Log** to view the indexing logs.

![](/wp-content/uploads/gij-manage-git-repo-view-reindex-logs-c.png)

If there is an error encountered when connecting to a repository, a similar indexing error log will be displayed:

![](/wp-content/uploads/gij-manage-git-repo-indexing-logs-dlg.png)

&nbsp;

### Atlassian Support End of Life

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        <b>Important changes to Atlassian Server and Data Center products</b><br>
        Atlassian is making changes to the Server and Data Center products, especially ending sale and support for the Server products -- <a href='https://www.atlassian.com/migration/journey-to-cloud'>Learn what this means for you</a>.
    </div>
    </div>
</div>

Starting **v2.13.0+**, we are dropping support for Java 7, Jira 6.3 and 6.4.

Starting **v3.5.1+**, support for Internet Explorer 11 browser is dropped.

The table below shows the Jira Version, when [Atlassian will stop supporting that Jira version](https://confluence.atlassian.com/support/atlassian-support-end-of-life-policy-201851003.html) and the corresponding version of Internet Explorer.

| **Jira Version** | **Jira End of Life Date** | **Oldest IE Supported** | **Git Integration for Jira supported?** |
| :--- | :--- | :--- | :--- |
| 8.0 | February 11, 2021 | Edge | Yes\* |
| 8.1 | April 4, 2021 | Edge | Yes\* |
| 8.2 | May 21, 2021 | Edge | Yes\* |
| 8.3 | July 22, 2021 | Edge | Yes\* |
| 8.4 | Sep 09, 2021 | Edge | Yes\* |
| 8.5 | October 21, 2021 | Edge | Yes\* |
| 8.6 | December 17, 2021 | Edge | Yes\* |
| 8.7 | February 3, 2022 | Edge | Yes\* |
| 8.8 | March 19, 2022 | Edge | Yes\* |
| 8.9 | May 20, 2022 | Edge | Yes\* |
| 8.10 | June 23, 2022 | Edge | Yes\* |
| 8.11 | July 15, 2022 | Edge | Yes\* |
| 8.12 | August 26, 2022 | Edge | Yes\* |
| 8.13 | October 8, 2022 | Edge | Yes\* |
| 8.14 | November 23, 2022 | Edge | Yes\* |
| 8.15 | February 2, 2023 | Edge | Yes\* |
| 8.16 | March 23, 2023 | Edge | Yes\* |
| 8.17 | May 18, 2023 | Edge | Yes\* |
| 8.18 | July 1, 2023 | Edge | Yes\* |
| 8.19 | August 26, 2023 | Edge | Yes\* |
| 8.20 | October 19, 2023 | Edge | Yes\* |
| 8.21 | December 9, 2023 | Edge | Yes\* |
| 8.22 | February 16, 2024 | Edge | Yes\* |
| 9.0 | June 21, 2024 | Edge | Yes\* |
| 9.1 | July 21, 2024 | Edge | Yes\* |
| 9.2 | August 25, 2024 | Edge | Yes\* |
| 9.3 | September 29, 2024 | Edge | Yes\* |
| 9.4 | November 15, 2024 | Edge | Yes\* |
| 9.5 | December 6, 2024 | Edge | Yes\* |
| 9.6 | January 24, 2025 | Edge | Yes\* |
| 9.7 | March 20, 2025 | Edge | Yes\* |
| 9.8 | April 25, 2025 | Edge | Yes\* |
| 9.9 | June 2, 2025 | Edge | Yes\* |
| 9.10 | Ju1y 11, 2025 | Edge | Yes\* |
| 9.11 | August 30, 2025 | Edge | Yes\* |
| 9.12 (LTS) | November 29, 2025 | Edge | Yes\* |
| 9.13 | January 22, 2026 | Edge | Yes\* |
| 9.14 | February 15, 2026 | Edge | Yes\* |
| 9.15 | March 27, 2026 | Edge | Yes\* |
| 9.16 | May 23, 2026 | Edge | Yes\* |
| 9.17 | June 26, 2026 | Edge | Yes\* |
| 10.0 | August 22, 2026 | Edge | Yes\* |
| 10.1 | October 9, 2026 | Edge | Yes\* |
| 10.2 | November 20, 2026 | Edge | Yes\* |
| 10.3 (LTS) | December 5, 2026 | Edge | Yes\* |
| 10.4 | January 22, 2027 | Edge | Yes\* |

\* _See information below about retiring IE11 support._

* * *

### **Retiring IE11 Support**

With the release of the Edge browser since 2015, IE has not been receiving major updates. Atlassian has stated in their [**blog**](https://blog.developer.atlassian.com/retiring-ie11-support-for-atlassian-cloud-server-and-data-center-products/) that they will withdraw support for IE11 on all Jira products.

In view of this, BigBrassBand LLC will also follow this decision effectively:

*   For all Atlassian Cloud products, support for IE11 will end on **31 March 2020**.

*   For Atlassian server and data center products, the last version to support IE11 were released between **September 2019** and **March 2020**.

&nbsp;

<div class="bbb-callout bbb--info">
    <div class="irow">
    <div class="ilogobox">
        <span class="logoimg"></span>
    </div>
    <div class="imsgbox">
        <b>Contact Us</b><br>
        If you still have a question - reach out to our <a href='https://help.gitkraken.com/git-integration-for-jira-data-center/gij-self-hosted-contact-support/'>Support Desk</a> or email us at <a href='mailto:gijsupport@gitkraken.com'>gijsupport@gitkraken.com</a>.
    </div>
    </div>
</div>


