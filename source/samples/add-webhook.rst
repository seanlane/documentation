.. code-block:: bash

    curl -s --user 'api:YOUR_API_KEY' \
	https://api.mailgun.net/v3/domains/YOUR_DOMAIN_NAME/webhooks \
	-F id='clicked' \
	-F url='http://bin.example.com/8de4a9c4'
	-F url='http://bin.example.com/8de4a9c5'
	-F url='http://bin.example.com/8de4a9c6'

.. code-block:: java

 import com.mashape.unirest.http.HttpResponse;
 import com.mashape.unirest.http.JsonNode;
 import com.mashape.unirest.http.Unirest;
 import com.mashape.unirest.http.exceptions.UnirestException;
 
 public class MGSample {
 
     // ...
 
     public static JsonNode addWebhook() throws UnirestException {
 
         HttpResponse <JsonNode> request = Unirest.post("https://api.mailgun.net/v3/domains/" + YOUR_DOMAIN_NAME + "/webhooks")
 		      .basicAuth("api", API_KEY)
 			  .field("id","click")
 		      .field("url", { 
                   "http://bin.example.com/8de4a9c4", 
                   "http://bin.example.com/8de4a9c5", 
                   "http://bin.example.com/8de4a9c6" 
              })
 		      .asJson();
 
         return request.getBody();
     }
 }

.. code-block:: php

  # Include the Autoloader (see "Libraries" for install instructions)
  require 'vendor/autoload.php';
  use Mailgun\Mailgun;

  # Instantiate the client.
  $mgClient = new Mailgun('YOUR_API_KEY');
  $domain = 'YOUR_DOMAIN_NAME';

  # Issue the call to the client.
  $result = $mgClient->post("domains/$domain/webhooks", array(
      'id'  => 'clicked',
      'url' => array(
          'http://bin.example.com/8de4a9c4',
          'http://bin.example.com/8de4a9c5',
          'http://bin.example.com/8de4a9c6'
      )
  ));

.. code-block:: py

 def add_webhook():
     return requests.post(
         "https://api.mailgun.net/v3/domains/YOUR_DOMAIN_NAME/webhooks",
         auth=("api", "YOUR_API_KEY"),
         data={
           'id':'clicked', 
           'url':[ 'http://bin.example.com/8de4a9c4',            
		     'http://bin.example.com/8de4a9c5',
		     'http://bin.example.com/8de4a9c6'
           ]
         })

.. code-block:: rb

 def add_webhook
   RestClient.post("https://api:YOUR_API_KEY"\
                   "@api.mailgun.net/v3/domains/YOUR_DOMAIN_NAME/webhooks",
                   :id => 'clicked',
                   :url => ['http://bin.example.com/8de4a9c4',
                            'http://bin.example.com/8de4a9c5',
                            'http://bin.example.com/8de4a9c6'])
 end

.. code-block:: csharp

 using System;
 using System.IO;
 using RestSharp;
 using RestSharp.Authenticators;

 public class AddWebhookChunk
 {

     public static void Main (string[] args)
     {
         Console.WriteLine (AddWebhook ().Content.ToString ());
     }

     public static IRestResponse AddWebhook ()
     {
         RestClient client = new RestClient ();
         client.BaseUrl = new Uri ("https://api.mailgun.net/v3/");
         client.Authenticator =
             new HttpBasicAuthenticator ("api",
                                         "YOUR_API_KEY");
         RestRequest request = new RestRequest ();
         request.Resource = "domains/YOUR_DOMAIN_NAME/webhooks";
         request.AddParameter ("id", "clicked");
         request.AddParameter ("url", new [] { 
              "http://bin.example.com/8de4a9c4", 
              "http://bin.example.com/8de4a9c5", 
              "http://bin.example.com/8de4a9c6"
         });
         request.Method = Method.POST;
         return client.Execute (request);
     }

 }

.. code-block:: go

 func CreateWebhook(domain, apiKey string) error {
   mg := mailgun.NewMailgun(domain, apiKey, "")
   return mg.CreateWebhook("deliver", "http://www.example.com")
 }

.. code-block:: js

 var DOMAIN = 'YOUR_DOMAIN_NAME';
 var mailgun = require('mailgun-js')({ apiKey: "YOUR_API_KEY", domain: DOMAIN });

 mailgun.post(`/domain/${DOMAIN}/webhooks`, {"id": 'clicked', "url": ['http://bin.example.com/8de4a9c4, http://bin.example.com/8de4a9c5, http://bin.example.com/8de4a9c6'}, function (error, body) {
   console.log(body);
 });
