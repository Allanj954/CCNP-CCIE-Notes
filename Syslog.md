# Syslog

- Standardized in RFC 5424
- Widely supported on most OS platforms
- Centralized servers are ideal for enterprice networks
- Centralized tools provide event correlation

- Console logging:By default, the router sends all log messages to its console port. Hence only the users that are physically connected to the router console port can view these messages.

- Terminal logging:It is similar to console logging, but it displays log messages to the router's VTY lines instead. This is not enabled by default

- Buffered logging:This type of logging uses router's RAM for storing log messages. buffer has a fixed size to ensure that the log will not deplete valuable system memory. The router accomplishes this by deleting old messages from the buffer as new messages are added.

- Syslog Server logging :The router can use syslog to forward log messages to external syslog servers for storage. This type of logging is not enabled by default.

- SNMP trap logging:The router is able to use SNMP traps to send log messages to an external SNMP server.

## Console Logging

The router does not check if a user is logged into the console port or a device is attached to it; if console logging is enabled, messages are always sent to the console port that can cause CPU load.

## Buffered logging

You want your router to record log messages, instead of just displaying them on the console.To use logging buffered configuration command to enable the local storage of router log messages

## Terminal logging

You want the router to display log messages to your VTY session in real time.Use the terminal monitor command to enable the displaying of log messages to your VTY:

## Syslog Server logging

You want to send log messages to a remote syslog server. By using this we can send messages to an external device for storing this logs and the storage size does depend on the available disk space of the external syslog server.

| Code | Severity      | Description                       |
| ---- | ------------- | --------------------------------- |
| 0    | Emergency     | System is unstable                |
| 1    | Alert         | Immediate action needed           |
| 2    | Critical      | Critical conditions exist         |
| 3    | Error         | Error conditions exists           |
| 4    | Warning       | Warning conditions exis t         |
| 5    | Notice        | Normal but significant conditions |
| 6    | Informational | Information messages              |
| 7    | Debug         | Debug-level messages              |

(Credit: TCC_2) - https://community.cisco.com/t5/networking-documents/how-to-configure-logging-in-cisco-ios/ta-p/3132434
