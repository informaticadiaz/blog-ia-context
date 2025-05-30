---
id: 'managing-config'
title: 'Managing config and secrets'
description: 'Managing local configuration using config.toml.'
---

The Supabase CLI uses a `config.toml` file to manage local configuration. This file is located in the `supabase` directory of your project.

## Config reference

The `config.toml` file is automatically created when you run `supabase init`.

There are a wide variety of options available, which can be found in the [CLI Config Reference](/docs/guides/cli/config).

For example, to enable the "Apple" OAuth provider for local development, you can append the following information to `config.toml`:

```toml
[auth.external.apple]
enabled = false
client_id = ""
secret = ""
redirect_uri = "" # Overrides the default auth redirectUrl.
```

## Using secrets inside config.toml

You can reference environment variables within the `config.toml` file using the `env()` function. This will detect any values stored in an `.env` file at the root of your project directory. This is particularly useful for storing sensitive information like API keys, and any other values that you don't want to check into version control.

```
.
├── .env
├── .env.example
└── supabase
    └── config.toml
```

<Admonition type="danger">

Do NOT commit your `.env` into git. Be sure to configure your `.gitignore` to exclude this file.

</Admonition>

For example, if your `.env` contained the following values:

```bash
GITHUB_CLIENT_ID=""
GITHUB_SECRET=""
```

Then you would reference them inside of our `config.toml` like this:

```toml
[auth.external.github]
enabled = true
client_id = "env(GITHUB_CLIENT_ID)"
secret = "env(GITHUB_SECRET)"
redirect_uri = "" # Overrides the default auth redirectUrl.
```