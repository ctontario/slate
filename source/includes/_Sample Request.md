# Sample Request

```javascript
"use strict";
const request = require('request');

const apiURL = 'https://ctodev.com/api/v1/';  // accessing the test deployment
const apiUser = 'username';                   // replace with your username
const apiPassword = '********';               // replace with your password
const studyId = '5a58e242496a3b420ef6991e';   // example study Id

const authRequestOptions = {
    url: apiURL + 'security/authentication',
    method: 'POST',
    headers: {
        'Content-Type':     'application/json'
    },
    json: {
        'username' : apiUser,
        'password': apiPassword,
    }
};

// make the authentication post request to get the JWT token
request(authRequestOptions, (err, response, authBody) => {

    // ... handle errors ...

    // make the study request with the JWT token
    const studyRequestOptions = {
        url: apiURL + 'study/' + studyId,
        method: 'GET',
        headers: {
            'Authorization' : authBody.token
        }
    };

    request(studyRequestOptions, (err, response, body) => {

        // ... handle errors ...

        // the returned body is a JSON object, for demo we parse it to a string and log to the console.
        console.log(JSON.stringify(JSON.parse(body), null, 4));
    });
});
```



 Here is an example nodejs script to get one study's data from the CTO Registry API

 * First, a POST request is made to authenticate and get a JWT token
 * Second, the JWT token is sent as an Authorization header in the request for the study

