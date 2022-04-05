---
editable: false
---

# Pricing for {{ mch-short-name }}

{% include [currency-choice](../_includes/pricing/currency-choice.md) %}

{% include [pricing-status.md](../_includes/mdb/pricing-status.md) %}

{% include [pricing-status-warning.md](../_includes/mdb/pricing-status-warning.md) %}

## What goes into the cost of using {{ mch-short-name }} {#rules}

The cost of {{ mch-name }} usage is based on:

* Storage type and size (disk space).

* Computing resources allocated to cluster hosts (including {{ ZK }} hosts).

* Settings and number of backups.

* Outgoing traffic from {{ yandex-cloud }} to the internet.


{% include [pricing-gb-size](../_includes/pricing-gb-size.md) %}


### DB host usage {#rules-hosts-uptime}

The cost is calculated for each hour of operation of the host in accordance with the allocated computing resources. Supported resource configurations are listed in the [{#T}](concepts/instance-types.md) section, prices for using vCPU and RAM — in the [Prices](#prices) section.

You can choose the host class for {{ CH }} and {{ ZK }} hosts (as appropriate for the expected replication load).

{% note warning %}

In clusters with disabled [{{ CK }}](./concepts/replication.md#ck) support and with two or more {{ CH }} hosts, 3 {{ ZK }} hosts with the minimal class are automatically created to provide replication and fault tolerance.

{% endnote %}

The minimum billing unit is a minute (for example, 1.5 minutes of host usage cost the same as 2 minutes). You aren't charged for time when the DBMS or {{ ZK }} host isn't performing its main functions.


### Disk space usage {#rules-storage}

The following is charged:

* Storage allocated for DB clusters.

    * Storage on local SSDs (`local-ssd`) can only be ordered for clusters running Intel Broadwell and Intel Cascade Lake with three or more hosts, in increments of 100 GB.
    * Storage on non-replicated SSDs (`network-ssd-nonreplicated`) can only be ordered for clusters with three or more hosts in increments of 93 GB.

* The storage size used by data backups of [local](concepts/storage.md#local-storage-features) and [network](concepts/storage.md) storage:

    * Backups are stored free of charge as long as the combined size of the database and all backups is less than the storage volume selected.

    * If the combined size of the database and all backups exceeds the storage volume of the cluster, you only pay for the excess of this volume.

   * During an automatic backup, {{ mch-short-name }} doesn't create a new copy, but saves changes to the database compared to the previous copy. This means that storage used by automatic backups increases only in proportion to the volume of changes that are made.

   * The number of hosts in the cluster does not affect the size of the storage or free backups.

    For example, if there are N free GB of space in the cluster, the first N GB of backups are stored free of charge.

* The storage size used by cold data backups of [hybrid storage](concepts/storage.md#hybrid-storage-features):

   * Cold data backups are stored in the same {{ objstorage-name }} bucket as the data itself.

   * The storage used by backups is taken into account when calculating the cost of using {{ objstorage-name }} as well as the volume of the data itself.

   * During an automatic backup, {{ mch-short-name }} doesn't create a new copy, but saves changes to the database compared to the previous copy. This means that storage used by automatic backups increases only in proportion to the volume of changes that are made.

The cost is specified for one month of use. The minimum billing unit is 1 GB per minute (for example, storing 1 GB for 1.5 minutes costs the same as storing 1 GB for 2 minutes).



## Pricing {#prices}



All prices are shown without VAT.

### {{ CH }} host computing resources {#prices-clickhouse}




{% include [usd-host-ch.md](../_pricing/managed-clickhouse/usd-host-ch.md) %}


### {{ ZK }} host computing resources {#prices-zookeeper}

{% note info %}

You can't order {{ ZK }} host resources using a CVoS.

{% endnote %}




{% include [usd-host-zoo.md](../_pricing/managed-clickhouse/usd-host-zoo.md) %}


### Storage and backups {#prices-storage}




{% include [usd-storage.md](../_pricing/managed-clickhouse/usd-storage.md) %}


### Outgoing traffic {#prices-traffic}




{% include notitle [usd-egress-traffic.md](../_pricing/usd-egress-traffic.md) %}

