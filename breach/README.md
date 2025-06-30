# Breach
This engagement aims to find a way to open the gate by bypassing the badge authentication system.
The control infrastructure may hold a weakness: Dig in, explore, and see if you have what it takes to exploit it.
Be sure to check all the open ports, you never know which one might be your way in!

![breach start](https://github.com/hw-hwh/2025-TryHackMe-CTF/blob/main/breach/images/image.webp)

# Flag
```
THM{s4v3_th3_d4t3_27_jun3}
```


  
# Write-up
**Step 1)** 타겟 서버에 대해 Nmap 스캔을 통해 정찰을 수행하였다. 스캔 결과 중 웹 서비스가 열려있었으며, vast-control과 관련된 1880번 포트가 열려있다.
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

  
  
**Step 2)** 웹 사이트에 접속하면 게이트가 닫혀있다는 페이지를 볼 수 있으며 /api/gate 에 접근하면 게이트의 상태를 가져오는거 같다.

![gate closed](https://github.com/hw-hwh/2025-TryHackMe-CTF/blob/main/breach/images/gateclose.webp)
```
{
  "image": "closed-b8ce334bae3faf976fa457702fe7545b.png",
  "status": "Gate CLOSED"
}
```


  
  

**Step 3)** 1880번 포트에 접근하면 IoT(사물 인터넷), 산업 제어 시스템, 홈 자동화를 위한 자동화 워크플로우를 구축하는 데 사용되는 오픈 소스 기반의 로우코드 흐름형 개발 도구인 Node-RED에 접속할 수 있다.

![1880port](https://github.com/hw-hwh/2025-TryHackMe-CTF/blob/main/breach/images/1880port.webp)
<br>

  
  

**Step 4)** /ui 에 접근하여 시스템 대쉬보드의 설정을 해제한다.

![ui](https://github.com/hw-hwh/2025-TryHackMe-CTF/blob/main/breach/images/ui.webp) 
<br>
<br>

**Step 5)** 대쉬보드 설정을 해제 후에 웹에 다시 접근하면 Flag 값을 알아낼수 있다.

![flag](https://github.com/hw-hwh/2025-TryHackMe-CTF/blob/main/breach/images/gateopen.webp)


