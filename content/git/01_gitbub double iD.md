  
  
## 문제 상황  
  
  
`git push` 시 아래 에러 발생:  
  
```  
Permission denied to ASOTEA  
```  
  
**원인:** 저장소는 Rigeltea 계정인데, remote가 HTTPS 방식이라 Windows에 저장된 ASOTEA 계정으로 인증되기 때문.  
  
---  
  
## 설정 순서  
  
### 1. Rigeltea 전용 SSH 키 생성  
  
```bash  
ssh-keygen -t ed25519 -C "Rigeltea 이메일" -f %USERPROFILE%\.ssh\id_ed25519_rigeltea  
```  
  
> passphrase는 초보자라면 Enter로 넘어가도 무방.  
  
생성 결과:  
  
|파일|의미|  
|---|---|  
|`id_ed25519_rigeltea`|비밀키 (private key)|  
|`id_ed25519_rigeltea.pub`|공개키 (public key)|  
  
---  
  
### 2. GitHub에 공개키 등록  
  
공개키 출력:  
  
```bash  
type %USERPROFILE%\.ssh\id_ed25519_rigeltea.pub  
```  
  
GitHub → `Settings` → `SSH and GPG keys` → `New SSH key` → 붙여넣기  
  
---  
  
### 3. SSH Config 설정  
  
파일 위치: `C:\Users\{이름}\.ssh\config`  
  
```ssh-config  
Host github-rigeltea  
  HostName github.com  User git  IdentityFile ~/.ssh/id_ed25519_rigeltea  IdentitiesOnly yes```  
  
> `git@github-rigeltea:...` 주소를 사용하면 자동으로 Rigeltea SSH 키로 인증됨.  
  
---  
  
### 4. SSH 연결 테스트  
  
```bash  
ssh -T github-rigeltea  
```  
  
성공 시:  
  
```  
Hi Rigeltea! You've successfully authenticated  
```  
  
---  
  
### 5. Remote 주소 변경 (HTTPS → SSH)  
  
기존 HTTPS 확인:  
  
```bash  
git remote -v  
# https://github.com/Rigeltea/저장소명.git  
```  
  
SSH로 변경:  
  
```bash  
git remote set-url origin git@github-rigeltea:Rigeltea/저장소명.git  
```  
  
> **이 설정은 저장소마다 1번만 하면 된다.**  
  
---  
  
### 6. 커밋 작성자 설정  
  
저장소 내부에서 (`--global` 없이) 설정:  
  
```bash  
# Rigeltea 저장소  
git config user.name "Rigeltea"  
git config user.email "Rigeltea@email.com"  
  
# ASOTEA 저장소  
git config user.name "ASOTEA"  
git config user.email "ASOTEA@email.com"  
```  
  
---  
  
## Remote 주소 규칙  
  
```  
# ASOTEA → 기본 키 사용  
git@github.com:ASOTEA/저장소명.git  
  
# Rigeltea → 전용 키 사용  
git@github-rigeltea:Rigeltea/저장소명.git  
```  
  
---  
  
## 새 프로젝트 시작 템플릿  
  
### ASOTEA  
  
```bash  
cd C:\...\01_ASOTEA  
git clone git@github.com:ASOTEA/저장소명.git  
cd 저장소명  
git config user.name "ASOTEA"  
git config user.email "ASOTEA@email.com"  
```  
  
### Rigeltea  
  
```bash  
cd C:\...\02_Rigeltea  
git clone git@github-rigeltea:Rigeltea/저장소명.git  
cd 저장소명  
git config user.name "Rigeltea"  
git config user.email "Rigeltea@email.com"  
```