### Get engine ID

To get the engine ID, submit a`GET` request using`engines:getIDbyName`. Specify the name of your engine as shown by `YOUR_ENGINE_NAME`in the example below.

**Request**

```bash
curl --request GET 'https://api.app.firebolt.io/core/v1/account/engines:getIDbyName?YOUR_ENGINE_NAME' \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN_VALUE'
```

**Response**

```bash
{
  "engine_id" {
    "account_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "engine_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
  }
}
```

### Start an engine

To start an engine, submit a `POST` request to `ENGINE_ID:start`. Replace `ENGINE_ID` with the value you retrieved for `engine_id`.

**Request**

```bash
curl --request POST 'https://api.app.firebolt.io/core/v1/account/engines/ENGINE_ID:start' \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN_VALUE'
```

**Response**

```bash
{
    "engine": {
        "id": {
            "account_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "name": "YOUR_ENGINE_NAME",
        "description": "",
        "emoji": "1F3A5",
        "compute_region_id": {
            "provider_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "region_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "settings": {
            "preset": "ENGINE_SETTINGS_PRESET_GENERAL_PURPOSE",
            "auto_stop_delay_duration": "1200s",
            "minimum_logging_level": "ENGINE_SETTINGS_LOGGING_LEVEL_INFO",
            "is_read_only": false,
            "warm_up": "ENGINE_SETTINGS_WARM_UP_INDEXES"
        },
        "current_status": "ENGINE_STATUS_RUNNING_IDLE",
        "current_status_summary": "ENGINE_STATUS_SUMMARY_STOPPED",
        "latest_revision_id": {
            "account_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_revision_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "endpoint": "MY_ENGINE_NAME.firebolt-product.us-east-1.app.firebolt.io",
        "endpoint_serving_revision_id": null,
        "create_time": "2021-05-03T20:40:43.024856Z",
        "create_actor": "/users/xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "last_update_time": "2021-05-21T23:54:15.841494Z",
        "last_update_actor": "",
        "last_use_time": null,
        "desired_status": "ENGINE_STATUS_UNSPECIFIED",
        "health_status": "ENGINE_HEALTH_STATUS_UNSPECIFIED",
        "endpoint_desired_revision_id": null
    },
    "desired_engine_revision": null
}
```

### Stop an engine

To stop an engine, submit a `POST` request to `ENGINE_ID:stop`. Replace `ENGINE_ID` with the value the you retrieved for`engine_id`.

**Request**

```bash
curl --request POST 'https://api.app.firebolt.io/core/v1/account/engines/ENGINE_ID:stop' \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN_VALUE'
```

**Response**

```bash
{
    "engine": {
        "id": {
            "account_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "name": "YOUR_ENGINE_NAME",
        "description": "",
        "emoji": "1F3A5",
        "compute_region_id": {
            "provider_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "region_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "settings": {
            "preset": "ENGINE_SETTINGS_PRESET_GENERAL_PURPOSE",
            "auto_stop_delay_duration": "1200s",
            "minimum_logging_level": "ENGINE_SETTINGS_LOGGING_LEVEL_INFO",
            "is_read_only": false,
            "warm_up": "ENGINE_SETTINGS_WARM_UP_INDEXES"
        },
        "current_status": "ENGINE_STATUS_RUNNING_REVISION_SERVING",
        "current_status_summary": "ENGINE_STATUS_SUMMARY_RUNNING",
        "latest_revision_id": {
            "account_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_revision_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "endpoint": "YOUR_ENGINE_NAME.firebolt-product.us-east-1.app.firebolt.io",
        "endpoint_serving_revision_id": null,
        "create_time": "2021-05-03T20:40:43.024856Z",
        "create_actor": "/users/xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "last_update_time": "2021-05-24T21:05:59.388381Z",
        "last_update_actor": "",
        "last_use_time": null,
        "desired_status": "ENGINE_STATUS_UNSPECIFIED",
        "health_status": "ENGINE_HEALTH_STATUS_UNSPECIFIED",
        "endpoint_desired_revision_id": null
    },
    "desired_engine_revision": null
}
```

### Restart an engine

To restart an engine, submit a `POST` request to `ENGINE_ID:stop`. Replace `ENGINE_ID` with the value the you retrieved for`engine_id`.

**Request**

```bash
curl --request POST 'https://api.app.firebolt.io/core/v1/account/engines/ENGINE_ID:restart' \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN_VALUE'
```

**Response**

```bash
{
    "engine": {
        "id": {
            "account_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "name": "YOUR_ENGINE_NAME",
        "description": "",
        "emoji": "1F3A5",
        "compute_region_id": {
            "provider_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "region_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "settings": {
            "preset": "ENGINE_SETTINGS_PRESET_GENERAL_PURPOSE",
            "auto_stop_delay_duration": "1200s",
            "minimum_logging_level": "ENGINE_SETTINGS_LOGGING_LEVEL_INFO",
            "is_read_only": false,
            "warm_up": "ENGINE_SETTINGS_WARM_UP_INDEXES"
        },
        "current_status": "ENGINE_STATUS_RUNNING_REVISION_SERVING",
        "current_status_summary": "ENGINE_STATUS_SUMMARY_RUNNING",
        "latest_revision_id": {
            "account_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "engine_revision_id": "xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        },
        "endpoint": "YOUR_ENGINE_NAME.YOUR_ACCOUNT_NAME.us-east-1.app.firebolt.io",
        "endpoint_serving_revision_id": null,
        "create_time": "2021-05-03T20:40:43.024856Z",
        "create_actor": "/users/xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "last_update_time": "2021-05-24T21:15:00.522042Z",
        "last_update_actor": "",
        "last_use_time": null,
        "desired_status": "ENGINE_STATUS_UNSPECIFIED",
        "health_status": "ENGINE_HEALTH_STATUS_UNSPECIFIED",
        "endpoint_desired_revision_id": null
    },
    "desired_engine_revision": null
}
```

## Get the URL of an engine

When you submit a request to run a Firebolt REST API operation, most requests require the URL of the engine to run the request. The engine must be running to accept requests. Commands to start, stop, and restart and engine use the engine ID instead of the URL. For more information about starting, stopping, and restarting engines using the Firebolt REST API, see [Start, stop, and restart engines](connecting-via-rest-api.md#start-stop-and-restart-engines) above.

**Get the URL of the default engine in your database**

Use the following request to get the URL of the default engine in your database:

```bash
curl --request GET 'https://api.app.firebolt.io/core/v1/account/engines:getURLByDatabaseName?database_name=YOUR_DATABASE_NAME' \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN_VALUE'
```

This results with:

```javascript
{
    "engine_url": "YOUR_ENGINE_URL"
}
```

**Get the URL of an engine with engine name**

Use the following request to retrieve the URL of an engine by using the engine name:

```bash
curl --request GET 'https://api.app.firebolt.io/core/v1/account/engines?filter.name_contains=YOUR_ENGINE_NAME' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN_VALUE'
```

This results with:

```sql
{
  "page": {
    ...
  },
  "edges": [
    {
      ...
        "endpoint": "YOUR_ENGINE_URL",
      ...
      }
    }
  ]
}
```
