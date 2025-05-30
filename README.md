
# Getting Started with PayPal REST APIs

## Introduction

An order represents a payment between two or more parties. Use the Orders API to create, update, retrieve, authorize, and capture orders., Call the Payments API to authorize payments, capture authorized payments, refund payments that have already been captured, and show payment information. Use the Payments API in conjunction with the <a href="/docs/api/orders/v2/">Orders API</a>. For more information, see the <a href="/docs/checkout/">PayPal Checkout Overview</a>., The Payment Method Tokens API saves payment methods so payers don't have to enter details for future transactions. Payers can check out faster or pay without being present after they agree to save a payment method.<br><br>The API associates a payment method with a temporary setup token. Pass the setup token to the API to exchange the setup token for a permanent token.<br><br>The permanent token represents a payment method that's saved to the vault. This token can be used repeatedly for checkout or recurring transactions such as subscriptions.<br><br>The Payment Method Tokens API is available in the US only.

Find out more here: [https://developer.paypal.com/docs/api/orders/v2/](https://developer.paypal.com/docs/api/orders/v2/)

## Building

You must have Python `3.7+` installed on your system to install and run this SDK. This SDK package depends on other Python packages like pytest, etc. These dependencies are defined in the `requirements.txt` file that comes with the SDK. To resolve these dependencies, you can use the PIP Dependency manager. Install it by following steps at [https://pip.pypa.io/en/stable/installing/](https://pip.pypa.io/en/stable/installing/).

Python and PIP executables should be defined in your PATH. Open command prompt and type `pip --version`. This should display the version of the PIP Dependency Manager installed if your installation was successful and the paths are properly defined.

* Using command line, navigate to the directory containing the generated files (including `requirements.txt`) for the SDK.
* Run the command `pip install -r requirements.txt`. This should install all the required dependencies.

![Building SDK - Step 1](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&step=installDependencies)

## Installation

The following section explains how to use the paypalrestapis library in a new project.

### 1. Open Project in an IDE

Open up a Python IDE like PyCharm. The basic workflow presented here is also applicable if you prefer using a different editor or IDE.

![Open project in PyCharm - Step 1](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&step=pyCharm)

Click on `Open` in PyCharm to browse to your generated SDK directory and then click `OK`.

![Open project in PyCharm - Step 2](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&step=openProject0)

The project files will be displayed in the side bar as follows:

![Open project in PyCharm - Step 3](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&projectName=paypalrestapis&step=openProject1)

### 2. Add a new Test Project

Create a new directory by right clicking on the solution name as shown below:

![Add a new project in PyCharm - Step 1](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&projectName=paypalrestapis&step=createDirectory)

Name the directory as "test".

![Add a new project in PyCharm - Step 2](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&step=nameDirectory)

Add a python file to this project.

![Add a new project in PyCharm - Step 3](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&projectName=paypalrestapis&step=createFile)

Name it "testSDK".

![Add a new project in PyCharm - Step 4](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&projectName=paypalrestapis&step=nameFile)

In your python file you will be required to import the generated python library using the following code lines

```python
from paypalrestapis.paypalrestapis_client import PaypalrestapisClient
```

![Add a new project in PyCharm - Step 5](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&projectName=paypalrestapis&libraryName=paypalrestapis.paypalrestapis_client&className=PaypalrestapisClient&step=projectFiles)

After this you can write code to instantiate an API client object, get a controller object and  make API calls. Sample code is given in the subsequent sections.

### 3. Run the Test Project

To run the file within your test project, right click on your Python file inside your Test project and click on `Run`

![Run Test Project - Step 1](https://apidocs.io/illustration/python?workspaceFolder=Paypalrestapis-Python&projectName=paypalrestapis&libraryName=paypalrestapis.paypalrestapis_client&className=PaypalrestapisClient&step=runProject)

## Initialize the API Client

**_Note:_** Documentation for the client can be found [here.](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/client.md)

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| environment | `Environment` | The API environment. <br> **Default: `Environment.SANDBOX`** |
| http_client_instance | `HttpClient` | The Http Client passed from the sdk user for making requests |
| override_http_client_configuration | `bool` | The value which determines to override properties of the passed Http Client from the sdk user |
| http_call_back | `HttpCallBack` | The callback value that is invoked before and after an HTTP call is made to an endpoint |
| timeout | `float` | The value to use for connection timeout. <br> **Default: 60** |
| max_retries | `int` | The number of times to retry an endpoint call if it fails. <br> **Default: 0** |
| backoff_factor | `float` | A backoff factor to apply between attempts after the second try. <br> **Default: 2** |
| retry_statuses | `Array of int` | The http statuses on which retry is to be done. <br> **Default: [408, 413, 429, 500, 502, 503, 504, 521, 522, 524]** |
| retry_methods | `Array of string` | The http methods on which retry is to be done. <br> **Default: ['GET', 'PUT']** |
| logging_configuration | [`LoggingConfiguration`](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/logging-configuration.md) | The SDK logging configuration for API calls |
| client_credentials_auth_credentials | [`ClientCredentialsAuthCredentials`](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/auth/oauth-2-client-credentials-grant.md) | The credential object for OAuth 2 Client Credentials Grant |

The API client can be initialized as follows:

```python
client = PaypalrestapisClient(
    client_credentials_auth_credentials=ClientCredentialsAuthCredentials(
        o_auth_client_id='OAuthClientId',
        o_auth_client_secret='OAuthClientSecret'
    ),
    environment=Environment.SANDBOX,
    logging_configuration=LoggingConfiguration(
        log_level=logging.INFO,
        request_logging_config=RequestLoggingConfiguration(
            log_body=True
        ),
        response_logging_config=ResponseLoggingConfiguration(
            log_headers=True
        )
    )
)
```

## Environments

The SDK can be configured to use a different environment for making API calls. Available environments are:

### Fields

| Name | Description |
|  --- | --- |
| Production | PayPal Live Environment |
| Sandbox | **Default** PayPal Sandbox Environment |

## Authorization

This API uses the following authentication schemes.

* [`Oauth2 (OAuth 2 Client Credentials Grant)`](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/auth/oauth-2-client-credentials-grant.md)

## List of APIs

* [Orders](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/controllers/orders.md)
* [Payments](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/controllers/payments.md)
* [Vault](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/controllers/vault.md)

## SDK Infrastructure

### Configuration

* [AbstractLogger](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/abstract-logger.md)
* [LoggingConfiguration](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/logging-configuration.md)
* [RequestLoggingConfiguration](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/request-logging-configuration.md)
* [ResponseLoggingConfiguration](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/response-logging-configuration.md)

### HTTP

* [HttpResponse](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/http-response.md)
* [HttpRequest](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/http-request.md)

### Utilities

* [ApiHelper](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/api-helper.md)
* [HttpDateTime](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/http-date-time.md)
* [RFC3339DateTime](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/rfc3339-date-time.md)
* [UnixDateTime](https://www.github.com/tahaali2000/test-python-sdk/tree/9.5.6/doc/unix-date-time.md)

