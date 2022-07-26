# 깃특강 2일차!
## 오늘 배운 내용  
1. .gitignore
2. clone, pull
3. Branch
4. Branch-merge
---
### .gitignore  
1. .gitignore란?  
특정 파일 혹은 폴더에 대해 Git이 버전 관리를 하지 못하도록 지정하는 것  

2. **작성시 주의사항**

   - 반드시 이름을 `.gitignore`로 작성합니다. 앞의 점(.)은 숨김 파일이라는 뜻입니다.
   - `.gitignore` 파일은 `.git` 폴더와 동일한 위치에 생성합니다.
   - **제외 하고 싶은 파일은 반드시 `git add` 전에 `.gitignore`에 작성합니다.**

3. .gitignore를 쉽게 작성하게 도와주는 사이트  
   *https://www.toptal.com/developers/gitignore/
   *https://github.com/github/gitignore

4. 패턴 예시
```shell
# .gitignore


# 확장자가 txt인 파일 무시
*.txt

# 현재 확장자가 txt인 파일이 무시되지만, 느낌표를 사용하여 test.txt는 무시하지 않음
!test.txt

# 현재 디렉터리에 있는 TODO 파일은 무시하고, folder/TODO 처럼 하위 디렉터리에 있는 파일은 무시하지 않음
/TODO

# build/ 디렉터리에 있는 모든 파일은 무시
build/

# folder/notes.txt 파일은 무시하고 folder/child/arch.txt 파일은 무시하지 않음
folder/*.txt

# folder 디렉터리 아래의 모든 .pdf 파일을 무시
folder/**/*.pdf
```
---
### clone,pull
1. git clone  
- 원격 저장소의 커밋 내역을 모두 가져와서, 로컬 저장소를 생성하는 명령어
 - clone은 `"복제"`라는 뜻으로, `git clone` 명령어를 사용하면 원격 저장소를 통째로 복제해서 내 컴퓨터에 옮길 수 있다.
 - `git clone <원격 저장소 주소>`의 형태로 작성한다.

2. git pull
 - 원격 저장소의 변경 사항을 가져와서, 로컬 저장소를 업데이트하는 명령어
 - 로컬 저장소와 원격 저장소의 내용이 완전 일치하면 git pull을 해도 변화가 일어나지 않습니다.
 - `git pull <저장소 이름> <브랜치 이름>`의 형태로 작성합니다.

**git clone과 git pull이 헷갈린다면?**

* git clone은 git init처럼 처음에 한 번만 실행한다다. 즉 로컬 저장소를 만드는 역할이다.
단, git init처럼 직접 로컬 저장소를 만드는 게 아니라, Github에서 저장소를 복제해서 내 컴퓨터에 똑같은 복제본을 만든다는 차이가 있다.

* git pull은 git push처럼 로컬 저장소와 원격 저장소의 내용을 동기화하고 싶다면 언제든 사용한다. 단, push는 로컬 저장소의 변경 내용을 원격 저장소에 반영하는 것이고, pull은 원격 저장소의 변경 내용을 로컬 저장소에 반영하는 것이다. 즉 방향이 다르다!
---
### Branch
![Branch](https://hphk-edu.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd6378065-5864-4832-8122-0fde3eb4f6ec%2FUntitled.png?table=block&id=d2787492-5d56-4aca-bf02-314e208fec67&spaceId=f7ab64f0-6613-4035-b609-06b6865d9b61&width=1940&userId=&cache=v2)
#### Branch란?
- Branch는 `나뭇가지`라는 뜻의 영어 단어.
- 즉 `브랜치`란 나뭇가지처럼 여러 갈래로 작업 공간을 나누어 **독립적으로 작업**할 수 있도록 도와주는 Git의 도구이다.

1.git branch  
* 브랜치 조회, 생성, 삭제 등 브랜치와 관련된 Git 명령어

```bash
# 브랜치 목록 확인
$ git branch

# 원격 저장소의 브랜치 목록 확인
$ git branch -r

# 새로운 브랜치 생성
$ git branch <브랜치 이름>

# 특정 커밋 기준으로 브랜치 생성
$ git branch <브랜치 이름> <커밋 ID>

# 특정 브랜치 삭제
$ git branch -d <브랜치 이름> # 병합된 브랜치만 삭제 가능
$ git branch -D <브랜치 이름> # (주의) 강제 삭제 (병합되지 않은 브랜치도 삭제 가능)
```
2. git switch

* 현재 브랜치에서 다른 브랜치로 HEAD를 이동시키는 명령어
* HEAD란 현재 브랜치를 가리키는 포인터를 의미한다.
```bash
   # 다른 브랜치로 이동
$ git switch <다른 브랜치 이름>

# 브랜치를 새로 생성과 동시에 이동
$ git switch -c <브랜치 이름>

# 특정 커밋 기준으로 브랜치 생성과 동시에 이동
$ git switch -c <브랜치 이름> <커밋 ID>
```
***※git switch하기전에 해당 브랜치의 변경사항을 무조건 commit할 것!***

---
### Branch merge
1. git merge
- 분기된 브랜치들을 하나로 합치는 명령어
- `git merge <합칠 브랜치 이름>`의 형태로 사용한다.
- **Merge하기 전에 일단 다른 브랜치를 합치려고 하는, 즉 메인 브랜치로 switch 해야한다.**
    
    ```bash
    # 1. 현재 branch1과 branch2가 있으며, HEAD가 가리키는 곳은 branch1 이다.
    $ git branch
    * branch1
      branch2
    
    # 2. branch2를 branch1에 합치려면?
    $ git merge branch2
    
    # 3. branch1을 branch2에 합치려면?
    $ git switch branch2
    $ git merge branch1
    ```

2. merge conflict 
- 병합하는 두 브랜치에서 `같은 파일의 같은 부분`을 수정한 경우, Git이 어느 브랜치의 내용으로 작성해야 하는지 판단하지 못해서 발생하는 충돌(Conflict) 현상
- 결국은 사용자가 직접 내용을 선택해서 Conflict를 해결해야 한다.  
* 충돌 내용을 살펴보고 원하는 것을 고른뒤에 git add와 git commit을 꼭 해서 저장해줘야 한다!!

