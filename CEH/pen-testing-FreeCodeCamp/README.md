# newly to me

an important file for unauthorized access logs is `/var/log/auth.log`, in kali, it might be the same on ubuntu! and what about centOS

Tutor's said `ifconfig` is the most important tool for networking, `iwconfig` for wifi

`ping -c n {target-ip}` the flag means count, we can do this:

```sh
ping -c 1 8.8.8.8
```

`arp -a` is short code prints ip && mac addresses

another tool is `netstat -ano` he likes these flags. it appears open ports and their attached to tools.

install the useful `ftp` tool, which is removed from default apps

another useful tool for internal penetration testing is `impacket` install it from github, it's useful for networking!

```sh
# he firstly removes everything related to it from kali, because of misConfigs
apt purge *impacket* # 🔴 purge is USEFUL 🔴
# then cloning the github repo after searching for it, secureAuthCorp is its author
cd /opt/
git clone {that repo}
cd impacket
# then check pip command line to install it
```

Then he started a web server using `apache2`:

```sh
# viewed the tended ip addr, using
ifconfig # got eth0 => inet {ip}
# my WSL one is: 172.27.142.80 on kali
service apache2 start # then go to that inet ip
```

After creating a default server, he started `SSH` and `PSQL` using:

```sh
service ssh start
service postgresql start # because metasploit requires psql!
```

to persist our steps, we use systemctl enabling our  vendor preset on boot, check the system config course, line 1515 [here:](https://github.com/Bader-Idris/courses/tree/main/linux/system_configuration%26operation#managing-services-with-systemctl)

To distinguish between success/fail ping reqs, we need to view the second line saying `n bytes from {ip_addr}` as in:

```sh
ping -c 1 8.8.8.8
# PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
# 64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=47.3 ms

# fail says:
PING 168.1.1.9 (168.1.1.9) 56(84) bytes of data.

# --- 168.1.1.9 ping statistics ---
# 1 packets transmitted, 0 received, 100% packet loss, time 0ms
```

As we know, we can shorten our statement using grep and other great tools as:

```sh
ping -c 1 8.8.8.8 | grep 'bytes from' | sed -E 's/.* ([0-9]+\.[0-9]+\.[0-9]+\.[0-9]+):.*/\1/'
# and even sending it to a file using > filename

# or we can use cut as:
ping -c 1 8.8.8.8 | grep 'bytes from' | cut -d ' ' -f 4 | sed 's/:$//' > filename # it's expensive
# or use tr -d ":" instead of sed at last!
```
