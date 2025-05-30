---
id: 'manage-usage-read-replicas'
title: 'Manage Read Replica usage'
---

## What you are charged for

Each [Read Replica](/docs/guides/platform/read-replicas) is a dedicated database. You are charged for its resources: [Compute](/docs/guides/platform/compute-and-disk#compute), [Disk Size](/docs/guides/platform/database-size#disk-size), provisioned [Disk IOPS](/docs/guides/platform/compute-and-disk#provisioned-disk-throughput-and-iops), provisioned [Disk Throughput](/docs/guides/platform/compute-and-disk#provisioned-disk-throughput-and-iops), and [IPv4](/docs/guides/platform/ipv4-address).

## How charges are calculated

Read Replica charges are the total of the charges listed below.

**Compute**
Compute is charged by the hour, meaning you are charged for the exact number of hours that a Read Replica is running and, therefore, incurring Compute usage. If a Read Replica runs for part of an hour, you are still charged for the full hour.

Read Replicas run on the same Compute size as the primary database.

**Disk Size**
Refer to [Manage Disk Size usage](/docs/guides/platform/manage-your-usage/disk-size) for details on how charges are calculated. The disk size of a Read Replica is 1.25x the size of the primary disk to account for WAL archives. With a Read Replica you go beyond your subscription plan's quota for Disk Size.

**Provisioned Disk IOPS (optional)**
Read Replicas inherit any additional provisioned Disk IOPS from the primary database. Refer to [Manage Disk IOPS usage](/docs/guides/platform/manage-your-usage/disk-iops) for details on how charges are calculated.

**Provisioned Disk Throughput (optional)**
Read Replicas inherit any additional provisioned Disk Throughput from the primary database. Refer to [Manage Disk Throughput usage](/docs/guides/platform/manage-your-usage/disk-throughput) for details on how charges are calculated.

**IPv4 (optional)**
If the primary database has a configured IPv4 address, its Read Replicas are also assigned one, with charges for each. Refer to [Manage IPv4 usage](/docs/guides/platform/manage-your-usage/ipv4) for details on how charges are calculated.

### Usage on your invoice

Compute incurred by Read Replicas is shown as "Replica Compute Hours" on your invoice. Disk Size, Disk IOPS, Disk Throughput and IPv4 are not shown separately for Read Replicas and are rolled up into the project.

## Billing examples

### No additional resources configured

The project has one Read Replica and no IPv4 and no additional Disk IOPS and Disk Throughput configured.

| Line Item                     | Units     | Costs      |
| ----------------------------- | --------- | ---------- |
| Pro Plan                      | 1         | $25        |
|                               |           |            |
| Compute Hours Small Project 1 | 744 hours | $15        |
| Disk Size Project 1           | 8 GB      | $0         |
|                               |           |            |
| Compute Hours Small Replica   | 744 hours | $15        |
| Disk Size Replica             | 10 GB     | $1.25      |
|                               |           |            |
| **Subtotal**                  |           | **$56.25** |
| Compute Credits               |           | -$10       |
| **Total**                     |           | **$46.25** |

### Additional resources configured

The project has two Read Replicas and IPv4 and additional Disk IOPS and Disk Throughput configured.

| Line Item                     | Units     | Costs       |
| ----------------------------- | --------- | ----------- |
| Pro Plan                      | 1         | $25         |
|                               |           |             |
| Compute Hours Large Project 1 | 744 hours | $110        |
| Disk Size Project 1           | 8 GB      | $0          |
| Disk IOPS Project 1           | 3600      | $14.40      |
| Disk Throughput Project 1     | 200 MB/s  | $7.13       |
| IPv4 Hours Project 1          | 744 hours | $4          |
|                               |           |             |
| Compute Hours Large Replica 1 | 744 hours | $110        |
| Disk Size Replica 1           | 10 GB     | $1.25       |
| Disk IOPS Replica 1           | 3600      | $14.40      |
| Disk Throughput Replica 1     | 200 MB/s  | $7.13       |
| IPv4 Hours Replica 1          | 744 hours | $4          |
|                               |           |             |
| Compute Hours Large Replica 2 | 744 hours | $110        |
| Disk Size Replica 2           | 10 GB     | $1.25       |
| Disk IOPS Replica 2           | 3600      | $14.40      |
| Disk Throughput Replica 2     | 200 MB/s  | $7.13       |
| IPv4 Hours Replica 2          | 744 hours | $4          |
|                               |           |             |
| **Subtotal**                  |           | **$434.09** |
| Compute Credits               |           | -$10        |
| **Total**                     |           | **$424.09** |

## FAQ

### Do Compute Credits apply to Read Replica Compute?

No, Compute Credits do not apply to Read Replica Compute.