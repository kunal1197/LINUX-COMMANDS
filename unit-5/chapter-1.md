# Statement keywords in named.conf

acl             Access Control List - determines the kind of access one has in DNS
include         Allows to include another file
logging         Specifies what gets logged and ignored
options         Addresses global server configuration issues
controls        Allows to declare control channels to be used by rndc
server          Set server specific configuration options
zone            Defines a DNS zone

# DNS Toolbox

## host

### Resolve hostname to IP

```console
user@programmer:~$ host internic.net
```

### Reverse lookups

```console
user@programmer:~$ host 198.41.0.6
```

### Query IPv6 records

```console
user@programmer:~$ host serverB-v6.example.org ::1
```

### Query a PTR record for IPv6

```console
user@programmer:~$ host 2001:db8::2 ::1
```

## dig

### Get MX record for example.org

```console
user@programmer:~$ dig @localhost example.org MX
```

### Query local DNS server for A records

```console
user@programmer:~$ dig @localhost yahoo.com
```

### Query IPv6 capable server for AAAA record

```console
user@programmer:~$ dig @localhost serverB-v6.example.org. -t AAAA
```

### Supress all verbosity

```console
user@programmer:~$ dig +short @localhost yahoo.com
```

### Query local server for reverse lookup information

```console
user@programmer:~$ dig -x 192.168.1.1 @localhost
```

### IPv6 reverse lookup

```console
user@programmer:~$ dig -x 2001:db8::2 @localhost
```

## nslookup

### Query local name server

```console
user@programmer:~$ nslookup www.example.org localhost
```

## whois

### Get information about example.com

```console
user@programmer:~$ whois example.com
```
