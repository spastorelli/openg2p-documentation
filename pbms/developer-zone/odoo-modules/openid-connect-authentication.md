# OpenID Connect Authentication

### Module name

g2p\_auth\_oidc

### Module title

OpenID Connect Authentication

### Technology base

[Odoo](https://www.odoo.com/)

### Functionality

The functionality of OpenID Connect (OIDC) Authentication module is&#x20;

* It allows users log in to Odoo using external [OIDC](https://openid.net/specs/openid-connect-core-1\_0.html) authentication providers.
* It inherits from the Odoo [OAuth2 Authentication](https://github.com/odoo/odoo/tree/17.0/addons/auth\_oauth) module and adds support for OIDC flows and additional features described here.
* It is a general-purpose Odoo module, not tied to any other G2P modules.

### Alternatives

OCA (Odoo Community Association) offers an [OIDC Authentication](https://github.com/OCA/server-auth/tree/17.0/auth\_oidc) module that provides functionality similar to this but doesn't contain all of the features described here. This module is not related to the OCA module. This module is also NOT compatible (not supposed to be used together) with the OCA module.

### Features

<table><thead><tr><th width="219">Feature</th><th>Descripton</th></tr></thead><tbody><tr><td>OIDC Flows</td><td>Supports Auth Code flow and Implicit flow</td></tr><tr><td>Tokenisation</td><td>Supports Access token and ID token validation</td></tr><tr><td><a href="https://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication">Client Authentication</a></td><td><ul><li>Supports client_secret_post, client_secret_basic, private_key_jwt.</li><li>If using private_key_jwt, allows overriding Audience claim in client Assertion JWT, otherwise defaults to Token Endpoint. (Helps during testing and development)</li></ul></td></tr><tr><td><a href="https://openid.net/specs/openid-connect-core-1_0.html#UserInfoResponse">Userinfo Responses</a></td><td><ul><li><p>Userinfo response content-types supported: </p><ul><li>"application/json"</li><li>"application/jwt" - TODO perform signature validation</li></ul></li><li>Supports mapping of Userinfo Response to fields of Odoo <code>res.user</code> (same as <code>res.partner</code>) table.</li></ul></td></tr><tr><td>Signup Handling</td><td><p>The mechanism involved in handling the users who logged in through the auth provider is not already present in Odoo.-</p><ul><li><p>Modes of Signup configurable:</p><ul><li>Always allow signups through this auth provider.</li><li>Follow the system default signup settings. (This usually involves enabling signup at the system level and configuring a template for new users to be created. Part of <a href="https://github.com/odoo/odoo/tree/17.0/addons/auth_signup">auth_signup</a> Odoo base module. TODO: Update docs.)</li><li>Do not allow signups through this auth provider at all.</li></ul></li><li>If user signups are always allowed for an auth provider, allow configuring default groups to be assigned to the new user.</li></ul></td></tr><tr><td>Group Synchronisation</td><td><p>Sync groups from the Authentication Provider with groups of the Odoo user.</p><ul><li><p>Supports groups sync on:</p><ul><li>every login</li><li>only when user groups are reset</li><li>never</li></ul></li><li>Matches Odoo user groups with the same name as the group from the auth provider.</li></ul></td></tr><tr><td>User Data Update</td><td>Supports update of Odoo user data with auth provider Userinfo, on login, when reset is requested.</td></tr><tr><td>An Icon on Login Page</td><td>Allows provision for showing an Icon for the auth provider on the login page.</td></tr><tr><td>Additional Parameters</td><td>Supports passing additional parameters to Authorize Endpoint. Allows to configure additional parameters as JSON.</td></tr></tbody></table>

### Guides

To learn more on _**Configure Keycloak Auth Provider for User Login**_, click [here](https://docs.openg2p.org/pbms/functionality/administration/role-based-access-control/user-guides/configure-keycloak-authentication-provider-for-user-login).

### Configuration

OAuth Provider Field Reference (OAuth Providers can be viewed in Settings -> General Settings):

The following list includes configuration fields from the base [auth\_oauth](https://github.com/odoo/odoo/tree/17.0/addons/auth\_oauth) Odoo module.

<table><thead><tr><th width="165">Field name</th><th width="211">Field Title</th><th width="271">Description</th><th>Default Value</th></tr></thead><tbody><tr><td>name</td><td>Provider name</td><td>Internal name given to Identify the auth provider</td><td></td></tr><tr><td>flow</td><td>Auth Flow</td><td>Authentication Flow to be used.</td><td>oauth2</td></tr><tr><td>token_map</td><td>Token Map</td><td>Map of Userinfo fields to Odoo user fields.</td><td><pre class="language-bash"><code class="lang-bash">sub:user_id name:name email:email phone_number:phone birthdate:birthdate gender:gender address:address picture:picture groups:groups
</code></pre></td></tr><tr><td>enabled</td><td>Allowed</td><td>Whether or not to show on login page</td><td></td></tr><tr><td>body</td><td>Login button label</td><td>Text to be shown on the button on login page</td><td></td></tr><tr><td>image_icon_url</td><td>Image Icon Url</td><td>Url of the image to be displayed on the login page</td><td></td></tr><tr><td>css_class</td><td>CSS class</td><td>CSS Class to be assigned to Image Icon on login page</td><td><pre><code>fa fa-fw fa-sign-in text-primary
</code></pre></td></tr><tr><td>auth_endpoint</td><td>Authorization URL</td><td></td><td></td></tr><tr><td>token_endpoint</td><td>Token Endpoint</td><td></td><td></td></tr><tr><td>validation_endpoint</td><td>Userinfo URL</td><td></td><td></td></tr><tr><td>jwks_uri</td><td>JWKS URL</td><td></td><td></td></tr><tr><td>jwt_assertion_aud</td><td>Client Assertion JWT Aud Claim</td><td>Ovewrite <em>aud</em> claim in Client assertion JWT. Leave blank to default to Token Endpoint.</td><td></td></tr><tr><td>client_id</td><td>Client ID</td><td></td><td></td></tr><tr><td>client_authentication_method</td><td>Client Authentication Method</td><td><p>Supported Methods:</p><ul><li>client_secret_post</li><li>client_secret_basic</li><li>private_key_jwt</li><li>none</li></ul></td><td>client_secret_post</td></tr><tr><td>client_secret</td><td>Client Secret</td><td>Used when client_authentication_method is client_secret_post/client_secret_basic.</td><td></td></tr><tr><td>client_private_key</td><td>Client Private Key</td><td><p>Supported File types:</p><ul><li>PEM file</li><li>JWKS Json file</li></ul><p>Used when client_authentication_method is private_key_jwt</p></td><td></td></tr><tr><td>scope</td><td>Scope</td><td>OAuth2 Scope</td><td><pre><code>openid profile email
</code></pre></td></tr><tr><td>extra_authorize_params</td><td>Extra Authorize Params</td><td>To be given as JSON</td><td></td></tr><tr><td>verify_at_hash</td><td>Verify AT Hash</td><td>Whether or not to verify Access Token hash during ID Token validation</td><td>true</td></tr><tr><td>date_format</td><td>Date Format</td><td>Format to be used for parsing dates in Userinfo Response (Like birthdate)</td><td></td></tr><tr><td>allow_signup</td><td>Allow Signup</td><td><p>Supported Values:</p><ul><li>Allows user signup (yes)</li><li>Denies user signup (no)</li><li>Use System settings for signup (system_default)</li></ul></td><td>Allows user signup (yes)</td></tr><tr><td>signup_default_groups</td><td>Signup Default Groups</td><td>List of Groups to be assigned to newly created user (when allow_signup == yes)</td><td></td></tr><tr><td>sync_user_groups</td><td>Sync User Groups</td><td><p>Supported Values:</p><ul><li>On every login (on_login)</li><li>When user groups are reset (on_reset)</li><li>Never (never)</li></ul></td><td>When user groups are reset (on_reset)</td></tr><tr><td>company_id</td><td>Company</td><td>Company to which the auth provider belongs to. This will also be used during user creation while signup.</td><td></td></tr></tbody></table>

### Source code

[https://github.com/OpenG2P/openg2p-odoo-commons/tree/17.0-develop/g2p\_auth\_oidc](https://github.com/OpenG2P/openg2p-odoo-commons/tree/17.0-develop/g2p\_auth\_oidc)
