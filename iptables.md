# Configuring the firewall on Linux with iptables

`iptables` is installed by default on most Linux systems. To confirm that iptables is installed, use the following command:

> sudo apt-get install iptables

To make sure that your iptables rules are persistent after reboot, you must install the iptables persistent package using the following command:

> sudo apt-get install iptables-persistent

Once this is installed, the iptables folder will contain two files for IPV4 and IPV6 rules:

```
/etc/iptables/rules.v4
/etc/iptables/rules.v6
```

Typically, an iptables command is as follows:

> sudo iptables [option] CHAIN_rule [-j target]

Here is a list of some common iptables options:

- `-A --append`: Adds a rule to a string (at the end).
- `-C --check`: Finds a rule that matches the requirements of the string.
- `-D --delete`: Removes the specified rules from a string.
- `-F --flush`: Deletes all rules.
- `-I --insert`: Adds a rule to a string at a given position.
- `-L --list`: Displays all rules in a string.
- `-N -new chain`: Creates a new string.
- `-v --verbose`: Displays more information when using a list option.
- `-X --delete-chain`: Deletes the supplied string.

### Check the current status of iptables

To display all of the current rules on your server, enter the following command in the terminal window:

```bash
sudo iptables -L
```

### Allow traffic on localhost

To allow traffic from your own system (the localhost), add the input string by entering the following:

```bash
sudo iptables -A INPUT -i lo -j ACCEPT
```
