# passport-concur

[![Build](https://travis-ci.org/outrightmental/passport-concur.png)](https://travis-ci.org/outrightmental/passport-concur)
[![Coverage](https://coveralls.io/repos/outrightmental/passport-concur/badge.png)](https://coveralls.io/r/outrightmental/passport-concur)
[![Quality](https://codeclimate.com/github/outrightmental/passport-concur.png)](https://codeclimate.com/github/outrightmental/passport-concur)
[![Dependencies](https://david-dm.org/outrightmental/passport-concur.png)](https://david-dm.org/outrightmental/passport-concur)
[![Tips](http://img.shields.io/gittip/jaredhanson.png)](https://www.gittip.com/jaredhanson/)

An OAuth 2.0 connector for the [Concur API](https://developer.concur.com/api-documentation), adapted from Jared Hanson's original [passport-oauth2](https://github.com/jaredhanson/passport-oauth2), a general-purpose OAuth 2.0 authentication strategy for [Passport](http://passportjs.org/).

This module lets you authenticate using the Concur API via OAuth 2.0 in your Node.js applications.
By plugging into Passport, OAuth 2.0 authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

Note that this strategy provides generic OAuth 2.0 support.  In many cases, a
provider-specific strategy can be used instead, which cuts down on unnecessary
configuration, and accommodates any provider-specific quirks.  See the
[list](https://github.com/jaredhanson/passport/wiki/Strategies) for supported
providers.

## Install

    $ npm install passport-concur

## Usage

#### Configure Strategy

The OAuth 2.0 authentication strategy authenticates users using a third-party
account and OAuth 2.0 tokens.  The provider's OAuth 2.0 endpoints, as well as
the client identifer and secret, are specified as options.  The strategy
requires a `verify` callback, which receives an access token and profile,
and calls `done` providing a user.

    passport.use(new ConcurStrategy({
        authorizationURL: 'https://www.example.com/oauth2/authorize',
        tokenURL: 'https://www.example.com/oauth2/token',
        clientID: EXAMPLE_CLIENT_ID,
        clientSecret: EXAMPLE_CLIENT_SECRET,
        callbackURL: "http://localhost:3000/auth/example/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ exampleId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'oauth2'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/example',
      passport.authenticate('oauth2'));

    app.get('/auth/example/callback',
      passport.authenticate('oauth2', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Related Modules

- [passport-oauth2](https://github.com/jaredhanson/passport-oauth2) — OAuth 2.0 authentication strategy
- [passport-oauth1](https://github.com/jaredhanson/passport-oauth1) — OAuth 1.0 authentication strategy
- [passport-http-bearer](https://github.com/jaredhanson/passport-http-bearer) — Bearer token authentication strategy for APIs
- [OAuth2orize](https://github.com/jaredhanson/oauth2orize) — OAuth 2.0 authorization server toolkit

## Tests

    $ npm install
    $ npm test

## Credits

  - [Nick Kaye](http://github.com/nickckaye)
  - [Jared Hanson](http://github.com/jaredhanson)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2011-2014 Jared Hanson <[http://jaredhanson.net/](http://jaredhanson.net/)>
