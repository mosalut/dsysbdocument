# dsysb Documentation

##  running
Assuming you are already in the directory where the program is located, you can run _dsysb_ directly in the terminal, or use  `&`  to run it in the background. For example:

```bash
$ ./dsysb -<connections|http_port|ip|log_file|network_id|port|remote_host>=<value> &
```
For background execution, it is recommended to use[tmux](https://github.com/tmux/tmux/wiki)


## Parameter Details

- _\-connections_  Maximum number of P2P connections，default: 32
- _\-http\_port_ HTTP Startup Port，default: "20000"
- _\-ip_ IP address to start the P2P service，default:"0.0.0.0"
- _\-log\_file_ Whether to write logs to a file，default: false
- _\-network\_id_  Network ID，0：Mainnet，1-15：Different testnets，16：Development network，default: 0
- _\-port_ P2P Startup port，default:10000
- _\-remote\_host_ specifies a remote P2P node’s UDP address. If `-remote_host` is provided, the seed addresses listed in `remote_hosts` in the config file will no longer be used.


Connect to Mainnet
```bash
$ ./dsysb -remote_host=124.243.173.119:10000
```

Connect to Testnet if it's running
```bash
$ ./dsysb -network_id=1 -remote_host=124.243.173.119:10000
```

In the same directory as dsysb, there is a configuration file named `config`.
Inside it, the field remote_hosts specifies the seed node addresses that the client should connect to. Multiple addresses are separated by commas.

For example:
remote_hosts=61.168.100.4:10000,61.168.100.10:10000

Note: Do not configure the _-remote\_host_ option with the address of the current node; doing so can cause unpredictable behavior. Providing the address of an inactive or non‑existent node (with the correct format) will not cause execution errors, but the connection attempt will silently fail.
