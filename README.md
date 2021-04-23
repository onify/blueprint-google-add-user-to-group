[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)
![Test suite](https://github.com/onify/blueprint-google-api-auth/workflows/Test%20suite/badge.svg)

# Onify Blueprint: Add user to group in Google via Google API

This Blueprint shows authenticates with Google API and then adds a user to a group. Please check [Google API docs (Method: members.insert)](https://developers.google.com/admin-sdk/directory/reference/rest/v1/members/insert) for more info. In this Blueprint we also show how to use swimlanes in BPMN to devide different processes.

![alt text](flow.png "Flow")

## Requirements

* Onify Hub v2
* Onify Flow license
* Camunda Modeler 4.4 or later 
* Google G Suite

## Included

* Settings
* Workflow (Flow)

## Setup

### Google

In order to index information from Google we need to setup a couple of things.

1. Create a new Google cloud project (optional)
2. Create a service account
3. Create a private key (json) for the service account
4. Activate Admin SDK service for the project
5. Enable G Suite domain-wide delegation
6. Delegate domain-wide authority to your service account

### Settings

Add the following settings via `/admin/settings`.

|Key|Name|Description|Value|Type|Tag|Role|
|---|----|-----------|-----|----|---|----|
|google_customerid|Google customer id|Customer id where the users are located|xxxxxxx|string|google|admin|
|google_serviceaccount_email|Google service account email|Service account email|*.iam.gserviceaccount.com|string|google|admin|
|google_serviceaccount_impersonate_email|Google service account impersonate email|What user to impersonate. Must be valid user in G Suite|*@onify.co|string|google|admin|
|google_serviceaccount_privatekey|Google service account private key|The private key for the service account|----BEGIN PRIVATE KEY-----***|string|google|admin|

### Flows

#### Configure

You need to update the `Set user and group parameters` task with your own configuration.
This is the default config:

```javascript
next(null, {
  group: {
    groupKey: 'aaabbbccc'
  },
  user: {
    email: 'user@acme.com',
    role: 'MEMBER',
    type: 'USER',
    delivery_settings: 'ALL_MAIL'
  }
});
```

> NOTE: Read more about the REST API request in Google here: [Google API docs (Method: members.insert)](https://developers.google.com/admin-sdk/directory/reference/rest/v1/members/insert).


#### Deploy

1. Open `blueprint-google-add-user-to-group.bpmn` in Camunda Modeler
2. Click `Deploy current diagram` and follow the steps

#### Run 

To test and run the flow, click `Start current diagram`

## Support

* Community/forum: https://support.onify.co/discuss
* Documentation: https://support.onify.co/docs
* Support and SLA: https://support.onify.co/docs/get-support

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.