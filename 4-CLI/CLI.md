# CLI

* Command line interface
* interface you use to configure cisco devices

## Rollover cable

You connect to a cisco device with a rollover cable. The pins in a rollover cable connect like:

1 -> 8<br/>
2 -> 7<br/>
3 -> 6<br/>
4 -> 5<br/>
5 -> 4<br/>
6 -> 7<br/>
8 -> 1<br/>

## Cisco IOS CLI

To enable privilaged exec mode
```
Router>enable
Router#
```
`?` can be used to find commands
```
Router>e?
enable exit
```
### Global configuration mode
```
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#
```
#### Enable password
```
Router(config)#enable password ?
7       Specifies a HIDDEN password will follow
LINE    The UNENCRYPTED (cleartext) 'enable' password
level   Set exec level password

Router(config)#enable password CCNA
```

```
Router(config)#exit
Router#exit
Router>enable
Password:
Router#
```

### Running config/startup config

There are two configuration files kept on the device at once. The running config is the current active file on the device, as you enter commands on the CLI you edit the active configuration. The startup config is the configuration file that will be loaded on restart of the device.

```
Router#show running-config

Router#show startup-config
```
To save the running config:
```
Router#write

Router#write memory

Router#copy running-config startup-config
```

### Service password-encryption
```
Router#conf t
Router(config)#service password-encryption
```
Or for more secure
```
Router(conifg)#enable secret Cisco
Router(config)#do sh run
```

If you enable the service password encryption command: Current passwords will be encrypted, future passwords will be encrypted, the enable secret will not be effected. If you disable it, current passwords will not be decrypted, future passwords will not be decrypted, the enable secret will not be effected.