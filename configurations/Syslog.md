# Syslog Configuration

## Console logging

The router does not check if a user is logged into the console port or a device is attached to it; if console logging is enabled, messages are always sent to the console port that can cause CPU load.

To stop the console logging, use the `no logging console` global configuration command.

## Buffered logging

```
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#logging buffered informational
Router(config)#end
```

You can also Set the Log Size on router.

```
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#logging buffered 64000
Router(config)#end
```

## Terminal logging

```
Router#terminal monitor
Router#
```

To disable logging to your VTY session, use the following command:

```
Router#terminal no monitor
Router#
```

## Syslog Server logging

If you have any syslog server please find the below simple config.

```
router#conf t
Router(config#logging host x.x.x.x
Router(config)#logging traps (i.e 0 1 2 3 4 5 .. according to your requirement)
```
