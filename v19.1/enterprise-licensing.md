---
title: Enterprise Features
summary: Request and set trial and enterprise license keys for CockroachDB
toc: true
---

CockroachDB distributes a single binary that contains both core and [enterprise features](https://www.cockroachlabs.com/pricing/). You can use core features without any license key. However, to use the enterprise features, you need either a trial or an enterprise license key.

This page lists enterprise features, and shows you how to obtain and set trial and enterprise license keys for CockroachDB.

## Enterprise features

Feature | Description
--------+-------------------------
[`BACKUP`](backup.html) / [`RESTORE`](restore.html) | CockroachDB's `BACKUP` [statement](sql-statements.html) allows you to create full or incremental backups of your cluster's schema and data that are consistent as of a given timestamp. The `RESTORE` [statement](sql-statements.html) restores your cluster's schemas and data from [an enterprise `BACKUP`](backup.html) stored on a services such as AWS S3, Google Cloud Storage, NFS, or HTTP storage.
[Change Data Capture](change-data-capture.html) | Change data capture (CDC) provides efficient, distributed, row-level [change feeds into Apache Kafka](create-changefeed.html) for downstream processing such as reporting, caching, or full-text indexing.
[Cluster Visualization](enable-node-map.html) | The **Node Map** visualizes the geographical configuration of a multi-regional cluster by plotting the node localities on a world map.
[Table Partitioning](partitioning.html) | CockroachDB allows you to define table partitions, thus giving you row-level control of how and where your data is stored. Partitioning enables you to reduce latencies and costs and can assist in meeting regulatory requirements for your data.

## Types of licenses

Type | Description
-------------|------------
**Trial License** | A trial license enables you to try out CockroachDB enterprise features for 30 days for free.
**Enterprise License** | A paid enterprise license enables you to use CockroachDB enterprise features for longer periods (one year or more).

## Obtain a trial or enterprise license key

To obtain a trial license key, fill out [the registration form](https://www.cockroachlabs.com/get-cockroachdb/) and receive your trial license key via email within a few minutes.

To upgrade to an enterprise license, <a href="mailto:sales@cockroachlabs.com">contact Sales</a>.

## Set the trial or enterprise license key

As the CockroachDB `root` user, open the [built-in SQL shell](use-the-built-in-sql-client.html) in insecure or secure mode, as per your CockroachDB setup. In the following example, we assume that CockroachDB is running in insecure mode. Then use the `SET CLUSTER SETTING` command to set the name of your organization and the license key:

{% include copy-clipboard.html %}
~~~ shell
$ cockroach sql --insecure
~~~

{% include copy-clipboard.html %}
~~~ sql
>  SET CLUSTER SETTING cluster.organization = 'Acme Company';
~~~

{% include copy-clipboard.html %}
~~~ sql
>  SET CLUSTER SETTING enterprise.license = 'xxxxxxxxxxxx';
~~~

## Verify the license key

To verify the license key, open the [built-in SQL shell](use-the-built-in-sql-client.html) and use the `SHOW CLUSTER SETTING` command to check the organization name and license key:

{% include copy-clipboard.html %}
~~~ sql
>  SHOW CLUSTER SETTING cluster.organization;
~~~
~~~
+----------------------+
| cluster.organization |
+----------------------+
| Acme Company         |
+----------------------+
(1 row)
~~~

{% include copy-clipboard.html %}
~~~ sql
>  SHOW CLUSTER SETTING enterprise.license;
~~~
~~~
+--------------------------------------------------------------------+
|                         enterprise.license                         |
+--------------------------------------------------------------------+
| xxxxxxxxxxxx                                                       |
+--------------------------------------------------------------------+
(1 row)
~~~

The license setting is also logged in the cockroach.log on the node where the command is run:

{% include copy-clipboard.html %}
~~~ sql
$ cat cockroach.log | grep license
~~~
~~~
I171116 18:11:48.279604 1514 sql/event_log.go:102  [client=[::1]:56357,user=root,n1] Event: "set_cluster_setting", target: 0, info: {SettingName:enterprise.license Value:xxxxxxxxxxxx User:root}
~~~

## Renew an expired license

After your license expires, the enterprise features stop working, but your production setup is unaffected. For example, the backup and restore features would not work until the license is renewed, but you would be able to continue using all other features of CockroachDB without interruption.

To renew an expired license, <a href="mailto:sales@cockroachlabs.com">contact Sales</a> and then [set](enterprise-licensing.html#set-the-trial-or-enterprise-license-key) the new license.

## See also

- [`SET CLUSTER SETTING`](set-cluster-setting.html)
- [`SHOW CLUSTER SETTING`](show-cluster-setting.html)
- [Enterprise Trial –– Get Started](get-started-with-enterprise-trial.html)
