---

copyright:

  years:  2017

lastupdated: "2017-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}


# Coalesce.Info for BlueMix

# Getting Started with Coalesce.Info for Risk Analysis
{: #gettingstarted_coalesce}

Investment managers, Risk and Compliance professionals use a wide variety of tools to understand the risks inherent in their investments. Coalesce is a unique Artificial Intelligence product that uses IBM Watson® to allow analysts and business users to search the internet and all forms of internal data for “Signals” that may be relevant to risk analysis.{:shortdesc}

To learn more about Coalesce.Info, visit our [website](http://coalesce.info/) {:new_window}.

To start using Coalesce.Info, please first sign up for an account. Click [here](https://v2-0.coalesce.info/html/index.html#/signup){:new_window} to get started!

Once you've signed up to use Coalesce.Info, there are a few easy steps to go live.

1.  [Log-in](https://v2-0.coalesce.info/html/index.html#/login){:new_window} into the Coalesce.Info with the credentials used for signup to view news alerts for the sample Fortune 500 companies.
  
2.	Copy your Coalesce username / password credentials into the Bluemix developer portal (Note: Never share your credentials outside of the Bluemix developer portal!)

3.	Use the Coalesce.Info API for real-time access (requires subscription) 

Coalesce.Info is free for 7 days. After that you will need to subscribe for continued access.

## API access 

To access the Coalesce APIs, a valid sessionId is necessary. To generate the sessionId one should have the valid username and password credentials.

You can use the same username / password used for Signup or Contact the support team to create username and password for you.

By default the response from the API feed is in JSON format.

## Authentication

Follow the steps to create the sessionId:
     URI : https://v2-0.coalesce.info/login.json
     Method : GET
1.	Concatenate the username and password with the separator ‘:’ and without space.
2.	Then use a function to encode the string to base64 ASCII String.
3.	Then Append ‘Basic <base64 String>‘ to the encoded string.
4.	Then add a request header with the key ‘Authorization’ and the generated string in the previous step as the value.
5.	Once it is successfully authenticated, the response body has the sessionId.
6.	To access the rest of the API endpoints, set a request header as Cookie and then prepend the string ‘JSESSIONID=’ to the sessionId and set it as value.

Shell
```shell
curl --basic --user username:password "https://v2-0.coalesce.info/login.json"
```
{: codeblock}


Python
```python
import requests, base64

url = "https://v2-0.coalesce.info/login.json"
base64string = base64.encodestring('%s:%s' % (username,password))
req.add_header("Authorization", "Basic %s" % base64string)
req = requests.get(url)
text_response = req.text # read response as Text
print(text_response)

json_response = req.json() # read response as JSON
print(json_response)
```
{: codeblock}

JavaScript
```javascript
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://v2-0.coalesce.info/login.json", true);
xhr.withCredentials = true;
xhr.setRequestHeader("Authorization", 'Basic ' + btoa('username:password'));
xhr.onload = function () {
    console.log(xhr.responseText);
};
xhr.send();
```
{: codeblock}

Java
```java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Base64;


public class HttpBasicAuth {

    public static void main(String[] args) {

        try {
            URL url = new URL ("https://v2-0.coalesce.info/login.json");
            String encoding = Base64.getEncoder().encodeToString(("username:password").getBytes("UTF-8"));

            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
            connection.setDoOutput(true);
            connection.setRequestProperty  ("Authorization", "Basic " + encoding);
            InputStream content = (InputStream)connection.getInputStream();
            BufferedReader in = new BufferedReader (new InputStreamReader (content));
            String line;
            while ((line = in.readLine()) != null) {
                System.out.println(line);
            }
        } catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```
{: codeblock}

## Entites

`GET https://pg.coalesce.info/entities`

By default this request will return the first 1000 entities.

Shell
```shell
curl --cookie JSESSIONID=XXXXsessionIdXXXXX "https://v2-0.coalesce.info/entities"
```
{: codeblock}

Python
```python
import requests

url = "https://v2-0.coalesce.info/entities"
req.add_header("cookie", "JSESSIONID=XXXXsessionIdXXXXX")
req = requests.get(url)
text_response = req.text # read response as Text
print(text_response)

json_response = req.json() # read response as JSON
print(json_response)
```
{: codeblock}

JavaScript
```javascript
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://v2-0.coalesce.info/entities", true);
xhr.withCredentials = true;
xhr.setRequestHeader("cookie", "JSESSIONID=XXXXsessionIdXXXXX");
xhr.onload = function () {
    console.log(xhr.responseText);
};
xhr.send();
```
{: codeblock}

Java
```java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Base64;


public class HttpBasicAuth {

    public static void main(String[] args) {

        try {
            URL url = new URL ("https://v2-0.coalesce.info/entities");
          
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
            connection.setDoOutput(true);
            connection.setRequestProperty  ("cookie", "JSESSIONID=XXXXsessionIdXXXXX");
            InputStream content = (InputStream)connection.getInputStream();
            BufferedReader in = new BufferedReader (new InputStreamReader (content));
            String line;
            while ((line = in.readLine()) != null) {
                System.out.println(line);
            }
        } catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```
{: codeblock}


> The above url returns the most recent 100 documents.

JSON Format
```json
[
  {
    "id": 1,
    "name": "SNaveos",
    "website": "www.naveosdata.com",
    "owner": "JW Demo",
    "country": "United States of America",
    "descriptions": "SNaveos, is a United States-based company engaged in providing platforms for team communication. The Company's Slack is the communication platform, which can sync between the desktop, iPhone, iPad or Android device. The Company's read-state synchronization allows users to read something on phone, which the user's laptop would mark those messages as read. It reflects action in one device across all connected devices. Slack notifies a user of new activity on their mobile, desktop or via e-mail. It allows users to add comments for feedback and stars, and offers built-in internal and external sharing. It also features search, filters and sorting, file drag and drop, and pasting of images into Slack from one's clipboard. It allows users to create open channels for the projects, groups and topics that the whole team shares. The channels include messages, files and comments, inline images and video, rich link summaries and integration with various Web services.",
    "sector": "Information Technology",
    "status": "Portfolio Company",
    "customId": "0017126318DB530204A9698F4D2DCF1D",
    "aliasName": "snaveos",
    "isActive": true,
    "createdBy": "demo",
    "createdTime": "2017-01-24 11:46:58"
  },
  {
    "id": 2,
    "name": "LTN Global Communications",
    "website": "http://www.ltnglobal.com",
    "owner": "JW Demo",
    "country": "China",
    "descriptions": "LTN Global Communications is a high-tech company. The Company has one main product, named Shinewonder cluster management system. It provides efficient collaborative rendering task for movies or cartoons, and also offers service of visual customization requirements for different types companies.",
    "sector": "Information Technology",
    "status": "Portfolio Company",
    "customId": "0BCD91B542E70FBC9117DA001D1E4005",
    "aliasName": "ltn global communications",
    "isActive": true,
    "createdBy": "demo",
    "createdTime": "2017-01-24 11:46:58"
  }
]
```
{: codeblock}

## Filtering

Parameter | Description
-----------| ------------
start	     | Filters entities by the index.
count      | Number of entities to be returned to a maximum of 1000 count.
active     | Filters documents by active flag.

### Filter by start, count, active

Shell
```shell
curl --cookie JSESSIONID=XXXXsessionIdXXXXX "https://v2-0.coalesce.info/entities?start=200&count=100&active=true"
```
{: codeblock}

Python
```python
import requests

url = "https://v2-0.coalesce.info/entities?start=200&count=100&active=true"
req.add_header("cookie", "JSESSIONID=XXXXsessionIdXXXXX")
req = requests.get(url)
text_response = req.text # read response as Text
print(text_response)

json_response = req.json() # read response as JSON
print(json_response)
```
{: codeblock}

JavaScript
```javascript
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://v2-0.coalesce.info/entities?start=200&count=100&active=true", true);
xhr.withCredentials = true;
xhr.setRequestHeader("cookie", "JSESSIONID=XXXXsessionIdXXXXX");
xhr.onload = function () {
    console.log(xhr.responseText);
};
xhr.send();
```
{: codeblock}

Java
```java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Base64;


public class HttpBasicAuth {

    public static void main(String[] args) {

        try {
            URL url = new URL ("https://v2-0.coalesce.info/entities?start=200&count=100&active=true");
          
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");
            connection.setDoOutput(true);
            connection.setRequestProperty  ("cookie", "JSESSIONID=XXXXsessionIdXXXXX");
            InputStream content = (InputStream)connection.getInputStream();
            BufferedReader in = new BufferedReader (new InputStreamReader (content));
            String line;
            while ((line = in.readLine()) != null) {
                System.out.println(line);
            }
        } catch(Exception e) {
            e.printStackTrace();
        }
    }
}
```
{: codeblock}

By default the response from the API feed is in JSON format. 

<!--  Moved Related links to toc file:
# Related Links
{: #rellinks notoc}

### Api Reference
{: #api} 

* [Overview of the Coalesce API](https://v2-0.coalesce.info/swagger-ui.html){:new_window}

-->

