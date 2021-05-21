# systemd-cfddns dualwan
Bash script to emulate DDNS client for Cloudflare-managed domain

# Difference from the original
- Dirty hack to work in a dual wan enviroment
- Works only in a very specific enviroment, if yours differs from mine it will most probably not work

# Configuration

- You need to create the DNS records before you can use this script
- You need to change api_token and zone_identifier

# Enviroment in use

I use OpenWRT with mwan3 for routing. The client needs to request IPv6 addresses via DHCPv6 so you get get a /128 with a static suffix
ISP 1 does have its IPv6 space in 2a01::/16 and ISP 2 in 2a02::/16 if that differs for you, you will need to rework how you get your IPv6 for each connection.
You will need to have a server with two IPv4 addresses running so you can set in mwan3 to use wan1 only for IPv4 1 and use only wan2 for IPv4 2
I have on the external server this PHP code running to return the IPv4s for the script
```php
<?php echo $_SERVER['REMOTE_ADDR']; ?>
```

# Pitfalls

- There is no error handling, if one connection is down there is no logic to remove the DNS entries for that connection