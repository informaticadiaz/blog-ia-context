---
id: 'manage-usage-realtime-messages'
title: 'Manage Realtime Messages usage'
---

## What you are charged for

You are charged for the number of messages going through Supabase Realtime throughout the billing cycle. Includes database changes, Broadcast and Presence.

**Database changes**
Each database change counts as one message per client that listens to the event. For example, if a database change occurs and 5 clients listen to that database event, it counts as 5 messages.

**Broadcast**
Each broadcast message counts as one message sent plus one message per subscribed client that receives it. For example, if you broadcast a message and 4 clients listen to it, it counts as 5 messages—1 sent and 4 received.

## How charges are calculated

Realtime Messages are billed using Package pricing, with each package representing 1 million messages. If your usage falls between two packages, you are billed for the next whole package.

### Example

For simplicity, let's assume a package size of 1,000,000 and a charge of $2.50 per package without quota.

| Messages  | Packages Billed | Costs |
| --------- | --------------- | ----- |
| 999,999   | 1               | $2.50 |
| 1,000,000 | 1               | $2.50 |
| 1,000,001 | 2               | $5.00 |
| 1,500,000 | 2               | $5.00 |

### Usage on your invoice

Usage is shown as "Realtime Messages" on your invoice.

## Pricing

<$Partial path="billing/pricing/pricing_realtime_messages.mdx" />

## Billing examples

### Within quota

The organization's Realtime messages are within the quota, so no charges apply.

| Line Item           | Units                | Costs   |
| ------------------- | -------------------- | ------- |
| Pro Plan            | 1                    | $25     |
| Compute Hours Micro | 744 hours            | $10     |
| Realtime Messages   | 1.8 million messages | $0      |
| **Subtotal**        |                      | **$35** |
| Compute Credits     |                      | -$10    |
| **Total**           |                      | **$25** |

### Exceeding quota

The organization's Realtime messages exceed the quota by 3.5 million, incurring charges for this additional usage.

| Line Item           | Units                | Costs   |
| ------------------- | -------------------- | ------- |
| Pro Plan            | 1                    | $25     |
| Compute Hours Micro | 744 hours            | $10     |
| Realtime Messages   | 8.5 million messages | $10     |
| **Subtotal**        |                      | **$45** |
| Compute Credits     |                      | -$10    |
| **Total**           |                      | **$35** |

## View usage

You can view Realtime Messages usage on the [organization's usage page](https://supabase.com/dashboard/org/_/usage). The page shows the usage of all projects by default. To view the usage for a specific project, select it from the dropdown. You can also select a different time period.

<Image
  alt="Usage page navigation bar"
  src={{
    light: '/docs/img/guides/platform/usage-navbar--light.png',
    dark: '/docs/img/guides/platform/usage-navbar--dark.png',
  }}
  zoomable
/>

In the Realtime Messages section, you can see the usage for the selected time period.

<Image
  alt="Usage page Realtime Messages section"
  src={{
    light: '/docs/img/guides/platform/usage-realtime-messages--light.png',
    dark: '/docs/img/guides/platform/usage-realtime-messages--dark.png',
  }}
  zoomable
/>