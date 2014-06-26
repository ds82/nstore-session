# nStore Session Store for Connect

[connect]: https://github.com/senchalabs/connect
[express]: https://github.com/visionmedia/express
[nStore]: http://github.com/creationix/nstore

This is a simple session store for [connect][] and [express][] based apps that uses [nStore][] for persisting session data.  It implements the full Session Store interface and has built-in pruning of stale sessions on every nStore database compaction.

## Usage

Create a connect/express app, and use this as the session store:

```
var
  express         = require('express'),
  app             = express(),
  nstoreSession   = require('nstore-session');
  ...
  app.configure(function() {
    app.use( express.cookieParser() );
    app.use( express.methodOverride() );
    app.use( express.session({ secret: 'keyboard cat', store: new nstoreSession() } ));
  });
  ...
  app.listen( process.env.PORT || 9000 );
```

## Options

You can pass options into the call to `new nStoreSession({})`.

 - **maxAge** - When the nStore database is compacted, any sessions last accessed more than `maxAge` ago (in ms) will be pruned. Defaults to 1 hour.
 - **dbFile** - Where to store the nStore database, defaults to "sessions.db" in the current directory.
 
