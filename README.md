node-travis-ci
==============

node library to access the [Travis-CI API](https://api.travis-ci.org/docs/)

### [Installation](https://npmjs.org/package/travis-ci)

```bs
npm install --save travis-ci
```

### Instantiation

```js
var Travis = require('travis-ci');
var travis = new Travis({
  version: '2.0.0'
});
```

### Authentication

Currently the only way to authenticate is to start with a github oauth token, request a travis access token, and authenticate with that.

```js
travis.auth.github({
    github_token: GITHUB_OAUTH_TOKEN
}, function (err, res) {
    // res => {
    //     access_token: XXXXXXX
    // }
    travis.authenticate(res.access_token, function (err) {
         // we've authenticated!
    });
});
```

### [Accounts](https://api.travis-ci.org/docs/#Accounts)

```js
travis.accounts(function (err, res) {
    // res => {
    //     accounts: [
    //         {
    //             id: 5186,
    //             name: 'Patrick Williams',
    //             login: 'pwmckenna',
    //             type: 'user',
    //             repos_count: 37
    //         },
    //         ...
    //     ]
    // }
})
```

### [Authorization](https://api.travis-ci.org/docs/#Authorization)

```js
travis.auth.github({
    github_token: GITHUB_OAUTH_TOKEN
}, function (err, res) {
    // res => {
    //     access_token: XXXXXXX
    // }
});
```

Additional endpoints that have not be implemented yet:
- [travis.auth.authorize](https://api.travis-ci.org/docs/#/auth/authorize)
- [travis.auth.access_token](https://api.travis-ci.org/docs/#POST /auth/access_token)

Endpoints that exist, but are intended for brower flows:
- [travis.auth.handshake](https://api.travis-ci.org/docs/#/auth/handshake)
- [travis.auth.post_message](https://api.travis-ci.org/docs/#/auth/post_message)
- [travis.auth.post_message.iframe](https://api.travis-ci.org/docs/#/auth/post_message/iframe)

### [Broadcasts](https://api.travis-ci.org/docs/#Broadcasts)

```js
travis.broadcasts(function (err, res) {
    // res => {
    //     broadcasts: []
    // }
})
```

### [Endpoints](https://api.travis-ci.org/docs/#Endpoints)

```js
```

### [Repos](https://api.travis-ci.org/docs/#Repos)

```js
travis.repos({
    owner_name: 'pwmckenna'
//  member: 'pwmckenna
}, function (err, res) {
    // res => {
    //     "repos": [
    //         {
    //         "id": 1095505,
    //         "slug": "pwmckenna/node-travis-ci",
    //         "description": "node library to access the Travis-CI API",
    //         "last_build_id": 6347735,
    //         "last_build_number": "468",
    //         "last_build_state": "started",
    //         "last_build_duration": null,
    //         "last_build_language": null,
    //         "last_build_started_at": "2013-04-15T09:45:29Z",
    //         "last_build_finished_at": null
    //         }
    //     ]
    // }
});

travis.repos({
    owner_name: 'pwmckenna',
    name: 'node-travis-ci'
}, function (err, res) {
    // res => {
    //     "repo": {
    //         "id": 1095505,
    //         "slug": "pwmckenna/node-travis-ci",
    //         "description": "node library to access the Travis-CI API",
    //         ...
    //     }
    // }
});

travis.repos.key({
    id: 
}, function (err, res) {
    // res => {
    //   key: '-----BEGIN RSA PUBLIC KEY-----\nMIGfMA0GCSqGSIb...'    
    // }
});

travis.repos.builds({
    owner_name: 'pwmckenna',
    name: 'node-travis-ci'
}, function (err, res) {
    // res => {
    //     builds: [],
    //     commits: []
    // }
});
```

### [Hooks](https://api.travis-ci.org/docs/#Hooks)

All hook calls require [authentication](#Authentication).

```js
travis.hooks(function (err, res) {
    // res => [
    //     {
    //         id: 1095505,
    //         name: 'node-travis-ci',
    //         owner_name: 'pwmckenna',
    //         description: 'node library to access the Travis-CI API',
    //         active: true,
    //         private: false,
    //         admin: true
    //     }
    //     ...
    // ]
});

travis.hooks({
    id: 1095505,
    active: false
}, function (err, res) {
});
```

### [Jobs](https://api.travis-ci.org/docs/#Jobs)

```js
travis.jobs(function (err, res) {
    
});

travis.jobs.log({
    job_id: JOB_ID
}, function (err, res) {
    
})
```

### [Logs](https://api.travis-ci.org/docs/#Logs)

```js
travis.logs({
    id: LOG_ID
}, function (err, res) {
    
});
```

### [Users](https://api.travis-ci.org/docs/#Users)

All user calls require [authentication](#Authentication).

```js
travis.users(function (err, res) {
    // res => {
    //     id: 5186,
    //     name: 'Patrick Williams',
    //     login: 'pwmckenna',
    //     ...
    // } 
});

travis.users.permissions(function (err, res) {});
travis.users.sync(function (err, res) {});
```
