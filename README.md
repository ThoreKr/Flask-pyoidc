# Flask-pyoidc

![PyPI](https://img.shields.io/pypi/v/flask-pyoidc.svg)

This repository contains an example of how to use the [pyoidc](https://github.com/rohe/pyoidc)
library to provide simple OpenID Connect authentication (using the ["Code Flow"](http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth).

## Usage

The extension support both static and dynamic provider configuration discovery as well as static
and dynamic client registration. The different modes of provider configuration can be combined in
any way with the different client registration modes.
 
* Static provider configuration: `OIDCAuthentication(provider_configuration_info=provider_config)`,
  where `provider_config` is a dictionary containing the [provider metadata](https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderMetadata).
* Dynamic provider configuration: `OIDCAuthentication(issuer=issuer_url)`, where `issuer_url`
  is the issuer URL of the provider.
* Static client registration: `OIDCAuthentication(client_registration_info=client_info)`, where
  `client_info` is all the [registered metadata](https://openid.net/specs/openid-connect-registration-1_0.html#RegistrationResponse)
  about the client. The `redirect_uris` registered with the provider MUST include
  `<flask_url>/redirect_uri`, where `<flask_url>` is the URL for the Flask application.
  


The application using this extension MUST set the following [builtin configuration values of Flask](http://flask.pocoo.org/docs/0.10/config/#builtin-configuration-values):

* `SERVER_NAME` (MUST be the same as `<flask_url>` if using static client registration
* `SECRET_KEY` (this extension relies on Flask session, which requires `SECRET_KEY`)

Have a look at the example Flask app in [app.py](example/app.py) for an idea of how to use it.