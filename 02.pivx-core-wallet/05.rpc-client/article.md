---
title: 'RPC Client'
date: '14-10-2021 00:00'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
---

### JSON-RPC

Running PIVX with the -server argument (or running pivxd) tells it to function as a HTTP JSON-RPC server, but Basic access authentication must be used when communicating with it, and, for security, by default, the server only accepts connections from other processes on the same machine. If your HTTP or JSON library requires you to specify which 'realm' is authenticated, use 'jsonrpc'.

Allowing arbitrary machines to access the JSON-RPC port (using the rpcallowip configuration option) is dangerous and strongly discouraged-- access should be strictly limited to trusted machines.

To access the server you should find a suitable library for your language.

### Python

python-jsonrpc is the official JSON-RPC implementation for Python. It automatically generates Python methods for RPC calls. However, due to its design for supporting old versions of Python, it is also rather inefficient. jgarzik has forked it as Python-BitcoinRPC and optimized it for current versions. Generally, this version is recommended.

While BitcoinRPC lacks a few obscure features from jsonrpc, software using only the ServiceProxy class can be written the same to work with either version the user might choose to install:

```python
from jsonrpc import ServiceProxy

access = ServiceProxy("http://user:password@127.0.0.1:51473")
access.getinfo()
access.listreceivedbyaddress(6)
access.sendtoaddress("11yEmxiMso2RsFVfBcCa616npBvGgxiBX", 10)
```

The latest version of python-bitcoinrpc has a new syntax.

```python
from bitcoinrpc.authproxy import AuthServiceProxy
```



### Ruby

```ruby
require 'net/http'
require 'uri'
require 'json'

class BitcoinRPC
  def initialize(service_url)
    @uri = URI.parse(service_url)
  end

  def method_missing(name, *args)
    post_body = { 'method' => name, 'params' => args, 'id' => 'jsonrpc' }.to_json
    resp = JSON.parse( http_post_request(post_body) )
    raise JSONRPCError, resp['error'] if resp['error']
    resp['result']
  end

  def http_post_request(post_body)
    http    = Net::HTTP.new(@uri.host, @uri.port)
    request = Net::HTTP::Post.new(@uri.request_uri)
    request.basic_auth @uri.user, @uri.password
    request.content_type = 'application/json'
    request.body = post_body
    http.request(request).body
  end

  class JSONRPCError < RuntimeError; end
end

if $0 == 
  h = BitcoinRPC.new('http://user:password@127.0.0.1:51473')
  p h.getbalance
  p h.getinfo
  p h.getnewaddress
  p h.dumpprivkey( h.getnewaddress )
  # also see: https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_Calls_list
end
```


### Erlang

Get the rebar dependency from https://github.com/edescourtis/ebitcoind . By default the client will use the configuration in $HOME/.pivx/pivx.conf or you can instead specify a URI like this:

```python
ebitcoind:start_link(<<"http://user:password@localhost:51473/">>).
Here is a usage example:

1> {ok,Pid} = ebitcoind:start_link().
{ok,<0.177.0>}
2> ebitcoind:getbalance(Pid).
8437.02478294
3> ebitcoind:getinfo(Pid).
{ok, #{<<"balance">> => 8437.02478294,
  <<"blocks">> => 260404,
  <<"connections">> => 8,
  <<"difficulty">> => 148819199.80509263,
  <<"errors">> => <<>>,
  <<"keypoololdest">> => 1420307921,
  <<"keypoolsize">> => 102,
  <<"paytxfee">> => 0.0,
  <<"protocolversion">> => 70002,
  <<"proxy">> => <<>>,
  <<"relayfee">> => 1.0e-5,
  <<"testnet">> => false,
  <<"timeoffset">> => -3,
  <<"version">> => 90300,
  <<"walletversion">> => 60000}}
4> ebitcoind:setgenerate(Pid,true).
{ok, null}
5> ebitcoind:getblocktemplate(Pid, #{}).
{ok,#{<<"bits">> => <<"181b0dca">>,
      <<"coinbaseaux">> => #{<<"flags">> => <<"062f503253482f">>},
      <<"coinbasevalue">> => 2518690558,
      <<"curtime">> => 1420421249,
      <<"height">> => 337533,
      <<"mintime">> => 1420416332,
      <<"mutable">> => [<<"time">>,<<"transactions">>,<<"prevblock">>],
      <<"noncerange">> => <<"00000000ffffffff">>,
      <<"previousblockhash">> => <<"000000000000000017ce0a0d328bf84cc597785844393e899e9a971a81679a5f">>,
      <<"sigoplimit">> => 20000,
      <<"sizelimit">> => 1000000,
      <<"target">> => <<"00000000000000001b0dca00000000000000000000000000000000000000"...>>,
      <<"transactions">> => [#{<<"data">> => <<"01000000049b47ce225d29bff7c18b7df7d7df4693523a52"...>>,
         <<"depends">> => [],
         <<"fee">> => 0,
         <<"hash">> => <<"6d0d76e1f27b3a6f7325923710dcdb4107c9"...>>,
         <<"sigops">> => 1},
      ...
```

### PHP

The JSON-RPC PHP library also makes it very easy to connect to PIVX. For example:

```php
  require_once 'jsonRPCClient.php';

  $pivx = new jsonRPCClient('http://user:password@127.0.0.1:51473/');

  echo "<pre>\n";
  print_r($pivx->getinfo()); echo "\n";
  echo "Received: ".$pivx->getreceivedbylabel("Your Address")."\n";
  echo "</pre>";
```

Note: The jsonRPCClient library uses fopen() and will throw an exception saying "Unable to connect" if it receives a 404 or 500 error from pivxd. This prevents you from being able to see error messages generated by pivxd (as they are sent with status 404 or 500). The EasyBitcoin-PHP library is similar in function to JSON-RPC PHP but does not have this issue.

### Java

The easiest way to tell Java to use HTTP Basic authentication is to set a default Authenticator:

```java
  final String rpcuser ="...";
  final String rpcpassword ="...";

  Authenticator.setDefault(new Authenticator() {
      protected PasswordAuthentication getPasswordAuthentication() {
          return new PasswordAuthentication (rpcuser, rpcpassword.toCharArray());
      }
  });
```
  
Once that is done, any JSON-RPC library for Java (or ordinary URL POSTs) may be used to communicate with the Bitcoin server.

Instead of writing your own implementation, consider using one of the existing wrappers like BitcoindClient4J, btcd-cli4j or Bitcoin-JSON-RPC-Client instead.

### Perl

The JSON::RPC package from CPAN can be used to communicate with PIVX. You must set the client's credentials; for example:

```perl
  use JSON::RPC::Client;
  use Data::Dumper;

  my $client = new JSON::RPC::Client;

  $client->ua->credentials(
     'localhost:51473', 'jsonrpc', 'user' => 'password'  # REPLACE WITH YOUR pivx.conf rpcuser/rpcpassword
      );

  my $uri = 'http://localhost:51473/';
  my $obj = {
      method  => 'getinfo',
      params  => [],
   };

  my $res = $client->call( $uri, $obj );

  if ($res){
      if ($res->is_error) { print "Error : ", $res->error_message; }
      else { print Dumper($res->result); }
  } else {
      print $client->status_line;
  }
```

### Go

The btcrpcclient package can be used to communicate with PIVX. You must provide credentials to match the client you are communicating with.

```go
package main

import (
	"github.com/btcsuite/btcd/chaincfg"
	"github.com/btcsuite/btcrpcclient"
	"github.com/btcsuite/btcutil"
	"log"
)

func main() {
	// create new client instance
	client, err := btcrpcclient.New(&btcrpcclient.ConnConfig{
		HTTPPostMode: true,
		DisableTLS:   true,
		Host:         "127.0.0.1:51473",
		User:         "rpcUsername",
		Pass:         "rpcPassword",
	}, nil)
	if err != nil {
		log.Fatalf("error creating new btc client: %v", err)
	}

	// list accounts
	accounts, err := client.ListAccounts()
	if err != nil {
		log.Fatalf("error listing accounts: %v", err)
	}
	// iterate over accounts (map[string]btcutil.Amount) and write to stdout
	for label, amount := range accounts {
		log.Printf("%s: %s", label, amount)
	}

	// prepare a sendMany transaction
	receiver1, err := btcutil.DecodeAddress("1someAddressThatIsActuallyReal", &chaincfg.MainNetParams)
	if err != nil {
		log.Fatalf("address receiver1 seems to be invalid: %v", err)
	}
	receiver2, err := btcutil.DecodeAddress("1anotherAddressThatsPrettyReal", &chaincfg.MainNetParams)
	if err != nil {
		log.Fatalf("address receiver2 seems to be invalid: %v", err)
	}
	receivers := map[btcutil.Address]btcutil.Amount{
		receiver1: 42,  // 42 satoshi
		receiver2: 100, // 100 satoshi
	}

	// create and send the sendMany tx
	txSha, err := client.SendMany("some-account-label-from-which-to-send", receivers)
	if err != nil {
		log.Fatalf("error sendMany: %v", err)
	}
	log.Printf("sendMany completed! tx sha is: %s", txSha.String())
}
```

### .NET (C#)

The communication with the RPC service can be achieved using the standard http request/response objects. A library for serializing and deserializing Json will make your life a lot easier:

Json.NET ( http://james.newtonking.com/json ) is a high performance JSON package for .NET. It is also available via NuGet from the package manager console ( Install-Package Newtonsoft.Json ).

The following example uses Json.NET:

```C#
 HttpWebRequest webRequest = (HttpWebRequest)WebRequest.Create("http://localhost.:51473");
 webRequest.Credentials = new NetworkCredential("user", "pwd");
 /// important, otherwise the service can't desirialse your request properly
 webRequest.ContentType = "application/json-rpc";
 webRequest.Method = "POST";

 JObject joe = new JObject();
 joe.Add(new JProperty("jsonrpc", "1.0"));
 joe.Add(new JProperty("id", "1"));
 joe.Add(new JProperty("method", Method));
 // params is a collection values which the method requires..
 if (Params.Keys.Count == 0)
 {
  joe.Add(new JProperty("params", new JArray()));
 }
 else
 {
     JArray props = new JArray();
     // add the props in the reverse order!
     for (int i = Params.Keys.Count - 1; i >= 0; i--)
     {
        .... // add the params
     }
     joe.Add(new JProperty("params", props));
     }

     // serialize json for the request
     string s = JsonConvert.SerializeObject(joe);
     byte[] byteArray = Encoding.UTF8.GetBytes(s);
     webRequest.ContentLength = byteArray.Length;
     Stream dataStream = webRequest.GetRequestStream();
     dataStream.Write(byteArray, 0, byteArray.Length);
     dataStream.Close();


     WebResponse webResponse = webRequest.GetResponse();

     ... // deserialze the response
There is also a wrapper for Json.NET called Bitnet (https://sourceforge.net/projects/bitnet) implementing Bitcoin API in more convenient way:

     BitnetClient bc = new BitnetClient("http://127.0.0.1:51473");
     bc.Credentials = new NetworkCredential("user", "pass");

     var p = bc.GetDifficulty();
     Console.WriteLine("Difficulty:" + p.ToString());

     var inf = bc.GetInfo();
     Console.WriteLine("Balance:" + inf["balance"]);
```
A more complete library and wrapper for Bitcoin (also for Litecoin and all Bitcoin clones) is BitcoinLib (https://github.com/GeorgeKimionis/BitcoinLib) which is also available via NuGet from the package manager console (Install-Package BitcoinLib).

Querying the daemon with BitcoinLib is as simple as:

```C#
     IBitcoinService bitcoinService = new BitcoinService();

     var networkDifficulty = bitcoinService.GetDifficulty();
     var myBalance = bitcoinService.GetBalance();
```

### Node.js

```js
node-bitcoin (npm: bitcoin)
Example using node-bitcoin:
var bitcoin = require('bitcoin');
var client = new bitcoin.Client({
  host: 'localhost',
  port: 51473,
  user: 'user',
  pass: 'pass'
});

client.getDifficulty(function(err, difficulty) {
  if (err) {
    return console.error(err);
  }

  console.log('Difficulty: ' + difficulty);
});
Example using Kapitalize:

var client = require('kapitalize')()

client.auth('user', 'password')

client
.getInfo()
.getDifficulty(function(err, difficulty) {
  console.log('Dificulty: ', difficulty)
})
```

### Command line (cURL)

You can also send commands and see results using cURL or some other command-line HTTP-fetching utility; for example:

```bash
  curl --user user --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo", "params": [] }'
    -H 'content-type: text/plain;' http://127.0.0.1:51473/
```

You will be prompted for your rpcpassword, and then will see something like:

```
  {"result":{"balance":0.000000000000000,"blocks":59952,"connections":48,"proxy":"","generate":false,
     "genproclimit":-1,"difficulty":16.61907875185736},"error":null,"id":"curltest"}
```

### Clojure

clj-btc is a Clojure wrapper for the bitcoin API.

```c
user=> (require '[clj-btc.core :as btc])
nil
user=> (btc/getinfo)
{"timeoffset" 0, "protocolversion" 70001, "blocks" 111908, "errors" "",
 "testnet" true, "proxy" "", "connections" 4, "version" 80500,
 "keypoololdest" 1380388750, "paytxfee" 0E-8M,
 "difficulty" 4642.44443532M, "keypoolsize" 101, "balance" 0E-8M,
 "walletversion" 60000}
```

### C

The C API for processing JSON is Jansson. C applications like libblkmaker use cURL for making the calls and Jansson for interpreting the JSON that cURL fetches.

For example basic usage (which can be easily modified for Bitcoin RPC), see the Jansson example github_commits.c and the associated tutorial.

The following does with libcurl what the cURL example above does:

```c
#include <curl/curl.h>

int main()
{
    CURL *curl = curl_easy_init();
    struct curl_slist *headers = NULL;

    if (curl) {
	const char *data =
	    "{\"jsonrpc\": \"1.0\", \"id\":\"curltest\", \"method\": \"getinfo\", \"params\": [] }";

	headers = curl_slist_append(headers, "content-type: text/plain;");
	curl_easy_setopt(curl, CURLOPT_HTTPHEADER, headers);

	curl_easy_setopt(curl, CURLOPT_URL, "http://127.0.0.1:51473/");

	curl_easy_setopt(curl, CURLOPT_POSTFIELDSIZE, (long) strlen(data));
	curl_easy_setopt(curl, CURLOPT_POSTFIELDS, data);

	curl_easy_setopt(curl, CURLOPT_USERPWD,
			 "bitcoinrpcUSERNAME:bitcoinrpcPASSWORD");

	curl_easy_setopt(curl, CURLOPT_USE_SSL, CURLUSESSL_TRY);

	curl_easy_perform(curl);
    }
    return 0;
}
```

This output can be parsed with Jansson, à la the Jansson tutorial linked to above. (source: Bitcoin StackExchange)

### Qt/C++

QJsonRpc is a Qt/C++ implementation of the JSON-RPC protocol. It integrates nicely with Qt, leveraging Qt's meta object system in order to provide services over the JSON-RPC protocol. QJsonRpc is licensed under the LGPLv2.1.

```c
/*
 * Copyright (C) 2012-2013 Matt Broadstone
 * Contact: http://bitbucket.org/devonit/qjsonrpc
 *
 * This file is part of the QJsonRpc Library.
 *
 * This library is free software; you can redistribute it and/or
 * modify it under the terms of the GNU Lesser General Public
 * License as published by the Free Software Foundation; either
 * version 2.1 of the License, or (at your option) any later version.
 *
 * This library is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
 * Lesser General Public License for more details.
 */
include <QCoreApplication>include <QAuthenticator>include <QStringList>include <QDebug>

include "qjsonrpchttpclient.h"

class HttpClient : public QJsonRpcHttpClient
{
    Q_OBJECT
public:
    HttpClient(const QString &endpoint, QObject *parent = 0)
        : QJsonRpcHttpClient(endpoint, parent)
    {
        // defaults added for my local test server
        m_username = "bitcoinrpc";
        m_password = "232fb3276bbb7437d265298ea48bdc46";
    }

    void setUsername(const QString &username) {
        m_username = username;
    }

    void setPassword(const QString &password) {
        m_password = password;
    }

private Q_SLOTS:
    virtual void handleAuthenticationRequired(QNetworkReply *reply, QAuthenticator * authenticator)
    {
        Q_UNUSED(reply)
        authenticator->setUser(m_username);
        authenticator->setPassword(m_password);
    }

private:
    QString m_username;
    QString m_password;

};

int main(int argc, char **argv)
{
    QCoreApplication app(argc, argv);
    if (app.arguments().size() < 2) {
        qDebug() << "usage: " << argv[0] << "[-u username] [-p password] <command> <arguments>";
        return -1;
    }

    HttpClient client("http://127.0.0.1:51473");
    if (app.arguments().contains("-u")) {
        int idx = app.arguments().indexOf("-u");
        app.arguments().removeAt(idx);
        client.setUsername(app.arguments().takeAt(idx));
    }

    if (app.arguments().contains("-p")) {
        int idx = app.arguments().indexOf("-p");
        app.arguments().removeAt(idx);
        client.setPassword(app.arguments().takeAt(idx));
    }

    QJsonRpcMessage message = QJsonRpcMessage::createRequest(app.arguments().at(1));
    QJsonRpcMessage response = client.sendMessageBlocking(message);
    if (response.type() == QJsonRpcMessage::Error) {
        qDebug() << response.errorData();
        return -1;
    }

    qDebug() << response.toJson();
}
```












