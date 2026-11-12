# Buildable Discourse application stack for Kubernetes on Wodby

Deploy Discourse with your own and third-party plugins on Kubernetes with
Wodby: your Git repository lists the plugins or holds them, and Wodby builds
Discourse with them.

This repository defines the Wodby stack manifests and default service
composition for buildable Discourse.

<!-- wodby:generated:start -->

## Stack contract

- [Discourse stack on Wodby](https://wodby.com/stacks/discourse)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Discourse stack guide](https://wodby.com/docs/2.0/stacks/catalog/discourse/)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Service definitions

- [Buildable Discourse service](https://github.com/wodby/service-discourse-buildable)
- [PostgreSQL service](https://github.com/wodby/service-postgres)
- [Redis service](https://github.com/wodby/service-redis)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)

## What's included

| Component / service | Default configuration |
| --- | --- |
| Discourse<br>`discourse` | required; enabled by default; volumes: `data` 20 GB; links: `db` → `postgres`, `redis` → `redis`, `sendmail` → `opensmtpd` |
| PostgreSQL<br>`postgres` | required; enabled by default; volumes: `data` 20 GB |
| Redis<br>`redis` | required; enabled by default; volumes: `data` 5 GB |
| OpenSMTPD<br>`opensmtpd` | required; enabled by default; volumes: `spool` 1 GB |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Validate the stack manifest

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

<!-- wodby:generated:end -->

## Deploy this stack

Connect a Git repository started from the
[Discourse boilerplate](https://github.com/wodby/discourse-boilerplate):

- `plugins.txt` lists plugins by Git URL, optionally with a branch or tag.
- `plugins/` holds plugins committed to the repository.

Choose the Discourse release line when you create the app. The build starts
from the prebuilt [wodby/discourse](https://github.com/wodby/discourse) image
of that line, adds your plugins and compiles their JavaScript. Plugins that
ship with Discourse are turned on in its settings, not added. To run Discourse
with only its own plugins, use the
[Discourse stack](https://github.com/wodby/stack-discourse).

## Maintain a custom version

1. Fork this repository.
2. Edit the stack manifest.
3. Import the repository as a [Git-backed stack](https://wodby.com/docs/2.0/stacks/create/#create-a-git-backed-stack).

When replacing or renaming a stack service, update every related link target
and derivative reference. Stack-local names and referenced service names are
distinct identifiers.
