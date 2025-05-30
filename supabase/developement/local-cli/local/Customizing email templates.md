---
id: 'customizing-email-templates'
title: 'Customizing email templates'
description: 'Customizing local email templates using config.toml.'
subtitle: 'Customizing local email templates using config.toml.'
---

You can customize the email templates for local development [using the `config.toml` settings](/docs/guides/cli/config#auth-config).

## Configuring templates

You should provide a relative URL to the `content_path` parameter, pointing to an HTML file which contains the template. For example

<$CodeTabs>

```toml name=supabase/config.toml
[auth.email.template.invite]
subject = "You are invited to Acme Inc"
content_path = "./supabase/templates/invite.html"
```

```html name=supabase/templates/invite.html
<html>
  <body>
    <h2>Confirm your signup</h2>
    <p><a href="{{ .ConfirmationURL }}">Confirm your email</a></p>
  </body>
</html>
```

</$CodeTabs>

## Available email templates

There are several Auth email templates which can be configured:

- `auth.email.template.invite`
- `auth.email.template.confirmation`
- `auth.email.template.recovery`
- `auth.email.template.magic_link`
- `auth.email.template.email_change`

## Template variables

The templating system provides the following variables for use:

### `ConfirmationURL`

Contains the confirmation URL. For example, a signup confirmation URL would look like:

```
https://project-ref.supabase.co/auth/v1/verify?token={{ .TokenHash }}&type=email&redirect_to=https://example.com/path
```

**Usage**

```html
<p>Click here to confirm: {{ .ConfirmationURL }}</p>
```

### `Token`

Contains a 6-digit One-Time-Password (OTP) that can be used instead of the `ConfirmationURL`.

**Usage**

```html
<p>Here is your one time password: {{ .Token }}</p>
```

### `TokenHash`

Contains a hashed version of the `Token`. This is useful for constructing your own email link in the email template.

**Usage**

```html
<p>Follow this link to confirm your user:</p>
<p>
  <a href="{{ .SiteURL }}/auth/confirm?token_hash={{ .TokenHash }}&type=email"
    >Confirm your email</a
  >
</p>
```

### `SiteURL`

Contains your application's Site URL. This can be configured in your project's [authentication settings](/dashboard/project/_/auth/url-configuration).

**Usage**

```html
<p>Visit <a href="{{ .SiteURL }}">here</a> to log in.</p>
```

### `Email`

Contains the user's email address.

**Usage**

```html
<p>A recovery request was sent to {{ .Email }}.</p>
```

### `NewEmail`

Contains the new user's email address. This is only available in the `email_change` email template.

**Usage**

```html
<p>You are requesting to update your email address to {{ .NewEmail }}.</p>
```

## Deploying email templates

These settings are for local development. To apply the changes locally, stop and restart the Supabase containers:

```sh
supabase stop && supabase start
```

For hosted projects managed by Supabase, copy the templates into the [Email Templates](/dashboard/project/_/auth/templates) section of the Dashboard.