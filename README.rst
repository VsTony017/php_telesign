========
TeleSign
========

**Information**: For more information, visit the `TeleSign website <http://www.TeleSign.com>`_ or the `TeleSign Developer Portal <https://developer.telesign.com/>`_.

**Author**: Telesign Corp.

TeleSign Web Services: PHP SDK
---------------------------------

**TeleSign web services** conform to the `REST Web Service Design Model <http://en.wikipedia.org/wiki/Representational_state_transfer>`_. Services are exposed as URI-addressable resources through the set of *RESTful* procedures in our **TeleSign REST API**.

The **TeleSign PHP SDK** is a PHP library that provides an interface to `TeleSign web services <https://developer.telesign.com/docs/getting-started-with-the-rest-api/>`_. You can include the SDK by including the 'api.class.php' file located here: https://github.com/TeleSign/php_telesign/tree/master/telesign/api.class.php .

Authentication
--------------

**You will need a Customer ID and API Key in order to use TeleSign’s REST API**.  If you are already a customer and need an API Key, you can generate one in `TelePortal <https://portal.telesign.com>`_.  If you are not a customer and would like to get an API Key, please contact `support@telesign.com <mailto:support@telesign.com>`_.

You supply your credentials to the API by passing them in during class initialization.

>>>
  include './telesign/api.class.php';
  $customer_id = "CUSTOMER_ID_GOES_HERE";
  $secret_key = "SECRECT_KEY_GOES_HERE";
  $verify = new Verify($customer_id, $secret_key);

The PHP Classes
------------------

With just two classes, **telesign.api** abstracts much of the complexity of the TeleSign REST API.

+------------------------------+--------------------------------------------------------------------------+ 
| PHP Class                   | Description                                                              | 
+==============================+==========================================================================+ 
|           PhoneId            | The **PhoneId** class exposes four services that each provide            | 
|                              | information about a specified phone number.                              | 
|                              |                                                                          | 
|                              | *standard*                                                               | 
|                              |     Retrieves the standard set of details about the specified phone      | 
|                              |     number. This includes the type of phone (for example, land line or   | 
|                              |     mobile), and its approximate geographic location.                    | 
|                              | *score*                                                                  | 
|                              |     Retrieves a score for the specified phone number. This ranks the     | 
|                              |     phone number's "risk level" on a scale from 0 to 1000, so you can    | 
|                              |     code your web application to handle particular use cases (for        | 
|                              |     example, to stop things like chargebacks, identity theft, fraud,     | 
|                              |     and spam).                                                           |
|                              | *contact*                                                                | 
|                              |     In addition to the information retrieved by *standard*, this service | 
|                              |     provides the name and address associated with the specified phone    | 
|                              |     number.                                                              | 
|                              | *live*                                                                   |
|                              |     In addition to the information retrieved by *standard*, this         |
|                              |     service provides actionable data associated with the specified phone |
|                              |     number.                                                              |
|                              |                                                                          |
+------------------------------+--------------------------------------------------------------------------+ 
|           Verify             | The **Verify** class exposes three services for sending users a          | 
|                              | verification token (a three to five-digit number). You can use this      | 
|                              | mechanism to test whether you can reach users at the phone number        | 
|                              | they supplied, or you can have them use the token to authenticate        | 
|                              | themselves with your web application. In addition, this class also       | 
|                              | exposes a service that allows you to confirm the result of the           | 
|                              | authentication.                                                          | 
|                              |                                                                          | 
|                              | You can use this verification factor in combination with *username*      | 
|                              | and *password* to provide *two-factor* authentication for higher         | 
|                              | security.                                                                | 
|                              |                                                                          | 
|                              | *call*                                                                   | 
|                              |     Calls the specified phone number and uses speech synthesis to speak  | 
|                              |     the verification code to the user.                                   | 
|                              | *sms*                                                                    | 
|                              |     Sends a text message containing the verification code to the         | 
|                              |     specified phone number (supported for mobile phones only).           | 
|                              | *status*                                                                 | 
|                              |     Retrieves the verification result. You make this call in your web    | 
|                              |     application after users complete the authentication transaction      | 
|                              |     (using either a *call* or *sms*).                                    | 
|                              |                                                                          | 
+------------------------------+--------------------------------------------------------------------------+ 

PHP Code Example: To Verify a Call
-------------------------------------

Here's a basic code example.

>>>
  $customer_id = "CUSTOMER_ID_GOES_HERE";
  $secret_key = "SECRECT_KEY_GOES_HERE";
  $verify = new Verify($customer_id, $secret_key);
  $ret = $verify->call("13103409700");
  print_r($ret);
  {"reference_id":"013C8CC050DF040BE4D412D700002101","resource_uri":"/v1/verify/013C8CC050DF040BE4D412D700002101","sub_resource":"call","errors":[],"status":{"updated_on":"2013-01-30T18:37:59.444100Z","code":103,"description":"Call in progress"},"verify":{"code_state":"UNKNOWN","code_entered":""}}

Documentation
-------------

Detailed documentation for TeleSign™ REST APIs is available in the
`Developer Portal <https://developer.telesign.com/>`_.

Testing
-------

The easiest way to run the tests is to install `phpunit
<http://junit.org/>`_ Tests are located in the *test/* directory.

Support and Feedback
--------------------

For more information about the Phone Verify and PhoneID Standard services, please contact your TeleSign representative:

Email: `support@telesign.com <mailto:support@telesign.com>`_
