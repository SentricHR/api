## Overview

Here you will find information on how to integrate with and use the SentricHR API. We've tried to make this documentation user-friendly and example-filled, but please drop us a line with any questions. The SentricHR API uses standard HTTP verbs to communicate and HTTP response codes to indicate status and errors. All requests and responses are standard JSON unless otherwise indicated. The SentricHR API is served over HTTPS to ensure data privacy; HTTP is not supported. Every request must include your authentication token.

## Gaining Access

To gain access to the SentricHR API, you will need to contact your CSR. You will be provided with a token that you can use to authenticate. API permissions are opt-in, in other words, no permissions are granted by default. Permissions must be granted by a CSR for each individual resource you want to access. Permissions allow either readonly of full access to each resource. It is suggested that you request the least permissive access you require. You can also create multiple tokens with different levels of access if desired.

## Response Status

We use standard HTTP response codes for success and failure notifications, and our errors are further classified by block. In general, 200 HTTP codes respond to success, 40X codes are for client-related failures, and 50X codes are for SentricHR-related issues. We're doing our best to maximize the former and diminish the latter; however, if you have any issues, please contact your CSR immediately.

Typically the status text will contain details about the error. For example if you are trying to return candidates but do not have sufficient permissions, the status text will indicate this and tell you what exactly you don't have access to. You can then contact your CSR to set up the proper permissions.

```
HTTP/1.1 403 You don't have permission to read ApiCandidates.
```

Another example is a malformed request. 

```
HTTP/1.1 400 Unable to parse json: The token '"' was expected but found '\'.
```

And a request that fails validation.

```
HTTP/1.1 400 'First Name' should not be empty. 'Last Name' should not be empty.
```

## Example

Lets take a look at a typical request and response. The request must contain the `authorization` header with the `Token` scheme and your API token. It must also include the `accept` header indicating JSON should be returned.

```
GET /api/candidates?count=2 HTTP/1.1
Host: urco.sentrichr.com
Authorization: Token WW91ciBtb3RoZXIgd2FzIGEgaGFtc3RlciBhbmQgeW91ciBmYXRoZXIgc21lbHQgb2YgZWxkZXJiZXJyaWVz
Accept: application/json
```
If successful, the server will respond with the data you requested.

```
HTTP/1.1 200 OK
Content-Type: application/json
Date: Thu, 08 Sep 2016 20:34:12 GMT
Content-Length: 2569
...

[
  {
    "id": "1ed259e6-a222-4d41-ab76-0779cf5e3e75",
    "applicantId": "e037fa974a904dd0abff25bc",
    "lastName": "4cb88db38bfd475cb1912051e08da9",
    ...
```

## Libraries

We have provided a library to make it easier to interact with our API on your platform. This library is published in the following registry below:

[![Nuget](https://raw.githubusercontent.com/SentricHR/api/master/nuget.png)](https://www.nuget.org/packages/SentricWorkforce/)

If you would like to see a library for your platform please let us know.
