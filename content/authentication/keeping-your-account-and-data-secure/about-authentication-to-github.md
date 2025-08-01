---
title: About authentication to GitHub
intro: 'You can securely access your account''s resources by authenticating to {% data variables.product.github %}, using different credentials depending on where you authenticate.'
versions:
  fpt: '*'
  ghes: '*'
  ghec: '*'
topics:
  - Identity
  - Access management
redirect_from:
  - /github/authenticating-to-github/about-authentication-to-github
  - /github/authenticating-to-github/keeping-your-account-and-data-secure/about-authentication-to-github
shortTitle: Authentication to GitHub
---
## About authentication to {% data variables.product.github %}

To keep your account secure, you must authenticate before you can access certain resources on {% data variables.product.github %}. When you authenticate to {% data variables.product.github %}, you supply or confirm credentials that are unique to you to prove that you are exactly who you declare to be.

You can access your resources in {% data variables.product.github %} in a variety of ways: in the browser, via {% data variables.product.prodname_desktop %} or another desktop application, with the API, or via the command line. Each way of accessing {% data variables.product.github %} supports different modes of authentication.
{%- ifversion not fpt %}
* Your identity provider (IdP){% endif %}
* Username and password (or social login) with two-factor authentication, or a passkey ({% data variables.product.prodname_free_user %}, and {% data variables.product.prodname_ghe_cloud %} only)
* {% data variables.product.pat_generic_caps %}
* SSH key

## Authenticating in your browser

{% ifversion fpt or ghec %}

If you're a member of an {% data variables.enterprise.prodname_emu_enterprise %}, you will authenticate to {% data variables.product.github %} in your browser using your IdP. For more information, see [AUTOTITLE](/enterprise-cloud@latest/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users#authenticating-as-a-managed-user){% ifversion fpt %} in the {% data variables.product.prodname_ghe_cloud %} documentation.{% else %}.{% endif %}

If you're not a member of an {% data variables.enterprise.prodname_emu_enterprise %}, you will authenticate using your {% data variables.product.prodname_dotcom %} username and password, or a passkey. You may also use two-factor authentication and SAML single sign-on, which can be required by organization and enterprise owners.

{% else %}

You can authenticate to {% data variables.product.github %} in your browser in a number of ways.

{% endif %}

{% ifversion mandatory-2fa-dotcom-contributors %}
{% data reusables.two_fa.mandatory-2fa-contributors-2023 %}
{% endif %}

If you need to use multiple accounts on {% data variables.location.product_location %}, such as a personal account and a service account, you can quickly switch between your accounts without always needing to reauthenticate each time. For more information, see [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/switching-between-accounts).

* **Username and password only**
  * You'll create a password when you create your account on {% data variables.product.github %}. We recommend that you use a password manager to generate a random and unique password. For more information, see [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/creating-a-strong-password).{% ifversion fpt or ghec %}
  * If you have not enabled 2FA, {% data variables.product.github %} may ask for additional verification when you first sign in from a new or unrecognized device, such as a new browser profile, a browser where the cookies have been deleted, or a new computer. For more information, see [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/verifying-new-devices-when-signing-in).{% endif %} {% ifversion fpt or ghec %}
* **Social login**
  * You'll authenticate with one of the supported social login providers (currently only Google is supported) when you create your account on {% data variables.product.github %}. We recommend that you also configure 2FA and add a passkey or a password as an additional account recovery mechanism.
  * If you have an existing account created with a password, you can add your social login email to the account. This allows you to use your social login identity as a first-factor (password) replacement when you sign in to {% data variables.product.github %}.
  * You can unlink your social login identities from your {% data variables.product.github %} email settings page. For more information, see [AUTOTITLE](/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-your-personal-account/unlinking-your-email-address-from-a-locked-account) {% endif %}
* **Two-factor authentication (2FA)** (recommended)
  * If you enable two-factor authentication (2FA), after you sign in with social login or your username and password, you'll be prompted to enter a code from a time-based one-time password (TOTP) application on your mobile device{% ifversion fpt or ghec %} or sent as a text message (SMS).{% endif %}{% ifversion 2fa-check-up-period %}
  * After you configure 2FA, your account enters a check up period for 28 days. You can leave the check up period by successfully performing 2FA within those 28 days. If you don't perform 2FA in that timespan, you'll then be asked to perform 2FA inside one of your existing {% data variables.product.prodname_dotcom %} sessions.
  * If you cannot perform 2FA to pass the 28th day checkup, you will be provided a shortcut that lets you reconfigure your 2FA settings. You must reconfigure your settings before you can access the rest of {% data variables.product.prodname_dotcom %}{% endif %}. For more information, see [AUTOTITLE](/authentication/securing-your-account-with-two-factor-authentication-2fa/accessing-github-using-two-factor-authentication#providing-a-2fa-code-when-signing-in-to-the-website){% ifversion 2fa-check-up-period %} and [AUTOTITLE](/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication){% endif %}.
  * In addition to authentication with a TOTP application{% ifversion fpt or ghec %} or a text message{% endif %}, you can optionally add an alternative method of authentication with {% ifversion fpt or ghec %}{% data variables.product.prodname_mobile %} or{% endif %} a security key using WebAuthn. See {% ifversion fpt or ghec %}[Configuring two-factor authentication using {% data variables.product.prodname_mobile %}](/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication#configuring-two-factor-authentication-using-github-mobile) or {% endif %}[Configuring two-factor authentication using a security key](/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication#configuring-two-factor-authentication-using-a-security-key).

    {% ifversion fpt or ghec %}

    > [!NOTE]
    > {% data reusables.two_fa.unlink-email-address %}

    {% endif %}
* **Passkey**
  * You can add a passkey to your account to enable a secure, passwordless login. Passkeys satisfy both password and 2FA requirements, so you can complete your sign in with a single step. See [AUTOTITLE](/authentication/authenticating-with-a-passkey/about-passkeys).

{% ifversion ghes %}
* **External authentication**
  * Your site administrator may configure {% data variables.location.product_location_enterprise %} to use external authentication instead of a username and password. For more information, see [AUTOTITLE](/admin/identity-and-access-management/managing-iam-for-your-enterprise/about-authentication-for-your-enterprise#external-authentication).{% endif %}{% ifversion fpt or ghec %}
* **SAML single sign-on**
  * Before you can access resources owned by an organization or enterprise account that uses SAML single sign-on, you may need to also authenticate through an IdP. For more information, see [AUTOTITLE](/authentication/authenticating-with-saml-single-sign-on/about-authentication-with-saml-single-sign-on){% ifversion fpt %} in the {% data variables.product.prodname_ghe_cloud %} documentation.{% else %}.{% endif %}{% endif %}

### Session cookies

{% data variables.product.company_short %} uses cookies to provide services and increase security. {% ifversion fpt or ghec %}You can review details about {% data variables.product.company_short %}'s cookies in [AUTOTITLE](/free-pro-team@latest/site-policy/privacy-policies/github-cookies).{% endif %}

* The gist.{% ifversion fpt or ghec %}github.com{% elsif ghes %}HOSTNAME domain{% endif %} and {% ifversion fpt or ghec %}github.com domains{% elsif ghes %}base domain for your instance{% endif %} use separate cookies.
* {% data variables.product.github %} typically marks a user session for deletion after two weeks of inactivity.
* {% data variables.product.github %} does not immediately delete a session when you sign out. Periodically, {% data variables.product.github %} automatically deletes expired sessions.

## Authenticating with {% data variables.product.prodname_desktop %}

You can authenticate with {% data variables.product.prodname_desktop %} using your browser. For more information, see [AUTOTITLE](/desktop/installing-and-authenticating-to-github-desktop/authenticating-to-github-in-github-desktop).

## Authenticating with the API

You can authenticate with the API in different ways. For more information, see [AUTOTITLE](/rest/overview/other-authentication-methods).

### Authenticating to the API with a {% data variables.product.pat_generic %}

If you want to use the {% data variables.product.company_short %} REST API for personal use, you can create a {% data variables.product.pat_generic %}. If possible, {% data variables.product.company_short %} recommends that you use a {% data variables.product.pat_v2 %} instead of a {% data variables.product.pat_v1 %}. For more information about creating a {% data variables.product.pat_generic %}, see [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

### Authenticating to the API with an app

If you want to use the API on behalf of an organization or another user, {% data variables.product.company_short %} recommends that you use a {% data variables.product.prodname_github_app %}. For more information, see [AUTOTITLE](/apps/creating-github-apps/authenticating-with-a-github-app/about-authentication-with-a-github-app).

You can also create an OAuth token with an {% data variables.product.prodname_oauth_app %} to access the REST API. However, {% data variables.product.company_short %} recommends that you use a {% data variables.product.prodname_github_app %} instead. {% data variables.product.prodname_github_apps %} allow more control over the access and permission that the app has.

### Authenticating to the API in a {% data variables.product.prodname_actions %} workflow

If you want to use the API in a {% data variables.product.prodname_actions %} workflow, {% data variables.product.company_short %} recommends that you authenticate with the built-in `GITHUB_TOKEN` instead of creating a token. You can grant permissions to the `GITHUB_TOKEN` with the `permissions` key.

Note that `GITHUB_TOKEN` can only access resources within the repository that contains the workflow. If you need to make changes to resources outside of the workflow repository, you will need to use a {% data variables.product.pat_generic %} or {% data variables.product.prodname_github_app %}.

For more information, see [AUTOTITLE](/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token).

## Authenticating with the command line

You can access repositories on {% data variables.product.github %} from the command line in two ways, HTTPS and SSH, and both have a different way of authenticating. The method of authenticating is determined based on whether you choose an HTTPS or SSH remote URL when you clone the repository. For more information about which way to access, see [AUTOTITLE](/get-started/git-basics/about-remote-repositories).

### HTTPS

You can work with all repositories on {% data variables.product.github %} over HTTPS, even if you are behind a firewall or proxy.

If you authenticate with {% data variables.product.prodname_cli %}, you can either authenticate with a {% data variables.product.pat_generic %} or via the web browser. For more information about authenticating with {% data variables.product.prodname_cli %}, see [`gh auth login`](https://cli.github.com/manual/gh_auth_login).

If you authenticate without {% data variables.product.prodname_cli %}, {% ifversion fpt or ghec %}you must authenticate with a {% data variables.product.pat_generic %}. {% data reusables.user-settings.password-authentication-deprecation %} Every time you use Git to authenticate with {% data variables.product.github %}, you'll be prompted to enter your credentials, unless you cache them with a [credential helper](/get-started/git-basics/caching-your-github-credentials-in-git).{% elsif ghes %}you can use authentication methods whose availability depend on your IdP.

The table outlines the available authentication methods based on the IdP configured for your instance. Different IdPs may impose specific restrictions or enable certain features, such as disabling password authentication. For more details, see [AUTOTITLE](/admin/authentication).

| IdP | Available authentication methods | More information |
| :- | :- | :- |
| SAML | {% data variables.product.pat_generic_caps %} | Password authentication disabled |
| LDAP | {% data variables.product.pat_generic_caps %} or Username / Password | Password authentication can be disabled by the site administrator |
| Built-in authentication | {% data variables.product.pat_generic_caps %} or Username / Password | Password authentication cannot be disabled |

{% endif %}

### SSH

You can work with all repositories on {% data variables.product.github %} over SSH, although firewalls and proxies might refuse to allow SSH connections.

If you authenticate with {% data variables.product.prodname_cli %}, the CLI will find SSH public keys on your machine and will prompt you to select one for upload. If {% data variables.product.prodname_cli %} does not find a SSH public key for upload, it can generate a new SSH public/private keypair and upload the public key to your account on {% data variables.location.product_location %}. Then, you can either authenticate with a {% data variables.product.pat_generic %} or via the web browser. For more information about authenticating with {% data variables.product.prodname_cli %}, see [`gh auth login`](https://cli.github.com/manual/gh_auth_login).

If you authenticate without {% data variables.product.prodname_cli %}, you will need to generate an SSH public/private keypair on your local machine and add the public key to your account on {% data variables.location.product_location %}. For more information, see [AUTOTITLE](/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). Every time you use Git to authenticate with {% data variables.product.github %}, you'll be prompted to enter your SSH key passphrase, unless you've [stored the key](/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent).

{% ifversion fpt or ghec %}

### Authorizing for SAML single sign-on

To use a {% data variables.product.pat_generic %} or SSH key to access resources owned by an organization that uses SAML single sign-on, you must also authorize the personal token or SSH key. For more information, see [AUTOTITLE](/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/authorizing-a-personal-access-token-for-use-with-saml-single-sign-on) or [AUTOTITLE](/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/authorizing-an-ssh-key-for-use-with-saml-single-sign-on){% ifversion fpt %} in the {% data variables.product.prodname_ghe_cloud %} documentation.{% else %}.{% endif %}{% endif %}

## {% data variables.product.company_short %}'s token formats

{% data variables.product.company_short %} issues tokens that begin with a prefix to indicate the token's type.

| Token type | Prefix | More information |
| :- | :- | :- |
| {% data variables.product.pat_v1_caps %} | `ghp_` | [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-personal-access-token-classic)  |
| {% data variables.product.pat_v2_caps %} | `github_pat_` | [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-fine-grained-personal-access-token) |
| OAuth access token | `gho_` | [AUTOTITLE](/apps/oauth-apps/building-oauth-apps/authorizing-oauth-apps) |
| User access token for a {% data variables.product.prodname_github_app %} | `ghu_` | [AUTOTITLE](/apps/creating-github-apps/authenticating-with-a-github-app/identifying-and-authorizing-users-for-github-apps) |
| Installation access token for a {% data variables.product.prodname_github_app %} | `ghs_` | [AUTOTITLE](/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app-installation) |
| Refresh token for a {% data variables.product.prodname_github_app %} | `ghr_` | [AUTOTITLE](/apps/creating-github-apps/authenticating-with-a-github-app/refreshing-user-access-tokens) |
