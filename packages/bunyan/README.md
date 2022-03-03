# 🪵 Logtail - Bunyan writable stream

[![ISC License](https://img.shields.io/badge/license-ISC-ff69b4.svg)](LICENSE.md)

**New to Logtail?** [Here's a low-down on logging in JavaScript.](https://github.com/logtail/logtail-js)

## `@logtail/bunyan`

This NPM library provides a [Bunyan](https://github.com/trentm/node-bunyan) writable stream that transmits logs to Logtail.com via the `@logtail/node` logger.

Here's how to get started:

## Installation

Install the Node.js Logtail logger and the Bunyan stream plugin via NPM:

```
npm i @logtail/node @logtail/bunyan
```

## Importing

In ES6/Typescript, import both the `Logtail` logger class and the Logtail Bunyan stream class:

```typescript
import { Logtail } from "@logtail/node";
import { LogtailStream } from "@logtail/bunyan";
```

For CommonJS, require the packages instead:

```js
const { Logtail } = require("@logtail/node");
const { LogtailStream } = require("@logtail/bunyan");
```

## Creating a client/stram

You can [create a client](https://github.com/logtail/logtail-js/tree/master/packages/node#creating-a-client) the usual way for `@logtail/node`, and then pass it into a new instance of `LogtailStream`:

```typescript
// Assuming you've imported the Logtail packages above, also import Bunyan...
import bunyan from "bunyan";

// Create a Logtail client
const logtail = new Logtail("logtail-source-token");

// Create a Bunyan logger - passing in the Logtail stream
const logger = bunyan.createLogger({
  name: "Example logger",
  level: "debug",
  streams: [
    {
      stream: new LogtailStream(logtail),
    },
  ],
});

// Log as normal in Bunyan - your logs will sync with Logtail.com!
logger.info("Hello from Bunyan");
```

## Log levels

Logtail will log at the `debug` level and above. Trace logs or any log level below `20` will be ignored.

The `fatal` log level is transformed to `error` in the Logtail logger.

## LICENSE

[ISC](LICENSE.md)
