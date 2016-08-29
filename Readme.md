shippable-bbs-oauth
===========

A fork of [node-oauth](https://github.com/ciaranj/node-oauth) that can set custom Content-Type headers.


Installation
============== 

    $ npm install shippable-bbs-oauth


Examples
==========

To run examples/tests install Mocha `$ npm install -g mocha` and run `$ mocha you-file-name.js`:

## OAuth1.0

```javascript
describe('OAuth1.0',function(){
  var OAuth = require('oauth');

  it('tests trends Twitter API v1.1',function(done){
    var oauth = new OAuth.OAuth(
      'https://api.twitter.com/oauth/request_token',
      'https://api.twitter.com/oauth/access_token',
      'your application consumer key',
      'your application secret',
      '1.0A',
      null,
      'HMAC-SHA1'
    );
    oauth.get(
      'https://api.twitter.com/1.1/trends/place.json?id=23424977',
      'your user token for this app', //test user token
      'your user secret for this app', //test user secret            
      function (e, data, res){
        if (e) console.error(e);        
        console.log(require('util').inspect(data));
        done();      
      });    
  });
});
```

## OAuth2.0 
```javascript
describe('OAuth2',function(){
  var OAuth = require('oauth');

   it('gets bearer token', function(done){
     var OAuth2 = OAuth.OAuth2;    
     var twitterConsumerKey = 'your key';
     var twitterConsumerSecret = 'your secret';
     var oauth2 = new OAuth2(server.config.keys.twitter.consumerKey,
       twitterConsumerSecret, 
       'https://api.twitter.com/', 
       null,
       'oauth2/token', 
       null);
     oauth2.getOAuthAccessToken(
       '',
       {'grant_type':'client_credentials'},
       function (e, access_token, refresh_token, results){
       console.log('bearer: ',access_token);
       done();
     });
   });
```

Change History
============== 
* 0.9.15
    - OAuth: Allow Content-Type to be set on GET and DELETE requests
* 0.9.14
    - OAuth2:   Extend 'successful' token responses to include anything in the 2xx range.
