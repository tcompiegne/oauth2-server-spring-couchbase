oauth2-server-spring-couchbase
==============================

OAuth2 Authorization Server based on Spring Security OAuth2 and Couchbase

![spring-oauth2-couchbase] (https://github.com/tcompiegne/oauth2-server-spring-couchbase/raw/master/site/site.PNG)

This is the basic Authorization server based on Spring Security OAuth2.

The main goal is to show you how to implement an Authorization Server with a Couchbase Server token service provider.

How to use it ?
==============================

First of all checkout my other project to retrieve the couchbase token store :

<pre>
- git clone https://github.com/tcompiegne/oauth2-couchbase-token-store.git
- mvn install
</pre>

Checkout the OAuth2 Authorization Server :

<pre>
- git clone https://github.com/tcompiegne/oauth2-server-spring-couchbase.git
- mvn install
</pre>

Install a Couchbase server :

<pre>
  Please refer to the offical documentation : http://www.couchbase.com/download
  The basic installation will be fine.
</pre>

Start the server : 

<pre>
  mvn jetty:run
</pre>

Get your tokens :

<pre>
Client Credentials Grant Type :

=============== =================================================
Request         POST /oauth/token
Request Body    grant_type=client_credentials&client_id=test&client_secret=test
Response Codes  200 OK
Response Body   ::

                  {
                      "access_token": "ecfe59e8-2983-4919-a44a-039766ed1c45",
                      "token_type": "bearer",
                      "expires_in": 43199,
                      "scope": "read write"
                  }

=============== =================================================

Resource Owner Password Grant Type :

=============== =================================================
Request         POST /oauth/token
Request Body    grant_type=password&client_id=test&client_secret=test&username=userTest&password=userTest
Response Codes  200 OK
Response Body   ::

                  {
                      "access_token": "46539a6f-67f0-4bcb-bdef-89e3794825f5",
                      "token_type": "bearer",
                      "refresh_token": "8c8d7232-9523-4838-85f7-14cb3aaa174c",
                      "expires_in": 43199,
                      "scope": "read write"
                  }

=============== =================================================

</pre>

Retrieve your tokens :

You can retrieve thanks to Couchbase web console (http://your-host:8091)

![couchbase-tokens] (https://github.com/tcompiegne/oauth2-server-spring-couchbase/raw/master/site/couchbase-tokens.PNG)


Informations
===================================

Couchbase tokens are no expiry time (they remain indefinitely inside couchbase)

To set an expiry time you can declare your document like this :

<pre>
@Document(expiry = 1000) 
public class OAuth2AccesToken {
  ...
}
</pre>

Community
===================================

I hope you will enjoy my work, any feedbacks will be grateful
