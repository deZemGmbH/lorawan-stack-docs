---
title: 'Identity Server Options'
description: ''
---

## Database Options

The Identity Server needs to be connected to a PostgreSQL-compatible database. Details for the form of the URI can be found in the [PostgreSQL documentation](https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING).

- `is.database-uri`: Database connection URI
- `is.read-database-uri`: Read-Only database connection URI {{< distributions "Cloud" "Enterprise" >}}

## Email Options

The Identity Server can be configured with different providers for sending emails. Currently the `sendgrid` and `smtp` providers are implemented.

- `is.email.provider`: Email provider to use

When `sendgrid` is used as provider, an API key is required. For testing, use the sandbox to prevent emails from actually being sent.

- `is.email.sendgrid.api-key`: The SendGrid API key to use
- `is.email.sendgrid.sandbox`: Use SendGrid sandbox mode for testing

When `smtp` is used as provider, provide the address of the SMTP server (`host:port`), as well as the username and password for the SMTP server.

- `is.email.smtp.address`: SMTP server address
- `is.email.smtp.username`: Username to authenticate with
- `is.email.smtp.password`: Password to authenticate with
- `is.email.smtp.connections`: Maximum number of connections to the SMTP server

The email address and name of the sender should be configured regardless of the provider that is used.

- `is.email.sender-address`: The address of the sender
- `is.email.sender-name`: The name of the sender

Most emails contain the name of the network and links to the Identity Server or Console.

- `is.email.network.name`: The name of the network
- `is.email.network.identity-server-url`: The URL of the Identity Server
- `is.email.network.console-url`: The URL of the Console

Although {{% tts %}} comes with a number of builtin email templates, it is possible to override those with custom templates. You can specify the source where to load templates from, and options for that source. For more information on email templates, see the [email templates reference]({{< ref "/reference/email-templates" >}}).

- `is.email.templates.source`: Source of the email template files (directory, url, blob)
- `is.email.templates.directory`: Directory on the filesystem where email templates are located
- `is.email.templates.url`: URL where email templates are located
- `is.email.templates.blob.bucket`: Bucket where email templates are located
- `is.email.templates.blob.path`: Path within the bucket.

If your custom templates rely on other files, such as headers or footers, those files need to be included.

- `is.email.templates.includes`: The email templates that will be preloaded on startup

## OAuth UI Options

The OAuth user interface needs to be configured with at least the canonical URL and the base URL of the Identity Server's HTTP API. The canonical URL needs to be the full URL of the UI, and looks like `https://thethings.example.com/oauth`. The base URL of the Identity Server's HTTP API looks like `https://thethings.example.com/api/v3`.

- `is.oauth.ui.canonical-url`: The page canonical URL
- `is.oauth.ui.is.base-url`: Base URL to the HTTP API

If you do not want to serve the OAuth user interface on `/oauth`, you may customize the mount path.

- `is.oauth.mount`: Path on the server where the OAuth server will be served

If page assets for the OAuth UI are served from a CDN or on a different path on the server, the base URL needs to be customized as well. If you want to [customize the branding]({{< ref "/reference/branding" >}}) of the OAuth UI, you can set the base URL for where your branding assets are located.

- `is.oauth.ui.assets-base-url`: The base URL to the page assets
- `is.oauth.ui.branding-base-url`: The base URL to the branding assets
- `is.oauth.ui.branding-cluster-id`: The cluster ID to show below the logo {{< distributions "Cloud" "Enterprise" >}}
- `is.oauth.ui.branding-text`: The branding text to show below the logo {{< distributions "Cloud" "Enterprise" >}}
- `is.oauth.ui.cluster-picker-url`: A URL to the a cluster picker to enable users to pick the correct cluster of the deployment

The appearance of {{% tts %}} can optionally be customized.

- `is.oauth.ui.site-name`: The site name
- `is.oauth.ui.title`: The page title
- `is.oauth.ui.sub-title`: The page sub-title
- `is.oauth.ui.descriptions`: The page description
- `is.oauth.ui.language`: The page language
- `is.oauth.ui.theme-color`: The page theme color

Further customization of the CSS files, JS files and icons is also possible:

- `is.oauth.ui.css-file`: The names of the CSS files
- `is.oauth.ui.js-file`: The names of the JS files
- `is.oauth.ui.icon-prefix`: The prefix to put before the page icons (favicon.ico, touch-icon.png, og-image.png)

It is possible to highlight some deployment information and disclaimers in the header of the Account App:

- `is.oauth.ui.fair-use-policy-information-url`: A URL with information about the applicable fair use policy of the deployment
- `is.oauth.ui.sla-applies`: The applicable Service Level Agreement of this deployment, e.g. `>99.9%`
- `is.oauth.ui.sla-information-url`: A URL with information about the SLA applicable for this deployment
- `is.oauth.ui.support-plan-applies`: The applicable support plan of this deployment, e.g. `priority`, `24h`
- `is.oauth.ui.support-plan-information-url`: A URL with information about the support plan applicable for this deployment

## Profile Picture Storage Options

The profile pictures that users upload for their accounts are stored in a blob bucket. The global [blob configuration]({{< relref "the-things-stack.md#blob-options" >}}) is used for this. In addition to those options, specify the name of the bucket and the public URL to the bucket.

- `is.profile-picture.bucket`: Bucket used for storing profile pictures
- `is.profile-picture.bucket-url`: Base URL for public bucket access

It is also possible to disable uploads:

- `is.profile-picture.disable-upload`: Disable profile picture uploads

It is also possible to use [Gravatar](https://gravatar.com) for profile pictures.

- `is.profile-picture.use-gravatar`: Use Gravatar fallback for users without profile picture

## End Device Picture Storage Options

Similar to profile pictures, end devices can have pictures associated with them.

- `is.end-device-picture.bucket`: Bucket used for storing end device pictures
- `is.end-device-picture.bucket-url`: Base URL for public bucket access

It is also possible to disable uploads:

- `is.end-device-picture.disable-upload`: Disable end device picture uploads

## User Registration Options

By default, users can register their own user accounts. User accounts can also be registered by admin users in the network. The user registration process can be customized by requiring approval by admin users, requiring email validation or by requiring new users to be invited by existing users.

- `is.user-registration.enabled`: Enable user registration. If user registration is disabled, admin users can still create users. {{< new-in-version "3.11" >}}
- `is.user-registration.admin-approval.required`: Require admin approval for new users
- `is.user-registration.contact-info-validation.required`: Require contact info validation for new users
- `is.user-registration.invitation.required`: Require invitations for new users
- `is.user-registration.invitation.token-ttl`: TTL of user invitation tokens

There are several options to customize the requirements for user passwords.

- `is.user-registration.password-requirements.max-length`: Maximum password length
- `is.user-registration.password-requirements.min-digits`: Minimum number of digits
- `is.user-registration.password-requirements.min-length`: Minimum password length
- `is.user-registration.password-requirements.min-special`: Minimum number of special characters
- `is.user-registration.password-requirements.min-uppercase`: Minimum number of uppercase letters
- `is.user-registration.password-requirements.reject-common`: Reject common passwords {{< new-in-version "3.12.1" >}}
- `is.user-registration.password-requirements.reject-user-id`: Reject passwords that contain user ID {{< new-in-version "3.12.1" >}}

## User Rights Options

By default users can create applications, gateways, organizations and OAuth clients. With the following configuration options it is possible to restrict this, in which case only admin users are allowed to create these entities. By adding users to organizations, and assigning the appropriate rights, they can still create these entities in the organization.

- `is.user-rights.create-applications`: Allow non-admin users to create applications in their user account
- `is.user-rights.create-clients`: Allow non-admin users to create OAuth clients in their user account
- `is.user-rights.create-gateways`: Allow non-admin users to create gateways in their user account
- `is.user-rights.create-organizations`: Allow non-admin users to create organizations in their user account

## Admin Rights Options {#admin-rights-options}

By default admins are granted _almost_ all rights on all entities in the network. The default configuration does not allow admins to read secrets, such as the root keys of end devices, and the CUPS/LNS secrets of gateways. This also means that admins can not assign those rights to others. The following option can be used to grant admin users all possible rights.

- `is.admin-rights.all`: Grant all rights to admins, including `_KEYS` and `_ALL`

## Gateway Secrets Encryption Options{#gateway-secrets-encryption-options}

- `is.gateways.encryption-key-id`: ID of the key used to encrypt gateway secrets at rest.

## Tenant Administration Options {{< distributions "Cloud" "Enterprise" >}} {#tenant-administration-options}

In multi-tenant deployments, tenants are managed with "tenant admin keys". These keys need to be configured in the Identity Server.

- `is.tenancy.admin-keys`: Keys that can be used for tenant administration (16, 24 or 32 hex-encoded bytes) {{< distributions "Cloud" "Enterprise" >}}
