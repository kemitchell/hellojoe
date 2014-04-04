nOTP
====

Not OTP.

nOTP is built on top of Node's `cluster` module to manage worker
threads. It allows you to write your application in an Erlang like
style, where if something goes wrong, crashing the whole process is
the acceptable and preferred way of handling it.

## Usage

Call `notp.serve` with a configuration object (can be empty, the
defaults are OK) and a function containing your main application code.
It should be the first and only thing your application does. Do *not*
initialise any resources before calling this function.

```js
var notp = require("notp");

notp.serve({}, function app() {
   /// my application code goes here
});
```

nOTP will launch a number of subprocesses running the provided
function, and the master process will be left in charge of monitoring
them and restarting them as necessary.

The configuration object you provide is merged with these default
values:

```js
{
  cores: n, // n == the physical number of cores on the running machine
  failureThreshold: 5000, // minimum lifetime (ms) of a process not considered a failure
  retryThreshold: 23, // amount of consecutive failures before retryDelay is triggered
  retryDelay: 10000 // delay (ms) before spawning processes after consecutive failures
}
```

# License

Copyright 2014 Future Ad Labs Ltd

Licensed under the Apache License, Version 2.0 (the "License"); you
may not use this file except in compliance with the License. You may
obtain a copy of the License at
[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
implied. See the License for the specific language governing
permissions and limitations under the License.