---
title: Checkly API
language_tabs:
  - shell: curl
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<h1 id="checkly-api">Checkly API V1</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Checkly public API

Base URLs:

* <a href="http://localhost:3000/">http://localhost:3000/</a>

# Authentication

The Checkly API uses API keys to authenticate requests. You can manage your API keys in the
[Checkly account settings](https://app/checklyhq.com/account/api-keys). Your API key is like a password: keep it secure!

Authentication to the API is performed using the bearer auth method in the Authorization header.

For example, use `-H "Authorization: Bearer <API_KEY>"` when using cURL.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail.
API requests without authentication will also fail.

<h1 id="checkly-api-check-results">Check results</h1>

## Lists all check results

<a id="opIdgetV1CheckresultsCheckid"></a>

> Code samples

```shell
curl -X GET http://localhost:3000/v1/check-results/{checkId} \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`GET /v1/check-results/{checkId}`

Lists the full, raw check results for a specific check. You can filter by check type and result type to narrowdown the list. Use the `to` and `from` parameters to specify a date range. Depending on the check type, some fields might be null.

<h3 id="lists-all-check-results-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|checkId<br><div class="requiredParam">(required)</div>|path|string|none|
|limit|query|number|none|
|page|query|number|none|
|location|query|string|Provide a data center location, e.g. "eu-west-1" to filter by location|
|to|query|number|Select results up to this UNIX timestamp date, i.e. < date|
|from|query|number|Select results from this UNIX timestamp date, i.e. >= date|
|checkType|query|string|The type of the check|
|hasFailures|query|boolean|Check result has one or more failures|

#### Enumerated Values

|Parameter|Value|
|---|---|
|checkType|BROWSER|
|checkType|API|

> Example responses

> 200 Response

```json
[
  {
    "id": "string",
    "name": "string",
    "checkId": "string",
    "hasFailures": true,
    "hasErrors": true,
    "runLocation": "string",
    "startedAt": "2019-04-12",
    "stoppedAt": "2019-04-12",
    "created_at": "2019-04-12",
    "responseTime": 0,
    "apiCheckResult": {},
    "browserCheckResult": {},
    "checkRunId": 0,
    "attempts": 0
  }
]
```

<h3 id="lists-all-check-results-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[CheckResultsList](#schemacheckresultslist)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Retrieve a check result

<a id="opIdgetV1CheckresultsCheckidCheckresultid"></a>

> Code samples

```shell
curl -X GET http://localhost:3000/v1/check-results/{checkId}/{checkResultId} \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`GET /v1/check-results/{checkId}/{checkResultId}`

Show details of a specific check result.

<h3 id="retrieve-a-check-result-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|checkId<br><div class="requiredParam">(required)</div>|path|string|none|
|checkResultId<br><div class="requiredParam">(required)</div>|path|string|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "name": "string",
  "checkId": "string",
  "hasFailures": true,
  "hasErrors": true,
  "runLocation": "string",
  "startedAt": "2019-04-12",
  "stoppedAt": "2019-04-12",
  "created_at": "2019-04-12",
  "responseTime": 0,
  "apiCheckResult": {},
  "browserCheckResult": {},
  "checkRunId": 0,
  "attempts": 0
}
```

<h3 id="retrieve-a-check-result-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[CheckResult](#schemacheckresult)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

<h1 id="checkly-api-check-status">Check status</h1>

## List all check statuses

<a id="opIdgetV1Checkstatuses"></a>

> Code samples

```shell
curl -X GET http://localhost:3000/v1/check-statuses \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`GET /v1/check-statuses`

Shows the current status information for all checks in your account. The check status records are continuously updatedas new check results come in.

<h3 id="list-all-check-statuses-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|

> Example responses

> 200 Response

```json
[
  {
    "checkId": "string",
    "hasFailures": true,
    "hasErrors": true,
    "longestRun": 0,
    "shortestRun": 0,
    "lastRunLocation": "string",
    "lastCheckRunId": "string",
    "sslDaysRemaining": 0,
    "created_at": "2019-04-12",
    "updated_at": "2019-04-12"
  }
]
```

<h3 id="list-all-check-statuses-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[CheckStatusList](#schemacheckstatuslist)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Retrieve check status details

<a id="opIdgetV1CheckstatusesCheckid"></a>

> Code samples

```shell
curl -X GET http://localhost:3000/v1/check-statuses/{checkId} \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`GET /v1/check-statuses/{checkId}`

Show the current status information for a specific check.

<h3 id="retrieve-check-status-details-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|checkId<br><div class="requiredParam">(required)</div>|path|string|none|

> Example responses

> 200 Response

```json
{
  "checkId": "string",
  "hasFailures": true,
  "hasErrors": true,
  "longestRun": 0,
  "shortestRun": 0,
  "lastRunLocation": "string",
  "lastCheckRunId": "string",
  "sslDaysRemaining": 0,
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}
```

<h3 id="retrieve-check-status-details-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[CheckStatus](#schemacheckstatus)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

<h1 id="checkly-api-checks">Checks</h1>

## List all checks

<a id="opIdgetV1Checks"></a>

> Code samples

```shell
curl -X GET http://localhost:3000/v1/checks \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`GET /v1/checks`

Lists all current checks in your account.

<h3 id="list-all-checks-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|limit|query|number|none|
|page|query|number|none|

> Example responses

> 200 Response

```json
[
  {
    "id": "string",
    "name": "string",
    "checkType": "BROWSER",
    "frequency": 0,
    "activated": true,
    "muted": false,
    "doubleCheck": true,
    "sslCheck": true,
    "sslCheckDomain": "string",
    "shouldFail": true,
    "locations": [
      "string"
    ],
    "request": {
      "method": "GET",
      "url": "localhost",
      "followRedirects": true,
      "body": "string",
      "bodyType": "JSON",
      "headers": [
        {
          "key": "string",
          "value": "",
          "locked": false
        }
      ],
      "queryParameters": [
        {
          "key": "string",
          "value": "",
          "locked": false
        }
      ],
      "assertions": [
        "string"
      ],
      "basicAuth": {
        "username": "",
        "password": ""
      }
    },
    "script": "string",
    "environmentVariables": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "tags": [
      "string"
    ],
    "setupSnippetId": 0,
    "tearDownSnippetId": 0,
    "localSetupScript": "string",
    "localTearDownScript": "string",
    "alertSettings": {
      "escalationType": "RUN_BASED",
      "runBasedEscalation": {
        "failedRunThreshold": 1
      },
      "timeBasedEscalation": {
        "minutesFailingThreshold": 5
      },
      "reminders": {
        "amount": 0,
        "interval": 5
      },
      "sslCertificates": {
        "enabled": true,
        "alertThreshold": 3
      }
    },
    "useGlobalAlertSettings": true,
    "created_at": "2019-04-12",
    "updated_at": "2019-04-12"
  }
]
```

<h3 id="list-all-checks-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[CheckList](#schemachecklist)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Create a check

<a id="opIdpostV1Checks"></a>

> Code samples

```shell
curl -X POST http://localhost:3000/v1/checks \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`POST /v1/checks`

Creates a new API or browser check. Will return a `402` when you are over the limit of your plan.

> Body parameter

```json
{
  "name": "string",
  "checkType": "BROWSER",
  "frequency": 0,
  "activated": true,
  "muted": false,
  "doubleCheck": true,
  "sslCheck": true,
  "sslCheckDomain": "string",
  "shouldFail": true,
  "locations": [
    "string"
  ],
  "request": {
    "method": "GET",
    "url": "localhost",
    "followRedirects": true,
    "body": "string",
    "bodyType": "JSON",
    "headers": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "queryParameters": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "assertions": [
      "string"
    ],
    "basicAuth": {
      "username": "",
      "password": ""
    }
  },
  "script": "string",
  "environmentVariables": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "alertChannels": {
    "email": [
      {
        "address": ""
      }
    ],
    "webhook": [
      {
        "name": "",
        "url": ""
      }
    ],
    "slack": [
      {
        "url": ""
      }
    ],
    "sms": [
      {
        "number": "",
        "name": "string"
      }
    ]
  },
  "tags": [
    "string"
  ],
  "setupSnippetId": 0,
  "tearDownSnippetId": 0,
  "localSetupScript": "string",
  "localTearDownScript": "string",
  "alertSettings": {
    "escalationType": "RUN_BASED",
    "runBasedEscalation": {
      "failedRunThreshold": 1
    },
    "timeBasedEscalation": {
      "minutesFailingThreshold": 5
    },
    "reminders": {
      "amount": 0,
      "interval": 5
    },
    "sslCertificates": {
      "enabled": true,
      "alertThreshold": 3
    }
  },
  "useGlobalAlertSettings": true
}
```

<h3 id="create-a-check-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|body|body|[CheckCreate](#schemacheckcreate)|none|

> Example responses

> 201 Response

```json
{
  "id": "string",
  "name": "string",
  "checkType": "BROWSER",
  "frequency": 0,
  "activated": true,
  "muted": false,
  "doubleCheck": true,
  "sslCheck": true,
  "sslCheckDomain": "string",
  "shouldFail": true,
  "locations": [
    "string"
  ],
  "request": {
    "method": "GET",
    "url": "localhost",
    "followRedirects": true,
    "body": "string",
    "bodyType": "JSON",
    "headers": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "queryParameters": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "assertions": [
      "string"
    ],
    "basicAuth": {
      "username": "",
      "password": ""
    }
  },
  "script": "string",
  "environmentVariables": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "tags": [
    "string"
  ],
  "setupSnippetId": 0,
  "tearDownSnippetId": 0,
  "localSetupScript": "string",
  "localTearDownScript": "string",
  "alertSettings": {
    "escalationType": "RUN_BASED",
    "runBasedEscalation": {
      "failedRunThreshold": 1
    },
    "timeBasedEscalation": {
      "minutesFailingThreshold": 5
    },
    "reminders": {
      "amount": 0,
      "interval": 5
    },
    "sslCertificates": {
      "enabled": true,
      "alertThreshold": 3
    }
  },
  "useGlobalAlertSettings": true,
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}
```

<h3 id="create-a-check-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[Check](#schemacheck)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|402|[Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2)|Payment Required|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Delete a check

<a id="opIddeleteV1ChecksId"></a>

> Code samples

```shell
curl -X DELETE http://localhost:3000/v1/checks/{id} \
 -H 'Accept: application/json' \
 -H 'Authorization: Bearer API_KEY'

```

`DELETE /v1/checks/{id}`

Permanently removes a API or browser check and all its related status and results data.

<h3 id="delete-a-check-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|id<br><div class="requiredParam">(required)</div>|path|string|none|

> Example responses

> 204 Response

```json
"string"
```

<h3 id="delete-a-check-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content|string|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Retrieve a check

<a id="opIdgetV1ChecksId"></a>

> Code samples

```shell
curl -X GET http://localhost:3000/v1/checks/{id} \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`GET /v1/checks/{id}`

Show details of a specific API or browser check

<h3 id="retrieve-a-check-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|id<br><div class="requiredParam">(required)</div>|path|string|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "name": "string",
  "checkType": "BROWSER",
  "frequency": 0,
  "activated": true,
  "muted": false,
  "doubleCheck": true,
  "sslCheck": true,
  "sslCheckDomain": "string",
  "shouldFail": true,
  "locations": [
    "string"
  ],
  "request": {
    "method": "GET",
    "url": "localhost",
    "followRedirects": true,
    "body": "string",
    "bodyType": "JSON",
    "headers": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "queryParameters": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "assertions": [
      "string"
    ],
    "basicAuth": {
      "username": "",
      "password": ""
    }
  },
  "script": "string",
  "environmentVariables": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "tags": [
    "string"
  ],
  "setupSnippetId": 0,
  "tearDownSnippetId": 0,
  "localSetupScript": "string",
  "localTearDownScript": "string",
  "alertSettings": {
    "escalationType": "RUN_BASED",
    "runBasedEscalation": {
      "failedRunThreshold": 1
    },
    "timeBasedEscalation": {
      "minutesFailingThreshold": 5
    },
    "reminders": {
      "amount": 0,
      "interval": 5
    },
    "sslCertificates": {
      "enabled": true,
      "alertThreshold": 3
    }
  },
  "useGlobalAlertSettings": true,
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}
```

<h3 id="retrieve-a-check-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[Check](#schemacheck)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Update a check

<a id="opIdputV1ChecksId"></a>

> Code samples

```shell
curl -X PUT http://localhost:3000/v1/checks/{id} \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`PUT /v1/checks/{id}`

Updates a new API or browser check.

> Body parameter

```json
{
  "name": "string",
  "checkType": "BROWSER",
  "frequency": 0,
  "activated": true,
  "muted": false,
  "doubleCheck": true,
  "sslCheck": true,
  "sslCheckDomain": "string",
  "shouldFail": true,
  "locations": [
    "string"
  ],
  "request": {
    "method": "GET",
    "url": "localhost",
    "followRedirects": true,
    "body": "string",
    "bodyType": "JSON",
    "headers": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "queryParameters": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "assertions": [
      "string"
    ],
    "basicAuth": {
      "username": "",
      "password": ""
    }
  },
  "script": "string",
  "environmentVariables": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "alertChannels": {
    "email": [
      {
        "address": ""
      }
    ],
    "webhook": [
      {
        "name": "",
        "url": ""
      }
    ],
    "slack": [
      {
        "url": ""
      }
    ],
    "sms": [
      {
        "number": "",
        "name": "string"
      }
    ]
  },
  "tags": [
    "string"
  ],
  "setupSnippetId": 0,
  "tearDownSnippetId": 0,
  "localSetupScript": "string",
  "localTearDownScript": "string",
  "alertSettings": {
    "escalationType": "RUN_BASED",
    "runBasedEscalation": {
      "failedRunThreshold": 1
    },
    "timeBasedEscalation": {
      "minutesFailingThreshold": 5
    },
    "reminders": {
      "amount": 0,
      "interval": 5
    },
    "sslCertificates": {
      "enabled": true,
      "alertThreshold": 3
    }
  },
  "useGlobalAlertSettings": true
}
```

<h3 id="update-a-check-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|id<br><div class="requiredParam">(required)</div>|path|string|none|
|body|body|[CheckCreate](#schemacheckcreate)|none|

> Example responses

> 200 Response

```json
{
  "id": "string",
  "name": "string",
  "checkType": "BROWSER",
  "frequency": 0,
  "activated": true,
  "muted": false,
  "doubleCheck": true,
  "sslCheck": true,
  "sslCheckDomain": "string",
  "shouldFail": true,
  "locations": [
    "string"
  ],
  "request": {
    "method": "GET",
    "url": "localhost",
    "followRedirects": true,
    "body": "string",
    "bodyType": "JSON",
    "headers": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "queryParameters": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "assertions": [
      "string"
    ],
    "basicAuth": {
      "username": "",
      "password": ""
    }
  },
  "script": "string",
  "environmentVariables": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "tags": [
    "string"
  ],
  "setupSnippetId": 0,
  "tearDownSnippetId": 0,
  "localSetupScript": "string",
  "localTearDownScript": "string",
  "alertSettings": {
    "escalationType": "RUN_BASED",
    "runBasedEscalation": {
      "failedRunThreshold": 1
    },
    "timeBasedEscalation": {
      "minutesFailingThreshold": 5
    },
    "reminders": {
      "amount": 0,
      "interval": 5
    },
    "sslCertificates": {
      "enabled": true,
      "alertThreshold": 3
    }
  },
  "useGlobalAlertSettings": true,
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}
```

<h3 id="update-a-check-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[Check](#schemacheck)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

<h1 id="checkly-api-snippets">Snippets</h1>

## List all snippets

<a id="opIdgetV1Snippets"></a>

> Code samples

```shell
curl -X GET http://localhost:3000/v1/snippets \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`GET /v1/snippets`

Lists all current snippets in your account.

<h3 id="list-all-snippets-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|limit|query|number|none|
|page|query|number|none|

> Example responses

> 200 Response

```json
[
  {
    "id": 0,
    "name": "string",
    "script": "string",
    "created_at": "2019-04-12",
    "updated_at": "2019-04-12"
  }
]
```

<h3 id="list-all-snippets-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[SnippetsList](#schemasnippetslist)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Create a snippet

<a id="opIdpostV1Snippets"></a>

> Code samples

```shell
curl -X POST http://localhost:3000/v1/snippets \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`POST /v1/snippets`

Creates a new snippet.

> Body parameter

```json
{
  "name": "string",
  "script": "string"
}
```

<h3 id="create-a-snippet-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|body|body|[SnippetCreate](#schemasnippetcreate)|none|

> Example responses

> 201 Response

```json
{
  "id": 0,
  "name": "string",
  "script": "string",
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}
```

<h3 id="create-a-snippet-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|[Snippet](#schemasnippet)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Delete a snippet

<a id="opIddeleteV1SnippetsId"></a>

> Code samples

```shell
curl -X DELETE http://localhost:3000/v1/snippets/{id} \
 -H 'Accept: application/json' \
 -H 'Authorization: Bearer API_KEY'

```

`DELETE /v1/snippets/{id}`

Permanently removes a snippet.

<h3 id="delete-a-snippet-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|id<br><div class="requiredParam">(required)</div>|path|number|none|

> Example responses

> 204 Response

```json
"string"
```

<h3 id="delete-a-snippet-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|204|[No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)|No Content|string|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Retrieve a snippet

<a id="opIdgetV1SnippetsId"></a>

> Code samples

```shell
curl -X GET http://localhost:3000/v1/snippets/{id} \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`GET /v1/snippets/{id}`

Show details of a specific snippet.

<h3 id="retrieve-a-snippet-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|id<br><div class="requiredParam">(required)</div>|path|number|none|

> Example responses

> 200 Response

```json
{
  "id": 0,
  "name": "string",
  "script": "string",
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}
```

<h3 id="retrieve-a-snippet-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[Snippet](#schemasnippet)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

## Update a snippet

<a id="opIdputV1SnippetsId"></a>

> Code samples

```shell
curl -X PUT http://localhost:3000/v1/snippets/{id} \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -H 'authorization: string' \
 -H 'Authorization: Bearer API_KEY'

```

`PUT /v1/snippets/{id}`

Updates a snippet.

> Body parameter

```json
{
  "name": "string",
  "script": "string"
}
```

<h3 id="update-a-snippet-parameters">Parameters</h3>

|Name|In|Type|Description|
|---|---|---|---|---|
|authorization<br><div class="requiredParam">(required)</div>|header|string|none|
|id<br><div class="requiredParam">(required)</div>|path|number|none|
|body|body|[SnippetCreate](#schemasnippetcreate)|none|

> Example responses

> 200 Response

```json
{
  "id": 0,
  "name": "string",
  "script": "string",
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}
```

<h3 id="update-a-snippet-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successful|[Snippet](#schemasnippet)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Not Found|string|

# Schemas

<h2 id="tocSapicheckresult">apiCheckResult</h2>

<a id="schemaapicheckresult"></a>

```json
{}

```

### Properties

*None*

<h2 id="tocSbrowsercheckresult">browserCheckResult</h2>

<a id="schemabrowsercheckresult"></a>

```json
{}

```

### Properties

*None*

<h2 id="tocScheckresult">CheckResult</h2>

<a id="schemacheckresult"></a>

```json
{
  "id": "string",
  "name": "string",
  "checkId": "string",
  "hasFailures": true,
  "hasErrors": true,
  "runLocation": "string",
  "startedAt": "2019-04-12",
  "stoppedAt": "2019-04-12",
  "created_at": "2019-04-12",
  "responseTime": 0,
  "apiCheckResult": {},
  "browserCheckResult": {},
  "checkRunId": 0,
  "attempts": 0
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|id|string|The unique ID of this result|
|name|string|The name of the check|
|checkId|string|The ID of the check|
|hasFailures|boolean|Describes if any failure has occurred during this check run. This is should be your mainmain focus for assessing API or browser check behaviour. Assertions that fail, timeouts or failing scripts all resolve tothis value being true|
|hasErrors|boolean|Describes if an internal error has occured in Checkly's backend. This should be false in almost all cases.|
|runLocation|string|What datacenter location this check result originated from|
|startedAt|string(date)|none|
|stoppedAt|string(date)|none|
|created_at|string(date)|none|
|responseTime|number|Describes the time it took to execute relevant parts of this check. Any setup timeor system time needed to start executing this check in the Checkly backend is not part of this.|
|apiCheckResult|[apiCheckResult](#schemaapicheckresult)|none|
|browserCheckResult|[browserCheckResult](#schemabrowsercheckresult)|none|
|checkRunId|number|The id of the specific check run that created this check result|
|attempts|number|How often this check was retried. This will be larger than 0 when double checking is enabled|

<h2 id="tocScheckresultslist">CheckResultsList</h2>

<a id="schemacheckresultslist"></a>

```json
[
  {
    "id": "string",
    "name": "string",
    "checkId": "string",
    "hasFailures": true,
    "hasErrors": true,
    "runLocation": "string",
    "startedAt": "2019-04-12",
    "stoppedAt": "2019-04-12",
    "created_at": "2019-04-12",
    "responseTime": 0,
    "apiCheckResult": {},
    "browserCheckResult": {},
    "checkRunId": 0,
    "attempts": 0
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[CheckResult](#schemacheckresult)]|none|

<h2 id="tocScheckstatus">CheckStatus</h2>

<a id="schemacheckstatus"></a>

```json
{
  "checkId": "string",
  "hasFailures": true,
  "hasErrors": true,
  "longestRun": 0,
  "shortestRun": 0,
  "lastRunLocation": "string",
  "lastCheckRunId": "string",
  "sslDaysRemaining": 0,
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|checkId|string|The ID of check this status belongs to|
|hasFailures|boolean|Describes if this check is currently failing. If any of the assertions for an API checkfail this value is true. If a browser check fails for whatever reason, this is true|
|hasErrors|boolean|Describes if due to some error outside of normal operation this check is failing. This should be extremely rare and only when there is an error in the Checkly backend|
|longestRun|number|The longest ever recorded response time for this check|
|shortestRun|number|The shortest ever recorded response time for this check|
|lastRunLocation|string|What location this check was last run at|
|lastCheckRunId|string|The unique incrementing ID for each check run|
|sslDaysRemaining|number|How many days remain till the current SSL certifacte expires|
|created_at|string(date)|none|
|updated_at|string(date)|none|

<h2 id="tocScheckstatuslist">CheckStatusList</h2>

<a id="schemacheckstatuslist"></a>

```json
[
  {
    "checkId": "string",
    "hasFailures": true,
    "hasErrors": true,
    "longestRun": 0,
    "shortestRun": 0,
    "lastRunLocation": "string",
    "lastCheckRunId": "string",
    "sslDaysRemaining": 0,
    "created_at": "2019-04-12",
    "updated_at": "2019-04-12"
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[CheckStatus](#schemacheckstatus)]|none|

<h2 id="tocSlocations">Locations</h2>

<a id="schemalocations"></a>

```json
[
  "string"
]

```

*An array of one or more data center locations where to run the this check*

### Properties

*None*

<h2 id="tocSkeyvalue">KeyValue</h2>

<a id="schemakeyvalue"></a>

```json
{
  "key": "string",
  "value": "",
  "locked": false
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|key<div class="requiredParam">(required)</div>|string|none|
|value<div class="requiredParam">(required)</div>|string|none|
|locked|boolean|none|

<h2 id="tocSheaders">Headers</h2>

<a id="schemaheaders"></a>

```json
[
  {
    "key": "string",
    "value": "",
    "locked": false
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[KeyValue](#schemakeyvalue)]|none|

<h2 id="tocSqueryparameters">QueryParameters</h2>

<a id="schemaqueryparameters"></a>

```json
[
  {
    "key": "string",
    "value": "",
    "locked": false
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[KeyValue](#schemakeyvalue)]|none|

<h2 id="tocSassertions">assertions</h2>

<a id="schemaassertions"></a>

```json
[
  "string"
]

```

### Properties

*None*

<h2 id="tocSbasicauth">basicAuth</h2>

<a id="schemabasicauth"></a>

```json
{
  "username": "",
  "password": ""
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|username|string|none|
|password|string|none|

<h2 id="tocSrequest">Request</h2>

<a id="schemarequest"></a>

```json
{
  "method": "GET",
  "url": "localhost",
  "followRedirects": true,
  "body": "string",
  "bodyType": "JSON",
  "headers": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "queryParameters": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "assertions": [
    "string"
  ],
  "basicAuth": {
    "username": "",
    "password": ""
  }
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|method<div class="requiredParam">(required)</div>|string|none|
|url<div class="requiredParam">(required)</div>|string|none|
|followRedirects|boolean|none|
|body|string|none|
|bodyType|string|none|
|headers|[Headers](#schemaheaders)|none|
|queryParameters|[QueryParameters](#schemaqueryparameters)|none|
|assertions|[assertions](#schemaassertions)|none|
|basicAuth|[basicAuth](#schemabasicauth)|none|

#### Enumerated Values

|Property|Value|
|---|---|
|method|GET|
|method|POST|
|method|PUT|
|method|HEAD|
|method|DELETE|
|method|PATCH|
|bodyType|JSON|
|bodyType|FORM|
|bodyType|RAW|

<h2 id="tocSenvironmentvariable">EnvironmentVariable</h2>

<a id="schemaenvironmentvariable"></a>

```json
{
  "key": "string",
  "value": "",
  "locked": false
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|key<div class="requiredParam">(required)</div>|string|none|
|value<div class="requiredParam">(required)</div>|string|none|
|locked|boolean|Used only in the UI to hide the value like a password|

<h2 id="tocSenvironmentvariables">EnvironmentVariables</h2>

<a id="schemaenvironmentvariables"></a>

```json
[
  {
    "key": "string",
    "value": "",
    "locked": false
  }
]

```

*Key/value pairs for setting environment variables during check execution*

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[EnvironmentVariable](#schemaenvironmentvariable)]|Key/value pairs for setting environment variables during check execution|

<h2 id="tocStags">Tags</h2>

<a id="schematags"></a>

```json
[
  "string"
]

```

*Tags for organizing and filtering checks*

### Properties

*None*

<h2 id="tocSrunbasedescalation">runBasedEscalation</h2>

<a id="schemarunbasedescalation"></a>

```json
{
  "failedRunThreshold": 1
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|failedRunThreshold|number|After how many failed consecutive check runs an alert notification should be send|

#### Enumerated Values

|Property|Value|
|---|---|
|failedRunThreshold|1|
|failedRunThreshold|2|
|failedRunThreshold|3|
|failedRunThreshold|4|
|failedRunThreshold|5|

<h2 id="tocStimebasedescalation">timeBasedEscalation</h2>

<a id="schematimebasedescalation"></a>

```json
{
  "minutesFailingThreshold": 5
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|minutesFailingThreshold|number|After how many minutes after a check starts failing an alert should be send|

#### Enumerated Values

|Property|Value|
|---|---|
|minutesFailingThreshold|5|
|minutesFailingThreshold|10|
|minutesFailingThreshold|15|
|minutesFailingThreshold|30|

<h2 id="tocSreminders">reminders</h2>

<a id="schemareminders"></a>

```json
{
  "amount": 0,
  "interval": 5
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|amount|number|How many reminders to send out after the initial alert notification|
|interval|number|At what interval the reminders should be send|

#### Enumerated Values

|Property|Value|
|---|---|
|amount|0|
|amount|1|
|amount|2|
|amount|3|
|amount|4|
|amount|5|
|interval|5|
|interval|10|
|interval|15|
|interval|30|

<h2 id="tocSsslcertificates">sslCertificates</h2>

<a id="schemasslcertificates"></a>

```json
{
  "enabled": true,
  "alertThreshold": 3
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|enabled|boolean|Determines if alert notifications should be send for expiring SSL certificates|
|alertThreshold|number|At what moment in time to start alerting on SSL certificates|

#### Enumerated Values

|Property|Value|
|---|---|
|alertThreshold|3|
|alertThreshold|7|
|alertThreshold|14|
|alertThreshold|30|

<h2 id="tocSalertsettingsschema">AlertSettingsSchema</h2>

<a id="schemaalertsettingsschema"></a>

```json
{
  "escalationType": "RUN_BASED",
  "runBasedEscalation": {
    "failedRunThreshold": 1
  },
  "timeBasedEscalation": {
    "minutesFailingThreshold": 5
  },
  "reminders": {
    "amount": 0,
    "interval": 5
  },
  "sslCertificates": {
    "enabled": true,
    "alertThreshold": 3
  }
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|escalationType|string|Determines what type of escalation to use|
|runBasedEscalation|[runBasedEscalation](#schemarunbasedescalation)|none|
|timeBasedEscalation|[timeBasedEscalation](#schematimebasedescalation)|none|
|reminders|[reminders](#schemareminders)|none|
|sslCertificates|[sslCertificates](#schemasslcertificates)|none|

#### Enumerated Values

|Property|Value|
|---|---|
|escalationType|RUN_BASED|
|escalationType|TIME_BASED|

<h2 id="tocScheck">Check</h2>

<a id="schemacheck"></a>

```json
{
  "id": "string",
  "name": "string",
  "checkType": "BROWSER",
  "frequency": 0,
  "activated": true,
  "muted": false,
  "doubleCheck": true,
  "sslCheck": true,
  "sslCheckDomain": "string",
  "shouldFail": true,
  "locations": [
    "string"
  ],
  "request": {
    "method": "GET",
    "url": "localhost",
    "followRedirects": true,
    "body": "string",
    "bodyType": "JSON",
    "headers": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "queryParameters": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "assertions": [
      "string"
    ],
    "basicAuth": {
      "username": "",
      "password": ""
    }
  },
  "script": "string",
  "environmentVariables": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "tags": [
    "string"
  ],
  "setupSnippetId": 0,
  "tearDownSnippetId": 0,
  "localSetupScript": "string",
  "localTearDownScript": "string",
  "alertSettings": {
    "escalationType": "RUN_BASED",
    "runBasedEscalation": {
      "failedRunThreshold": 1
    },
    "timeBasedEscalation": {
      "minutesFailingThreshold": 5
    },
    "reminders": {
      "amount": 0,
      "interval": 5
    },
    "sslCertificates": {
      "enabled": true,
      "alertThreshold": 3
    }
  },
  "useGlobalAlertSettings": true,
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|id|string|none|
|name|string|The name of the check|
|checkType|string|The type of the check|
|frequency|number|how often the check should run in minutes|
|activated|boolean|Determines if the check is running or not|
|muted|boolean|Determines if any notifications will be send out when a check fails and/or recovers|
|doubleCheck|boolean|Setting this to "true" will trigger a retry when a check fails from the failing region and another, randomly selected region before marking the check as failed|
|sslCheck|boolean|Determines if the SSL certificate should be validated for expiry|
|sslCheckDomain|string|Provides the domain for the SSLCheck option|
|shouldFail|boolean|Allows to invert the behaviour of when a check is considered to fail. Allows for validating error status like 404|
|locations|[Locations](#schemalocations)|An array of one or more data center locations where to run the this check|
|request|[Request](#schemarequest)|none|
|script|string|A valid piece of Node.js javascript code describing a browser interaction with the Puppeteer framework.|
|environmentVariables|[EnvironmentVariables](#schemaenvironmentvariables)|Key/value pairs for setting environment variables during check execution|
|tags|[Tags](#schematags)|Tags for organizing and filtering checks|
|setupSnippetId|number|An ID reference to a snippet to use in the setup phase of an API check|
|tearDownSnippetId|number|An ID reference to a snippet to use in the teardown phase of an API check|
|localSetupScript|string|A valid piece of Node.js code to run in the setup phase|
|localTearDownScript|string|A valid piece of Node.js code to run in the teardown phase|
|alertSettings|[AlertSettingsSchema](#schemaalertsettingsschema)|none|
|useGlobalAlertSettings|boolean|When true, the account level alert setting will be used, not the alert setting defined on this check|
|created_at|string(date)|none|
|updated_at|string(date)|none|

#### Enumerated Values

|Property|Value|
|---|---|
|checkType|BROWSER|
|checkType|API|

<h2 id="tocSchecklist">CheckList</h2>

<a id="schemachecklist"></a>

```json
[
  {
    "id": "string",
    "name": "string",
    "checkType": "BROWSER",
    "frequency": 0,
    "activated": true,
    "muted": false,
    "doubleCheck": true,
    "sslCheck": true,
    "sslCheckDomain": "string",
    "shouldFail": true,
    "locations": [
      "string"
    ],
    "request": {
      "method": "GET",
      "url": "localhost",
      "followRedirects": true,
      "body": "string",
      "bodyType": "JSON",
      "headers": [
        {
          "key": "string",
          "value": "",
          "locked": false
        }
      ],
      "queryParameters": [
        {
          "key": "string",
          "value": "",
          "locked": false
        }
      ],
      "assertions": [
        "string"
      ],
      "basicAuth": {
        "username": "",
        "password": ""
      }
    },
    "script": "string",
    "environmentVariables": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "tags": [
      "string"
    ],
    "setupSnippetId": 0,
    "tearDownSnippetId": 0,
    "localSetupScript": "string",
    "localTearDownScript": "string",
    "alertSettings": {
      "escalationType": "RUN_BASED",
      "runBasedEscalation": {
        "failedRunThreshold": 1
      },
      "timeBasedEscalation": {
        "minutesFailingThreshold": 5
      },
      "reminders": {
        "amount": 0,
        "interval": 5
      },
      "sslCertificates": {
        "enabled": true,
        "alertThreshold": 3
      }
    },
    "useGlobalAlertSettings": true,
    "created_at": "2019-04-12",
    "updated_at": "2019-04-12"
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[Check](#schemacheck)]|none|

<h2 id="tocSalertemail">AlertEmail</h2>

<a id="schemaalertemail"></a>

```json
{
  "address": ""
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|address<div class="requiredParam">(required)</div>|string|none|

<h2 id="tocSemail">email</h2>

<a id="schemaemail"></a>

```json
[
  {
    "address": ""
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[AlertEmail](#schemaalertemail)]|none|

<h2 id="tocSalertwebhook">AlertWebhook</h2>

<a id="schemaalertwebhook"></a>

```json
{
  "name": "",
  "url": ""
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|name|string|none|
|url<div class="requiredParam">(required)</div>|string|none|

<h2 id="tocSwebhook">webhook</h2>

<a id="schemawebhook"></a>

```json
[
  {
    "name": "",
    "url": ""
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[AlertWebhook](#schemaalertwebhook)]|none|

<h2 id="tocSalertslack">AlertSlack</h2>

<a id="schemaalertslack"></a>

```json
{
  "url": ""
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|url<div class="requiredParam">(required)</div>|string|none|

<h2 id="tocSslack">slack</h2>

<a id="schemaslack"></a>

```json
[
  {
    "url": ""
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[AlertSlack](#schemaalertslack)]|none|

<h2 id="tocSalertsms">AlertSms</h2>

<a id="schemaalertsms"></a>

```json
{
  "number": "",
  "name": "string"
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|number<div class="requiredParam">(required)</div>|string|none|
|name<div class="requiredParam">(required)</div>|string|none|

<h2 id="tocSsms">sms</h2>

<a id="schemasms"></a>

```json
[
  {
    "number": "",
    "name": "string"
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[AlertSms](#schemaalertsms)]|none|

<h2 id="tocSalertchannels">AlertChannels</h2>

<a id="schemaalertchannels"></a>

```json
{
  "email": [
    {
      "address": ""
    }
  ],
  "webhook": [
    {
      "name": "",
      "url": ""
    }
  ],
  "slack": [
    {
      "url": ""
    }
  ],
  "sms": [
    {
      "number": "",
      "name": "string"
    }
  ]
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|email|[email](#schemaemail)|none|
|webhook|[webhook](#schemawebhook)|none|
|slack|[slack](#schemaslack)|none|
|sms|[sms](#schemasms)|none|

<h2 id="tocScheckcreate">CheckCreate</h2>

<a id="schemacheckcreate"></a>

```json
{
  "name": "string",
  "checkType": "BROWSER",
  "frequency": 0,
  "activated": true,
  "muted": false,
  "doubleCheck": true,
  "sslCheck": true,
  "sslCheckDomain": "string",
  "shouldFail": true,
  "locations": [
    "string"
  ],
  "request": {
    "method": "GET",
    "url": "localhost",
    "followRedirects": true,
    "body": "string",
    "bodyType": "JSON",
    "headers": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "queryParameters": [
      {
        "key": "string",
        "value": "",
        "locked": false
      }
    ],
    "assertions": [
      "string"
    ],
    "basicAuth": {
      "username": "",
      "password": ""
    }
  },
  "script": "string",
  "environmentVariables": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "alertChannels": {
    "email": [
      {
        "address": ""
      }
    ],
    "webhook": [
      {
        "name": "",
        "url": ""
      }
    ],
    "slack": [
      {
        "url": ""
      }
    ],
    "sms": [
      {
        "number": "",
        "name": "string"
      }
    ]
  },
  "tags": [
    "string"
  ],
  "setupSnippetId": 0,
  "tearDownSnippetId": 0,
  "localSetupScript": "string",
  "localTearDownScript": "string",
  "alertSettings": {
    "escalationType": "RUN_BASED",
    "runBasedEscalation": {
      "failedRunThreshold": 1
    },
    "timeBasedEscalation": {
      "minutesFailingThreshold": 5
    },
    "reminders": {
      "amount": 0,
      "interval": 5
    },
    "sslCertificates": {
      "enabled": true,
      "alertThreshold": 3
    }
  },
  "useGlobalAlertSettings": true
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|name<div class="requiredParam">(required)</div>|string|The name of the check|
|checkType<div class="requiredParam">(required)</div>|string|The type of the check|
|frequency|number|how often the check should run in minutes|
|activated<div class="requiredParam">(required)</div>|boolean|Determines if the check is running or not|
|muted|boolean|Determines if any notifications will be send out when a check fails and/or recovers|
|doubleCheck|boolean|Setting this to "true" will trigger a retry when a check fails from the failing region and another, randomly selected region before marking the check as failed|
|sslCheck|boolean|Determines if the SSL certificate should be validated for expiry|
|sslCheckDomain|string|Provides the domain for the SSLCheck option|
|shouldFail|boolean|Allows to invert the behaviour of when a check is considered to fail. Allows for validating error status like 404|
|locations|[Locations](#schemalocations)|An array of one or more data center locations where to run the this check|
|request|[Request](#schemarequest)|none|
|script|string|A valid piece of Node.js javascript code describing a browser interaction with the Puppeteer framework.|
|environmentVariables|[EnvironmentVariables](#schemaenvironmentvariables)|Key/value pairs for setting environment variables during check execution|
|alertChannels|[AlertChannels](#schemaalertchannels)|none|
|tags|[Tags](#schematags)|Tags for organizing and filtering checks|
|setupSnippetId|number|An ID reference to a snippet to use in the setup phase of an API check|
|tearDownSnippetId|number|An ID reference to a snippet to use in the teardown phase of an API check|
|localSetupScript|string|A valid piece of Node.js code to run in the setup phase|
|localTearDownScript|string|A valid piece of Node.js code to run in the teardown phase|
|alertSettings|[AlertSettingsSchema](#schemaalertsettingsschema)|none|
|useGlobalAlertSettings|boolean|When true, the account level alert setting will be used, not the alert setting defined on this check|

#### Enumerated Values

|Property|Value|
|---|---|
|checkType|BROWSER|
|checkType|API|

<h2 id="tocSsnippet">Snippet</h2>

<a id="schemasnippet"></a>

```json
{
  "id": 0,
  "name": "string",
  "script": "string",
  "created_at": "2019-04-12",
  "updated_at": "2019-04-12"
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|id|number|none|
|name|string|The snippet name|
|script|string|Your Node.js code that interacts with the API check lifecycle, or functions as a partial for browser checks.|
|created_at|string(date)|none|
|updated_at|string(date)|none|

<h2 id="tocSsnippetslist">SnippetsList</h2>

<a id="schemasnippetslist"></a>

```json
[
  {
    "id": 0,
    "name": "string",
    "script": "string",
    "created_at": "2019-04-12",
    "updated_at": "2019-04-12"
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[Snippet](#schemasnippet)]|none|

<h2 id="tocSsnippetcreate">SnippetCreate</h2>

<a id="schemasnippetcreate"></a>

```json
{
  "name": "string",
  "script": "string"
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|name<div class="requiredParam">(required)</div>|string|The snippet name|
|script<div class="requiredParam">(required)</div>|string|Your Node.js code that interacts with the API check lifecycle, or functions as a partial for browser checks.|

<h2 id="tocSschema1">schema1</h2>

<a id="schemaschema1"></a>

```json
{
  "key": "string",
  "value": "",
  "locked": false
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|key<div class="requiredParam">(required)</div>|string|none|
|value<div class="requiredParam">(required)</div>|string|none|
|locked|boolean|none|

<h2 id="tocSschema2">schema2</h2>

<a id="schemaschema2"></a>

```json
[
  {
    "key": "string",
    "value": "",
    "locked": false
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[schema1](#schemaschema1)]|none|

<h2 id="tocSschema3">schema3</h2>

<a id="schemaschema3"></a>

```json
[
  {
    "key": "string",
    "value": "",
    "locked": false
  }
]

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[schema1](#schemaschema1)]|none|

<h2 id="tocSschema4">schema4</h2>

<a id="schemaschema4"></a>

```json
[
  "string"
]

```

### Properties

*None*

<h2 id="tocSschema5">schema5</h2>

<a id="schemaschema5"></a>

```json
{
  "username": "",
  "password": ""
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|username|string|none|
|password|string|none|

<h2 id="tocSschema6">schema6</h2>

<a id="schemaschema6"></a>

```json
{
  "key": "string",
  "value": "",
  "locked": false
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|key<div class="requiredParam">(required)</div>|string|none|
|value<div class="requiredParam">(required)</div>|string|none|
|locked|boolean|Used only in the UI to hide the value like a password|

<h2 id="tocSschema7">schema7</h2>

<a id="schemaschema7"></a>

```json
{
  "method": "GET",
  "url": "localhost",
  "followRedirects": true,
  "body": "string",
  "bodyType": "JSON",
  "headers": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "queryParameters": [
    {
      "key": "string",
      "value": "",
      "locked": false
    }
  ],
  "assertions": [
    "string"
  ],
  "basicAuth": {
    "username": "",
    "password": ""
  }
}

```

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|method<div class="requiredParam">(required)</div>|string|none|
|url<div class="requiredParam">(required)</div>|string|none|
|followRedirects|boolean|none|
|body|string|none|
|bodyType|string|none|
|headers|[schema2](#schemaschema2)|none|
|queryParameters|[schema3](#schemaschema3)|none|
|assertions|[schema4](#schemaschema4)|none|
|basicAuth|[schema5](#schemaschema5)|none|

#### Enumerated Values

|Property|Value|
|---|---|
|method|GET|
|method|POST|
|method|PUT|
|method|HEAD|
|method|DELETE|
|method|PATCH|
|bodyType|JSON|
|bodyType|FORM|
|bodyType|RAW|

<h2 id="tocSschema8">schema8</h2>

<a id="schemaschema8"></a>

```json
{}

```

### Properties

*None*

<h2 id="tocSschema9">schema9</h2>

<a id="schemaschema9"></a>

```json
[
  {
    "key": "string",
    "value": "",
    "locked": false
  }
]

```

*Key/value pairs for setting environment variables during check execution*

### Properties

|Name|Type|Description|
|---|---|---|---|---|
|*anonymous*|[[schema6](#schemaschema6)]|Key/value pairs for setting environment variables during check execution|

<h2 id="tocSschema10">schema10</h2>

<a id="schemaschema10"></a>

```json
{}

```

### Properties

*None*

