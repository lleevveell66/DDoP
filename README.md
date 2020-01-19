<<<<<<< HEAD
DDoP (Distributed Denial of Packets) v.0.0.1
by level6 of LiE
---------------------------------------------

This is a work in progress...  sorry.  

To Do:
------
- Add ddop_fwscript script for firewalld
- Daemonize ddopd and built init scripts for sysv
- Implement SSL for MQTT

Theory of Operation:
--------------------
I have several public-facing IP addresses which do not route through a single firewall/gateway 
that I control.  They each have their own firewall configured.  I have centralized logging and 
alerting, and am constantly being attacked on one or more.  I got sick of hitting every box 
to block the same IP or subnet.  So, DDoP was born.  

By utilizing MQTT, machines can "subscribe" to channels to listen to, then decide to take 
action on themselves based on that.  An attack on one machine could trigger an MQTT "publish" to 
the broker, and all other machines which are subscribing can then also block the attacker.

Better description to come later...


Requirements:
-------------
- Perl
- Net::MQTT::Simple
- MMQT Mosquito broker running on some reachable server
- Customization of ddop_fwscript for your chains, tables, software, etc.

Installation:
-------------

chmod 755 ddop*
cp ddop* /usr/local/bin

# In one terminal (this will be daemonized, later):
/usr/local/bin/ddopd -s your_mqtt_broker_ip -h this_host_tag

# Customize the ddop_fwscript, making sure to pay attention to the chain names, etc.

# In another terminal, to test with iptables:
/usr/local/bin/ddop -s your_mqtt_broker_ip -h this_host_tag -t insert -i 123.123.123.0/24

# Verify the new rule for 123.123.123.0/24 was inserted
iptables -L -n | grep 123

/usr/local/bin/ddop -s your_mqtt_broker_ip -h this_host_tag -t delete -i 123.123.123.0/24

# Verify the new rule for 123.123.123.0/24 was deleted
iptables -L -n | grep 123

# Check syslog for the activity.
=======
# DDoP
DDoP (Distributed Denial of Packets)
>>>>>>> 142624e2287941bd37764f48e74d184278420d86
