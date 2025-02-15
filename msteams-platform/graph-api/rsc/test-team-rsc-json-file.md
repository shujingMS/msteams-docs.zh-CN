---
title: 在 Teams 中测试用于团队的资源特定许可
description: 在本模块中，了解如何在使用 Postman 和示例 JSON 文件Teams测试团队的特定于资源的许可。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: how-to
ms.openlocfilehash: 9688d4d2f4bf56a0c5c4fa41b7b5263d864bbd2f
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144066"
---
# <a name="test-team-rsc-postman-collection-json"></a>测试团队 RSC Postman 集合 JSON

```json
{
 "info": {
  "_postman_id": "57dc5f09-d719-4d48-a50d-6b09053cc7a7",
  "name": "Test-RSC",
  "description": "Collection to test RSC.",
  "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
 },
 "item": [
  {
   "name": "Create App Context Token",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "1e0d2bb5-8d0d-47a1-a42e-fcd8d58bb8a3",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(200);\r",
       "\r",
       "    // Set the app_context access token\r",
       "    const { access_token } = pm.response.json();\r",
       "    pm.environment.set(\"appContextToken\", access_token);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "POST",
    "header": [
     {
      "key": "Content-Type",
      "type": "text",
      "value": "application/x-www-form-urlencoded",
      "disabled": true
     }
    ],
    "body": {
     "mode": "urlencoded",
     "urlencoded": [
      {
       "key": "grant_type",
       "value": "client_credentials",
       "type": "text"
      },
      {
       "key": "client_id",
       "value": "{{azureADAppId}}",
       "type": "text"
      },
      {
       "key": "client_secret",
       "value": "{{azureADAppSecret}}",
       "type": "text"
      },
      {
       "key": "scope",
       "value": "{{token_scope}}",
       "type": "text"
      }
     ]
    },
    "url": {
     "raw": "https://login.microsoftonline.com/{{tenantId}}/oauth2/v2.0/token",
     "protocol": "https",
     "host": [
      "login",
      "microsoftonline",
      "com"
     ],
     "path": [
      "{{tenantId}}",
      "oauth2",
      "v2.0",
      "token"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Get Team",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "92ae0b6b-859c-4210-b9ee-d7e76b1bb523",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(200);\r",
       "\r",
       "    const { internalId } = pm.response.json();\r",
       "    pm.environment.set(\"generalChannelId\", internalId);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "GET",
    "header": [
     {
      "key": "Authorization",
      "value": "{{appContextToken}}",
      "type": "text"
     }
    ],
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Edit Team",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "f4fcb689-366e-4d28-9113-45adf84495a5",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(204);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "PATCH",
    "header": [
     {
      "key": "Authorization",
      "value": "{{appContextToken}}",
      "type": "text"
     },
     {
      "key": "Content-Type",
      "value": "application/json",
      "type": "text"
     }
    ],
    "body": {
     "mode": "raw",
     "raw": "{  \r\n  \"funSettings\": {\r\n    \"allowGiphy\": true,\r\n    \"giphyContentRating\": \"strict\"\r\n  },\r\n}"
    },
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Get Channels",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "5acf1e2a-e4bb-4146-a4a7-d8677a3356be",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(200);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "GET",
    "header": [
     {
      "key": "Authorization",
      "value": "{{appContextToken}}",
      "type": "text"
     }
    ],
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}/channels",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}",
      "channels"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Get Specific Channel",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "da816d2b-97d6-4cd6-b243-2eb5257cce7c",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(200);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "GET",
    "header": [
     {
      "key": "Authorization",
      "type": "text",
      "value": "{{appContextToken}}"
     }
    ],
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}/channels/{{generalChannelId}}",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}",
      "channels",
      "{{generalChannelId}}"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Get Channel Messages",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "c511c14f-a193-4387-84d1-94d05f12ee67",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(200);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "GET",
    "header": [
     {
      "key": "Authorization",
      "type": "text",
      "value": "{{appContextToken}}"
     }
    ],
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}/channels/{{generalChannelId}}/messages",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}",
      "channels",
      "{{generalChannelId}}",
      "messages"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Create Channel",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "6e58c6b2-7dd5-4746-b9cb-3b0b1d3b80e7",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "\r",
       "pm.test(\"Status Code 201 or 400\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       " pm.expect(pm.response.code).to.be.oneOf([201, 400]); //400 means that at least the permission check \r",
       "});\r",
       "\r",
       "// pm.test(\"Status Code 201\", () => {\r",
       "//     // Need to validate the request succeeded. \r",
       "//     pm.response.to.have.status(201);\r",
       "// });\r",
       "\r",
       "\r",
       "// pm.test(\"Successful POST request\", function () {\r",
       "//     pm.expect(pm.response.code).to.be.oneOf([201, 400]); //400 means that at least the permission check passed\r",
       "// });"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "POST",
    "header": [
     {
      "key": "Authorization",
      "value": "{{appContextToken}}",
      "type": "text"
     },
     {
      "key": "Content-Type",
      "value": "application/json",
      "type": "text"
     }
    ],
    "body": {
     "mode": "raw",
     "raw": "{\r\n  \"displayName\": \"ChannelCreatedThruRsc\",\r\n  \"description\": \"This channel was created using RSC\",\r\n  \"membershipType\": \"standard\"\r\n}",
     "options": {
      "raw": {
       "language": "json"
      }
     }
    },
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}/channels",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}",
      "channels"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Get Tabs",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "aeafd689-f2b5-48b7-8f44-4d53f070b46e",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(200);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "GET",
    "header": [
     {
      "key": "Authorization",
      "value": "{{appContextToken}}",
      "type": "text"
     }
    ],
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}/channels/{{generalChannelId}}/tabs",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}",
      "channels",
      "{{generalChannelId}}",
      "tabs"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Add Tab",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "0a7cae52-c103-403f-a016-d22c9fe1a477",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 201\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(201);\r",
       "\r",
       "    const { id } = pm.response.json();\r",
       "    pm.environment.set(\"createdTabId\", id);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "POST",
    "header": [
     {
      "key": "Authorization",
      "value": "{{appContextToken}}",
      "type": "text"
     },
     {
      "key": "Content-Type",
      "value": "application/json",
      "type": "text"
     }
    ],
    "body": {
     "mode": "raw",
     "raw": "{\n\t\"teamsApp@odata.bind\":\"https://graph.microsoft.com/beta/appCatalogs/teamsApps/com.microsoft.teamspace.tab.powerbi\",\n\t\"displayName\":\"TabCreatedThroughRsc\"\n}"
    },
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}/channels/{{generalChannelId}}/tabs",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}",
      "channels",
      "{{generalChannelId}}",
      "tabs"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Edit Tab",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "70276fd7-6d40-4305-9628-735170a6e749",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(200);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "PATCH",
    "header": [
     {
      "key": "Authorization",
      "value": "{{appContextToken}}",
      "type": "text"
     },
     {
      "key": "Content-Type",
      "value": "application/json",
      "type": "text"
     }
    ],
    "body": {
     "mode": "raw",
     "raw": "{\n\"displayName\":\"UpdatedTabName\"\n}"
    },
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}/channels/{{generalChannelId}}/tabs/{{createdTabId}}",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}",
      "channels",
      "{{generalChannelId}}",
      "tabs",
      "{{createdTabId}}"
     ]
    }
   },
   "response": []
  },
  {
   "name": "Get InstalledApps",
   "event": [
    {
     "listen": "test",
     "script": {
      "id": "14554c18-68b8-45ec-b1fb-33049b72ff95",
      "exec": [
       "console.log(\"responseHeaders: \" + JSON.stringify(pm.response.headers));\r",
       "console.log(\"responseBody: \" + JSON.stringify(pm.response.text()));\r",
       "\r",
       "pm.test(\"Status Code 200\", () => {\r",
       "    // Need to validate the request succeeded. \r",
       "    pm.response.to.have.status(200);\r",
       "});"
      ],
      "type": "text/javascript"
     }
    }
   ],
   "request": {
    "method": "GET",
    "header": [
     {
      "key": "Authorization",
      "value": "{{appContextToken}}",
      "type": "text"
     }
    ],
    "url": {
     "raw": "https://graph.microsoft.com/beta/teams/{{teamGroupId}}/installedApps?$expand=teamsApp",
     "protocol": "https",
     "host": [
      "graph",
      "microsoft",
      "com"
     ],
     "path": [
      "beta",
      "teams",
      "{{teamGroupId}}",
      "installedApps"
     ],
     "query": [
      {
       "key": "$expand",
       "value": "teamsApp"
      }
     ]
    }
   },
   "response": []
  }
 ],
 "protocolProfileBehavior": {}
}
```
