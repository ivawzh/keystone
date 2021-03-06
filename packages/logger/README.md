<!--[meta]
section: api
subSection: utilities
title: Logger
[meta]-->

# Logger

**Deprecation notice** This module is no longer maintained. Please directly use `pino` or the logging library of your choice.

## API

### `require('@keystonejs/logger').logger(name)`

Provides an instance of [`pino`](https://github.com/pinojs/pino) based on the given `name`.

Instances are cached and re-used, making it safe to request the same named instance across multiple files.

### `process.env.DISABLE_LOGGING`

When set to any "truthy" value, will prevent any log output from occurring (particularly useful during test runs).
