## Server
{: #Server}

A `server` runs and manages a set of **mediasoup** worker child processes that handle media realtime-communications (ICE, DTLS, RTP, RTCP, DataChannel, etc).


### Dictionaries
{: #Server-dictionaries}

<section markdown="1">

#### ServerSettings
{: #Server-ServerSettings .code}

<div markdown="1" class="table-wrapper">

Field                    | Type    | Description   | Default
------------------------ | ------- | ------------- | -------------
`numWorkers`             | Number  | Number of child worker processes. | The number of CPU cores in the host
`logLevel`               | String  | Logging level for logs generated by the media handler subprocesses (check the [Debugging](/documentation/debugging) documentation). Valid values are "debug", "warn", "error". | "debug"
`rtcListenIPv4`          | String\|boolean | IPv4 for RTC. Valid values are a IPv4, `true` (auto-detect) and `false` (disabled). | `true`
`rtcListenIPv6`          | String\|boolean | IPv6 for RTC. Valid values are a IPv6, `true` (auto-detect) and `false` (disabled). | `true`
`rtcMinPort`             | Number  | Minimun RTC port. | 10000
`rtcMaxPort`             | Number  | Maximum RTC port. | 59999
`dtlsCertificateFile`    | String  | Path to the DTLS certificate. If unset, a random certificate is generated. | Unset
`dtlsPrivateKeyFile`     | String  | Path to the DTLS private key. If unset, a random certificate is generated. | Unset

</div>

#### ServerUpdateableSettings
{: #Server-ServerUpdateableSettings .code}

<div markdown="1" class="table-wrapper">

Field                    | Type    | Description  
------------------------ | ------- | -------------
`logLevel`               | String  | Logging level for logs generated by the media handler subprocesses. Valid values are "debug", "warn", "error".

</div>

</section>


### Properties
{: #Server-properties}

<section markdown="1">

#### server.closed
{: #server-closed .code}

* Read only

A boolean indicating whether the `server` has been closed.

</section>


### Methods
{: #Server-methods}

<section markdown="1">

#### server.close()
{: #server-close .code}

Closes the `server`, including all its `rooms`, and triggers a [`close`](#server-on-close) event.


#### server.dump()
{: #server-dump .code}

For debugging purposes. Returns a Promise that resolves to an Object containing the current status and details of the `server`.

*TBD:* Document it.

#### server.updateSettings(settings)
{: #server-updateSettings .code}

Updates the `server` settings in runtime. Just a subset of the full [ServerSettings](#Server-ServerSettings) can be updated.

<div markdown="1" class="table-wrapper">

Argument   | Type    | Required  | Description  
---------- | ------- | --------- | -------------
`settings` | [ServerUpdateableSettings](#Server-ServerUpdateableSettings) | No | Server settings.

</div>

#### server.Room(settings)
{: #server-Room .code}

Returns a new [Room](#Room) instance.

<div markdown="1" class="table-wrapper">

Argument   | Type    | Required  | Description  
---------- | ------- | --------- | -------------
`settings` | [RoomSettings](#Room-RoomSettings) | No | Room settings.

</div>

Usage example:

```javascript
var room = server.Room();
```

</section>


### Events
{: #Server-events}

The `Server` class inherits from [EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter).

<section markdown="1">

#### server.on("close", fn(error))
{: #server-on-close .code}

Emitted when the `server` is closed. In case of error, the callback is called with the corresponding `Error` object.

```javascript
server.on("close", (error) => {
  if (error)
    console.error("server closed with error: %o", error);
});
```

</section>