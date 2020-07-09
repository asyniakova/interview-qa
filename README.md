# API QA

Design a set of integration tests in Postman for the provided API.

## Instructions

The API that you will be testing can be found [here](https://documenter.getpostman.com/view/6917194/SzYdSvsf?version=latest). Use the `dev` environment for all the tests:

- https://api.identity.charge-dev.net/v1.0

The login credentials are:

```json
{
    "email": "admin@admin.com",
    "password": "password"
}
```

Provide your solution as an exported Postman collection in `json`:

- Collection v2.1

To submit your solution:

- clone this repository: `git clone git@github.com:charge-tech/interview-qa.git`

- branch off master: `git checkout -b my_name_here`

- add the Postman `json` collection and push to your branch

You can also email the `json` collection if you prefer.

## Requirements

The order of the tests should be

- **success case** - `POST /login` with the given credentials

- **success case** -`POST /apiKeys` create a new api key following the documentation

- **success case** -`GET /apiKeys/:id` get the previously created api key by `id`

- **fail case** - `GET /apiKeys/:id` try to get an api key by passing a wrong `id` 

- **success case** - `DELETE /apiKeys/:id` delete the previously created api key by `id`

- **success case** - `POST /webhooks` create a new webhook following the documentation

- **success case** -`GET /webhooks/:id` get the previously created webhook by `id`

- **fail case** - `GET /webhooks/:id` try to get a webhook by passing a wrong `id`

- **success case** - `DELETE /webhooks/:id` delete the previously created webhook by `id`

- each test should validate the response, including the following:

**status code**
```
pm.test("status code test", function () {
    pm.response.to.have.status(The code I expect here);
});
```

**response body**
```
pm.test("response must be valid and have a body", function () {
     pm.response.to.be.ok;
     pm.response.to.be.withBody;
     pm.response.to.be.json;
     pm.expect(response.body.PARAMETER).is.to.equal(The value I expect)
     // All other parameters of response
});
```

- set an environment variable for the `jwt` that is returned from `POST /login` and use this to authenticate all subsequent requests

- tests should be sequential meaning that the order matters:

```
postman.setNextRequest("my next request here")
```

## Bonus

Using Postman's visualization [tool](https://learning.postman.com/docs/sending-requests/visualizer/) generate a table visualization for the response for:

- `GET /webhooks/:id`