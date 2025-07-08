# Chess Industry
The main goal was to gain initial user access, enumerate the system to discover valuable information, and ultimately escalate privileges to root.

![Chess Industry start](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/image.webp)
<br>

# Flag
```
# user
THM{bishop_to_c4_check}

#root
THM{check_check_check_mate}
```
<br>

# Write-up
**Step 1)** 정보 수집 단계
Nmap 스캔을 통해 타겟의 취약한정보를 수집한다. 스캔 결과를 보면 22, 79, 80번포트가 열려 있다.
<br>
![Nmap Scan](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/nmapscan.webp)
<br>

79번 포트 finger 서비스에 nc 명령어를 사용하여 대중적으로 사용하는 사용자로 접근을 시도한다. 
ubuntu와 root가 활성화 된 두 사용자라는 것을 확인했지만, 계정의 비밀번호를 크랙하기에는 어려워 보인다.
<br>
![ubuntu nc](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/nc%20ubuntu.webp)
![root nc](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/nc%20root.webp)
<br>

**Step 2)** 웹 페이지 계정 접근
80번 포트로 접근하면 웹 사이트가 존재한다. 웹 페이지에는 3개의 키워드를 언급하고 있다.
<br>
![WEB](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/web.webp)
<br>

3개의 계정을 NC 명령어를 통해 접근하면 fabiano 계정이 base64 인코딩 된 값이 확인 된다.
<br>
![base64](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/base64.webp)


**Step 3)** USER 권한 접근
확인된 fabiano 계정의 base64 디코딩을 하고 SSH 쉘 연결을 시도한다.
<br>
![base64 Decoding](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/base64%20Decoding.webp)
![ssh 로그인](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/ssh%20login.webp)
<br>

로그인을 완료 되면 user.txt 를 열람하면 flag 값을 확인할 수 있다.
<br>
![user flag](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/user%20flag.webp)
<br>

**Step 4)** root 권한 접근
fabiano 계정에서 "/usr/bin/python3.10 cap_setuid=ep" 설정이 되어 있다. 일반 사용자가 작성한 Python 스크립트가 setuid() 호출로 권한 상승을 할 수 있다.
<br>
![root get](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/root%20%EC%A0%91%EA%B7%BC.webp)
<br>

```
/usr/bin/python3.10 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```
- os.setuid(0) : 현재 프로세스의 UID를 0 (root)으로 변경
- os.system("/bin/bash") : 쉘 실행 (UID가 이미 root이므로 root 쉘로 진입)

![root shell](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/root%20shell.webp)
<br>

![root flag](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Chess%20Industry/images/rootflag.webp)
<br>
  
