---
id: 'manage-usage-disk-throughput'
title: 'Manage Disk Throughput usage'
---

## What you are charged for

Each database has a dedicated disk, and you are charged for its provisioned disk throughput. However, unless you explicitly opt in for additional throughput, no charges apply.

Refer to our [disk guide](/docs/guides/platform/compute-and-disk#disk) for details on how disk throughput, disk IOPS, disk size, disk type and compute size interact, along with their limitations and constraints.

<Admonition type="note">

Launching a Read Replica creates an additional database with its own dedicated disk. Read Replicas inherit the primary database's disk throughput settings. You are charged for the provisioned throughput of the Read Replica.

</Admonition>

## How charges are calculated

Disk throughput is charged by MB/s-Hrs (MB/s stands for megabytes per second). 1 MB/s-Hr represents disk throughput of 1 MB/s being provisioned for 1 hour. For example, having 10 MB/s provisioned for 5 hours results in 50 MB/s-Hrs (10 MB/s × 5 hours).

### Usage on your invoice

Usage is shown as "Disk Throughput MB/s-Hrs" on your invoice.

## Pricing

Pricing depends on the [disk type](/docs/guides/platform/compute-and-disk#disk-types), with type gp3 being the default.

### General purpose disks (gp3)

$0.00013 per MB/s-Hr ($0.095 per MB/s per month). gp3 disks come with a baseline throughput of 125 MB/s. You are only charged for provisioned throughput exceeding these 125 MB/s.

| Plan       | Included Disk Throughput | Over-Usage per MB/s per month | Over-Usage per MB/s-Hr |
| ---------- | ------------------------ | ----------------------------- | ---------------------- |
| Pro        | 125 MB/s                 | $0.095                        | $0.00013               |
| Team       | 125 MB/s                 | $0.095                        | $0.00013               |
| Enterprise | Custom                   | Custom                        | Custom                 |

### High performance disks (io2)

There are no charges. Throughput scales with IOPS at no additional cost.

## Billing examples

### No additional throughput configured

| Line Item                     | Units     | Costs   |
| ----------------------------- | --------- | ------- |
| Pro Plan                      | 1         | $25     |
|                               |           |         |
| Compute Hours Micro Project 1 | 744 hours | $10     |
| Disk Throughput Project 1     | 125 MB/s  | $0      |
|                               |           |         |
| **Subtotal**                  |           | **$35** |
| Compute Credits               |           | -$10    |
| **Total**                     |           | **$25** |

### Additional throughput configured

| Line Item                     | Units     | Costs       |
| ----------------------------- | --------- | ----------- |
| Pro Plan                      | 1         | $25         |
|                               |           |             |
| Compute Hours Large Project 1 | 744 hours | $110        |
| Disk Throughput Project 1     | 200 MB/s  | $7.13       |
|                               |           |             |
| **Subtotal**                  |           | **$142.13** |
| Compute Credits               |           | -$10        |
| **Total**                     |           | **$132.13** |

### Additional throughput configured with Read Replica

| Line Item                     | Units     | Costs       |
| ----------------------------- | --------- | ----------- |
| Pro Plan                      | 1         | $25         |
|                               |           |             |
| Compute Hours Large Project 1 | 744 hours | $110        |
| Disk Throughput Project 1     | 200 MB/s  | $7.13       |
|                               |           |             |
| Compute Hours Large Replica   | 744 hours | $110        |
| Disk Throughput Replica       | 200 MB/s  | $7.13       |
|                               |           |             |
| **Subtotal**                  |           | **$259.26** |
| Compute Credits               |           | -$10        |
| **Total**                     |           | **$249.26** |