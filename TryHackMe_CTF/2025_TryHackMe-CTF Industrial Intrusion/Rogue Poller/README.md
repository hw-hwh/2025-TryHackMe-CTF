# Rogue Poller
An intruder has breached the internal OT network and systematically probed industrial devices for sensitive data. Network captures reveal unusual traffic from a suspicious host scanning PLC memory over TCP port 502.

Analyse the provided PCAP and uncover what data the attacker retrieved during their register scans.
![Rogue Poller start](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Rogue%20Poller/images/image.webp)
<br>

# Flag
```
THM{inDu5tr14L_r3g1st3rs}
```
<br>

# Write-up
**Step 1)** 문제 접근
침입자가 내부 OT 네트워크에 침입했는데 TCP 포트 502를 통해 PLC 메모리를 스캔한것으로 보인다.
502번 포트는 Modbus 프로토콜이다. 제공된 PCAP에서 Modbus 프로토콜 통신을 확인해 본다.
<br>
```
tcp.port == 502 && modbus
```
<br>

![modbus search](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Rogue%20Poller/images/modbus%20search.webp)
<br>

**Step 2)** 통신한 Flag 값 확인
Modbus 프로토콜의 패킷을 TCP 스트림을 통해 확인하면 줄마다 나눠지는 Flag값 형태를 확인할 수 있다.
<br>
![flag check](https://github.com/hw-hwh/CTF/blob/main/TryHackMe_CTF/2025_TryHackMe-CTF%20Industrial%20Intrusion/Rogue%20Poller/images/flag%20check.webp)
