# Description
There is a web server on port :80 protected with Port Knocking. Find the one "knock" needed (sending a SYN to a single port, not a sequence) so you can curl localhost

## Process
Simulate Port Knocking on all ports
```
admin@i-049db4ecadaf1c67e:~$ nmap -Pn -p 1000-8888 --host-timeout 201 --max-retries 0 localhost
Starting Nmap 7.80 ( https://nmap.org ) at 2024-12-02 07:01 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00021s latency).
Not shown: 7887 closed ports
PORT     STATE SERVICE
6767/tcp open  bmc-perf-agent
8080/tcp open  http-proxy

Nmap done: 1 IP address (1 host up) scanned in 0.20 seconds
```

Check if Port 80 is Open
```
admin@i-049db4ecadaf1c67e:~$ nmap -p 80 localhost
Starting Nmap 7.80 ( https://nmap.org ) at 2024-12-02 07:01 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00012s latency).

PORT   STATE SERVICE
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.04 seconds
```

Get message from `curl localhost`
```
admin@i-049db4ecadaf1c67e:~$ curl localhost
Who is there?
```
