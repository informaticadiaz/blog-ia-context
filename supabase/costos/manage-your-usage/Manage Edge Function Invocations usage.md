---
id: 'manage-usage-edge-function-invocations'
title: 'Manage Edge Function Invocations usage'
---

## What you are charged for

You are charged for the number of times your functions get invoked, regardless of the response status code.

## How charges are calculated

Edge Function Invocations are billed using Package pricing, with each package representing 1 million invocations. If your usage falls between two packages, you are billed for the next whole package.

### Example

For simplicity, let's assume a package size of 1 million and a charge of $2 per package without a free quota.

| Invocations | Packages Billed | Costs |
| ----------- | --------------- | ----- |
| 999,999     | 1               | $2    |
| 1,000,000   | 1               | $2    |
| 1,000,001   | 2               | $4    |
| 1,500,000   | 2               | $4    |

### Usage on your invoice

Usage is shown as "Function Invocations" on your invoice.

## Pricing

<$Partial path="billing/pricing/pricing_edge_functions.mdx" />

## Billing examples

### Within quota

The organization's function invocations are within the quota, so no charges apply.

| Line Item            | Units                 | Costs   |
| -------------------- | --------------------- | ------- |
| Pro Plan             | 1                     | $25     |
| Compute Hours Micro  | 744 hours             | $10     |
| Function Invocations | 1,800,000 invocations | $0      |
| **Subtotal**         |                       | **$35** |
| Compute Credits      |                       | -$10    |
| **Total**            |                       | **$25** |

### Exceeding quota

The organization's function invocations exceed the quota by 1.4 million, incurring charges for this additional usage.

| Line Item            | Units                 | Costs   |
| -------------------- | --------------------- | ------- |
| Pro Plan             | 1                     | $25     |
| Compute Hours Micro  | 744 hours             | $10     |
| Function Invocations | 3,400,000 invocations | $4      |
| **Subtotal**         |                       | **$39** |
| Compute Credits      |                       | -$10    |
| **Total**            |                       | **$29** |

## View usage

You can view Edge Function Invocations usage on the [organization's usage page](https://supabase.com/dashboard/org/_/usage). The page shows the usage of all projects by default. To view the usage for a specific project, select it from the dropdown. You can also select a different time period.

<Image
  alt="Usage page navigation bar"
  src={{
    light: '/docs/img/guides/platform/usage-navbar--light.png',
    dark: '/docs/img/guides/platform/usage-navbar--dark.png',
  }}
  zoomable
/>

In the Edge Function Invocations section, you can see how many invocations your projects have had during the selected time period.

<Image
  alt="Usage page Edge Function Invocations section"
  src={{
    light: '/docs/img/guides/platform/usage-function-invocations--light.png',
    dark: '/docs/img/guides/platform/usage-function-invocations--dark.png',
  }}
  zoomable
/>