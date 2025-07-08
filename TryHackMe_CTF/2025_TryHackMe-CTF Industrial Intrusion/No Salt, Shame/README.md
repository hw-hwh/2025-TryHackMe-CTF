# No Salt, Shame [Crypto]
Virelia's gateway vendor "secured" the maintenance logs by encrypting all sensitive items with AES-CBC, using the plant's codename as the password and setting the IV to all zeros. Of course, without salting or integrity checking, there is only obscurity, not true security. The actual shutdown command is somewhere in the encrypted log.

![No Salt, Shame start]()
<br>

# Flag
```
THM{cbc_cl3ar4nce_gr4nt3d_10939}
```
<br>

# Write-up
**Step 1)** 문제 접근 해석
문제에서 주는 내용들을 해석해야한다.
- 유지 관리 로그를 '보안'하기 위해 Virelia의 게이트웨이 공급업체는 모든 중요 항목을 AES-CBC로 암호화했습니다.
**  -> AES-CBC 방식으로 로그 파일의 일부(중요한 항목)를 암호화했다는 뜻입니다.**
<br>

- 발전소의 코드명을 암호로 사용하고 IV는 0으로 고정했습니다.
**  -> 암호: VIRELIA-WATER-FAC ← 이게 암호화에 쓰인 비밀번호(passphrase) 또는 키(key) 라는 뜻
**  -> IV (Initialization Vector): 모든 블록에 대해 0x00으로 설정되었다는 것 → 취약함.
<br>

**Step 2)** 키 변환
문자열 "VIRELIA-WATER-FAC"의 SHA-256 해시값을 출력해야 한다.
<br>
```
echo -n "VIRELIA-WATER-FAC" | sha256sum

-> 9cfa5c575052bee2ac406f82dbbcae08a18edf6bba396b9be46231347cf8f959
```
<br>

IV (Initialization Vector)를 0으로 고정한다 =  IV를 b'\x00' * 16으로 지정했기 때문에 그런 결과가 나온 것
```
0x00 * 16 (16 bytes of 0)

-> 00000000000000000000000000000000

```
<br>

**Step 3)** flag 출력
```
sudo openssl enc -aes-256-cbc -d -in shutdown.log-1750934543756.enc -K 9cfa5c575052bee2ac406f82dbbcae08a18edf6bba396b9be46231347cf8f959 -iv 00000000000000000000000000000000
```
<br>
![flag]()
