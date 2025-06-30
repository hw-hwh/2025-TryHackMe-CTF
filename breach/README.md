# Breach
This engagement aims to find a way to open the gate by bypassing the badge authentication system.
The control infrastructure may hold a weakness: Dig in, explore, and see if you have what it takes to exploit it.
Be sure to check all the open ports, you never know which one might be your way in!

![breach start](https://github.com/hw-hwh/2025-TryHackMe-CTF/blob/main/breach/images/image.webp)


# Write-up
Reconnaissance must be conducted on the target server using an Nmap scan. Among the scan results, a web service is accessible, and port 1880, associated with vast-control, stands out as particularly noteworthy.
```
root@ip-10-10-119-24:~# nmap -sS 10.10.78.197 -p- -T4
Starting Nmap 7.80 ( https://nmap.org ) at 2025-06-27 14:37 BST
Nmap scan report for ip-10-10-78-197.eu-west-1.compute.internal (10.10.78.197)
Host is up (0.00033s latency).
Not shown: 65528 closed ports
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
102/tcp   open  iso-tsap
502/tcp   open  mbap
1880/tcp  open  vsat-control
8080/tcp  open  http-proxy
44818/tcp open  EtherNetIP-2
MAC Address: 02:52:83:5E:E3:5F (Unknown)
```

Accessing the website reveals a page indicating that the gate is closed.

