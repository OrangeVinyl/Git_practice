# Git_practice

# # git 생성

해당 폴더에서(VS Code 터미널 기본) 아래 명령어 입력

`git init`

폴더에 숨김모드로 **.git** 폴더 생성 확인

- 🛑 이 폴더를 지우면 Git 관리내역이 삭제됩니다. (현 파일들은 유지)
- 맥에서 숨김 파일 보기: `command` + `shift` + `.`

### **❗️ 모든 작업(파일 생성, 수정)마다 파일을 꼭 저장**

터미널에 아래 명령어 입력

`git status`

# # gitignore

## **Git의 관리에서 특정 파일/폴더를 배제해야 할 경우**

### **a. 포함할 필요가 없을 때**

- 자동으로 생성 또는 다운로드되는 파일들 (빌드 결과물, 라이브러리)

### **b. 포함하지 말아야 할 때**

- 보안상 민감한 정보를 담은 파일

### **.gitignore 파일을 사용해서 배제할 요소들을 지정**

`.gitignore 파일 생성 후 파일 이름 삽입`

```yaml
.gitignore 파일 안에 작성 
# 이렇게 #를 사용해서 주석

# 모든 file.c
file.c

# 최상위 폴더의 file.c
/file.c

# 모든 .c 확장자 파일
*.c

# .c 확장자지만 무시하지 않을 파일
!not_ignore_this.c

# logs란 이름의 파일 또는 폴더와 그 내용들
logs

# logs란 이름의 폴더와 그 내용들
logs/

# logs 폴더 바로 안의 debug.log와 .c 파일들
logs/debug.log
logs/*.c

# logs 폴더 바로 안, 또는 그 안의 다른 폴더(들) 안의 debug.log
logs/**/debug.log
```

# # Add / Commit

## **프로젝트의 변경사항들을 타임캡슐(버전)에 담기**

변경사항 확인

`git status`

- 추적하지 않는(**untracked**) 파일: Git의 관리에 들어간 적 없는 파일

파일 하나 담기

`git add tigers.yaml`

모든 파일 담기

`git add .`

---

## **타임캡슐 묻기**

아래 명령어로 **commit**

`git commit`

- Vi 입력 모드로 진입
    
    
    | 작업 | Vi 명령어 | 상세 |
    | --- | --- | --- |
    | 입력 시작 | i | 명령어 입력 모드에서 텍스트 입력 모드로 전환 |
    | 입력 종료 | ESC | 텍스트 입력 모드에서 명령어 입력 모드로 전환 |
    | 저장 없이 종료 | :q |  |
    | 저장 없이 강제 종료 | :q! | 입력한 것이 있을 때 사용 |
    | 저장하고 종료 | :wq | 입력한 것이 있을 때 사용 |
    | 위로 스크롤 | k | git log등에서 내역이 길 때 사용 |
    | 아래로 스크롤 | j | git log등에서 내역이 길 때 사용 |

깃 활동내역 확인

`git log`

- 종료는 `:q`

---

## **다음 변경사항들을 만들고 타임캡슐에 묻기**

- `git status`로 확인
    - 파일의 **추가**, **변경**, **삭제** 모두 내역으로 저장할 대상
- `git diff`로 확인
    
    
    | 작업 | Vi 명령어 | 상세 |
    | --- | --- | --- |
    | 위로 스크롤 | k | git log등에서 내역이 길 때 사용 |
    | 아래로 스크롤 | j | git log등에서 내역이 길 때 사용 |
    | 끄기 | :q | :가 입력되어 있으므로 q만 눌러도 됨 |

### **캡슐에 담기**

`git add .`

- `git status`로 확인

`git commit -m "example"`

### **💡 TIP `add`와 `commit` 한꺼번에**

`git commit -am "(메시지)"`

- 🛑 새로 추가된(untracked) 파일이 없을 때 한정

# # Reset / Revert

## **reset 사용해서 과거로 돌아가기**

아래 명령어로 커밋 내역 확인

`git log`

- 되돌아갈 시점: `Add team Cheetas`의 커밋 해시 복사
- `:q`로 빠져나가기

`git reset --hard (돌아갈 커밋 해시)`

---

## **reset 하기 전 시점으로 복원해보기**

백업해 둔 **.git** 폴더 사용

- `.git` 폴더 복원
- `git log`, `git status`로 상태 확인
- 아래 명령어로 현 커밋 상태로 초기화

`git reset --hard`

- 💡 뒤에 커밋 해시가 없으면 마지막 커밋을 가리킴

---

## **revert 로 과거의 커밋 되돌리기**

`Add George to Tigers`의 커밋 해시 구하기

아래 명령어로 **revert**

`git revert (되돌릴 커밋 해시)`

- `:wq`로 커밋 메시지 저장

### **🎯 `Replace Lions with Leopards`의 커밋 되돌려보기**

- 이후 `leopards.yaml` 수정한 내역 때문에 충돌
    - `git rm leopards.yaml`로 Git에서 해당 파일 삭제
    - `git revert --continue`로 마무리
    - `:wq`로 커밋 메시지 저장

### **🎯 reset 사용해서 revert 전으로 되돌아가기**

### **💡 커밋해버리지 않고 revert하기**

`git revert --no-commit (되돌릴  커밋 해시)`

- 원하는 다른 작업을 추가한 다음 함께 커밋
- 취소하려면 `git reset --hard`

# # Brach

지울 브랜치에 다른 브랜치로 적용되지 않는 내용이 커밋이 있을 시에는 -D(대문자) 옵션으로 강제 삭제합니다.

- `git branch -D(브랜치명)`

## **브랜치 생성 / 이동 / 삭제하기**

`add-coach`란 이름의 브랜치 생성

`git branch add-coach`

브랜치 목록 확인

`git branch`

`add-coach` 브랜치로 이동

`git switch add-coach`

- `checkout` 명령어가 Git 2.23 버전부터 `switch`, `restore`로 분리

### **💡 브랜치 생성과 동시에 이동하기**

`git switch -c new-teams`

- 기존의 `git checkout -b (새 브랜치명)`

### **🗑 브랜치 삭제하기**

`git branch -d (삭제할 브랜치명)`

- `to-delete`란 브랜치 만들고 삭제해보기

지워질 브랜치에만 있는 내용의 커밋이 있을 경우즉 다른 브랜치로 가져오지 않은 내용이 있는 브랜치를 지울 때는`-d` 대신 `-D`(대문자)로 강제 삭제해야 합니다.

`git branch -D (강제삭제할 브랜치명)`

### **✏️ 브랜치 이름 바꾸기**

`git branch -m (기존 브랜치명) (새 브랜치명)`

---

## **결과 살펴보기**

`git log`: 위치한 브랜치에서의 내역만 볼 수 있음

여러 브랜치의 내역 편리하게 보기

`git log --all --decorate --oneline --graph`

### **소스트리에서 확인**

![https://www.yalco.kr/images/lectures/git-github/3-1/3-branches.png](https://www.yalco.kr/images/lectures/git-github/3-1/3-branches.png)

# # Branch 합치기

### **서로 다른 브랜치를 합치는 두 방식**

- **merge** : 두 브랜치를 한 커밋에 이어.
    - 브랜치 사용내역을 남길 필요가 있을 때 적합한 방식입니다.
    - 다른 형태의 merge에 대해서도 이후 다루게 될 것입니다.
- **rebase** : 브랜치를 다른 브랜치에 이어.
    - 한 줄로 깔끔히 정리된 내역을 유지하기 원할 때 적합합니다.
    - 이미 팀원과 공유된 커밋들에 대해서는 사용하지 않는 것이 좋습니다.

## **merge로 합치기**

`add-coach` 브랜치를 `main` 브랜치로 **merge**

- `main` 브랜치로 이동
- 아래의 명령어로 병합

`git merge add-coach`

- `:wq`로 자동입력된 커밋 메시지 저장하여 마무리(맥에서만 사용)
- 소스트리에서 확인

## **💡 `merge`는 `reset`으로 되돌리기 가능**

- `merge`도 하나의 커밋
- `merge`하기 전 해당 브랜치의 마지막 시점으로

## **병합된 브랜치는 삭제**

삭제 전 소스트리에서 `add-coach` 위치 확인

`git branch -d add-coach`

---

## **rebase로 합치기**

`new-teams` 브랜치를 `main` 브랜치로 **rebase**

- `new-teams` 브랜치로 이동
    - 🛑 `merge`때와는 반대!
- 아래의 명령어로 병합

`git rebase main`

- 소스트리에서 상태 확인
    - `main` 브랜치는 뒤쳐져 있는 상황
- `main` 브랜치로 이동 후 아래 명령어로 `new-teams`의 시점으로 **fast-forward**

`git merge new-teams`

- `new-teams` 브랜치 삭제

# # 충돌 해결하기

## **브랜치 간 충돌**

- 파일의 같은 위치에 다른 내용이 입력된 상황

---

## **`merge` 충돌 해결하기**

`git merge conflict-1`로 병합을 시도하면 충돌 발생

- 오류 메시지와 `git status` 확인
- VS Code에서 해당 부분 확인

### **아래 기능 사라짐 *노랗게 표시한 부분***

![https://www.yalco.kr/images/lectures/git-github/3-4/vs-code.png](https://www.yalco.kr/images/lectures/git-github/3-4/vs-code.png)

당장 충돌 해결이 어려울 경우 아래 명령어로 `merge` 중단

`git merge --abort`

해결 가능 시 충돌 부분을 수정한 뒤 `git add .`, `git commit`으로 병합 완료

---

## **`rebase` 충돌 해결하기**

`conflict-2`에서 `git rebase main`로 리베이스 시도하면 충돌 발생

- 오류 메시지와 `git status` 확인
- VS Code에서 해당 부분 확인

당장 충돌 해결이 어려울 경우 아래 명령어로 `rebase` 중단

`git rebase --abort`

### **해결 가능 시**

- 충돌 부분을 수정한 뒤 `git add .`
- 아래 명령어로 계속

`git rebase --continue`

- 충돌이 모두 해결될 때까지 반복

`main`에서 `git merge conflict-2`로 마무리

`conflict-1`, `conflict-2` 삭제

## 소스코드로 만들기

## **브랜치 만들고 `merge`, `rebase` 하기**

1. `to-merge`, `to-rebase` 브랜치 생성
    - 상단의 `브랜치` 버튼 클릭
    - 왼쪽의 브랜치 탭에서 클릭하여 이동
2. `main` 브랜치
    - Tigers의 `manager`를 `Brenda`로 변경
    - 커밋 메시지: `Edit Tigers manager`
3. `to-merge` 브랜치
    - Tigers의 `coach`를 `Ruth`로 변경
    - 커밋 메시지: `Edit Tigers coach`
4. `to-rebase` 브랜치
    - Tigers의 `memebers`에 `Tyler` 추가
    - 커밋 메시지: `Edit Tigers members`

### **⭐️ 브랜치를 이동하며 파일 살펴보기**

1. `to-merge` 브랜치 `main`으로 `merge`
    - `main`에 위치한 뒤 `to-merge` 브랜치를 우클릭하여 `Merge ...` 클릭
2. `to-rebase` 브랜치 `main`으로 `rebase`
    - `to-rebase`에 위치한 뒤 `main` 브랜치를 우클릭하여 `... 재배치` 클릭
    - `main`에 위치한 뒤 `to-rebase` 브랜치를 우클릭하여 `Merge ...` 클릭
3. `main`으로 이동 후 `to-merge`와 `to-rebase` 우클릭하여 삭제
    - `merge`되지 않은 브랜치의 경우 `강제 삭제` 체크박스 선택

---

## **`merge` 충돌 해결해보기**

💡 `rebase`는 충돌 가능시 CLI로 진행 권장

1. `conflict` 브랜치 생성
2. `main` 브랜치
    - Tigers의 `members`에 `Kim` 추가
    - 커밋 메시지: `Edit Kim to Tigers`
3. `conflict` 브랜치
    - Tigers의 `members`에 `Park` 추가
    - 커밋 메시지: `Edit Park to Tigers`
4. `merge`하여 충돌 해결해보기
5. `conflict` 브랜치 삭제

# # 원격저장소 사용하기(GitHub)

## **로컬에 원격 저장소 추가 후 Push**

### **GitHub 레포지토리 생성 후 복붙 명령어**

`git remote add origin (원격 저장소 주소)`

- 로컬의 Git 저장소에 원격 저장소로의 연결 추가
    - 원격 저장소 이름에 흔히 `origin` 사용. 다른 것으로 수정 가능

`git branch -M main`

- GitHub 권장 - 기본 브랜치명을 `main`으로

`git push -u origin main`

- 로컬 저장소의 커밋 내역들 원격으로 `push`(업로드)
    - `u` 또는 `-set-upstream` : 현재 브랜치와 명시된 원격 브랜치 기본 연결

### **⭐️ GitHub의 해당 레포지토리 페이지 새로고침하여 살펴보기**

- 파일들 내용
- 커밋 내역들

원격 목록 보기

`git remote`

- 자세히 보기: `git remote -v`

원격 지우기 (로컬 프로젝트와의 연결만 없애는 것. GitHub의 레포지토리는 지워지지 않음)

`git remote remove (origin 등 원격 이름)`

---

## **GitHub에서 프로젝트 다운받기**

- `Download ZIP`: 파일들만 다운받음, Git 관리내역 제외
- Git **clone**: Git 관리내역 포함 다운로드

### **터미널이나 Git Bash에서 대상 폴더 이동 후**

`git clone (원격 저장소 주소)`

- 이번 강에서는 **HTTPS** 프로토콜 사용
- VS Code로 해당 폴더 열어보기

# # Push & Pull

<aside>
💡 Git 충돌 발생시, 충돌 사항 변경  후, git add .  > git commit 입력 하면 해결 된다.

</aside>

<aside>
💡 협업 상황에서 rebase를 쓰지말라 함은, 로컬에서 작업할때 뭔가 공유된 것들을 rebase해서 올리지 말라 한 것! (뭔가를 pull 받는 상황에서 rebase 하는 것은 괜찮다.)

</aside>

## **원격으로 커밋 밀어올리기(push)**

`git push`

- 이미 `git push -u origin main`으로 대상 원격 브랜치가 지정되었기 때문에 가능

---

## **원격의 커밋 당겨오기(pull)**

`git pull`

 - 로컬에서 파일과 로그 살펴보기

---

## **3. pull 할 것이 있을 때 push를 하면?**

1. **로컬에서** Leopards의 `manager`를 `Dooli`로 수정
    - 커밋 메시지: `Edit Leopards manager`
2. **GitHub에서** Leopards의 `coach`를 `Lupi`로 수정
    - 커밋 메시지: `Edit Leopards coach`
3. push 해보기
    - 원격에 먼저 적용된 새 버전이 있으므로 적용 불가
    - pull 해서 원격의 버전을 받아온 다음 push 가능
4. push 할 것이 있을 시 pull 하는 두 가지 방법
    - `git pull --no-rebase` - **merge** 방식
        - 소스트리에서 확인해보기
        - `reset`으로 되돌린 다음 아래 방식도 해보기
    - `git pull --rebase` - **rebase** 방식
        - pull 상의 rebase는 다름 (협업시 사용 OK) > 2번째 콜아웃 내용
5. push하기

### 

---

## **4. 협업상 충돌 발생 해결하기**

1. **로컬에서** Panthers에 `Maruchi` 추가
    - 커밋 메시지: `Add Maruchi to Panthers`
2. **원격에서** Panthers에 `Arachi` 추가
    - 커밋 메시지: `Add Arachi to Panthers`
3. pull 하여 충돌상황 마주하기
    - `-no-rebase`와 `-rebase` 모두 해 볼 것
    

---

## **5. 로컬의 내역 강제 push해보기**

1. 로컬의 내역 충돌 전으로 `reset`
2. 아래 명령어로 원격에 강제 적용

# # remote branch 다루기

## **로컬에서 브랜치 만들어 원격에 push 해보기**

아래와 같이 하면 대상을 명시하라는 메시지 나타남

`git push`

아래 명령어로 원격의 브랜치 명시 및 기본설정

`git push -u origin from-local`

1. 브랜치 목록 살펴보기
    - GitHub에서 목록 보기
    - 아래 명령어로 로컬과 원격의 브랜치들 확
        
        `git branch --all`
        

---

## **원격의 브랜치 로컬에 받아오기**

1. GitHub에서 `from-remote` 브랜치 만들기
    - `git branch -a`에서 현재는 보이지 않음
2. 아래 명령어로 원격의 변경사항 확인
    
    `git fetch`
    
    - `git branch -a`로 확인
3. 아래 명령어로 로컬에 같은 이름의 브랜치를 생성하여 연결하고 switch
    
    `git switch -t origin/from-remote`
    

## **3. 원격의 브랜치 삭제**

`git push 원격 이름 --delete 원격의 브랜치명`
