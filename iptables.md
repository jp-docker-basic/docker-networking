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

This command configures the `firewall` to accept traffic for the `localhost (lo)` `interface (-i)`. From now on, everything that comes from your system will pass through your firewall. You must set this rule to allow applications to communicate with the localhost interface.

### Allow traffic on specific ports

These rules allow traffic on the different ports that you specify using the commands listed below. A port is a communication endpoint specified for a specific type of data.

To allow HTTP Web traffic, enter the following command:

> sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT

To allow only inbound SSH (Secure Shell) traffic, enter the following (note that we use the default `SSH` port number `22`. If your port number is different, make sure to adjust the commands accordingly):

> sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

To allow HTTPS Internet traffic, enter the following command:

> sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

The options work this way:

- `-p`: Checks the specified protocol (tcp).
- `--dport`: Specifies the destination port.
- `-j jump`: Performs the action.

### Control traffic by IP address

Use the following command to accept traffic from a specific IP address.

> sudo iptables -A INPUT -s your_IP_address_to_authorise -j ACCEPT

Replace the IP address in the command with the IP address you want to authorise.

You can also block traffic from an IP address:

> sudo iptables -A INPUT -s your_IP_address_to_block -j DROP

Replace the IP address in the command with the IP address you want to block.

You can reject traffic from an IP address range with the following command:

> sudo iptables -A INPUT -m iprange --src-range your_start_IP_address-your_end_IP_address -j REJECT
