오늘 배웠던 내용에 대해 MD파일로 작성해보는 시간
## Git 초기설정
1. 작성자 이름, 메일 등록
- 커밋 기록을 남겼는지 확인할수 있도록 초기 설정.
```python
git config --global user.name "이름" 
git config --global user.email "메일 주소"
```

2. 확인
```python
git config --global -l
```
## 기본 명령어
0. 로컬 저장소
- Working Directory (= Working Tree) : 사용자의 일반적인 작업이 일어나는 곳
- Staging Area (= Index) : 커밋을 위한 파일 및 폴더가 추가되는 곳
- Repository : staging area에 있던 파일 및 폴더의 변경사항(커밋)을 저장하는 곳
- Git은 Working Directory → Staging Area → Repository 의 과정으로 버전 관리를 수행합니다.

1. 디렉토리를 Git으로 관리하는 명령어

    `**일반 폴더 -> 로컬 저장소**`
``` python
git init
Initialized empty Git repository in C:/Users/kyle/git-practice/.git/

kyle@KYLE MINGW64 ~/git-practice (master) 
```
- 터미널에 이미 (master)가 있다면, git init을 절대 입력하면 안됩니다.

2. 파일 현재 상태 확인

    `**버전 상태 출력**`
```python
git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   git_day00.md
        modified:   git_day01.md
```
- `Untracked` : Git이 관리하지 않는 파일 (한번도 Staging Area에 올라간 적 없는 파일)
- `Tracked`: Git이 관리하는 파일
    - `Unmodified` : 최신 상태
    - `Modified` : 수정되었지만 아직 Staging Area에는 반영하지 않은 상태
    - `Staged` : Staging Area에 올라간 상태

3. Working Directory -> Staging Area로 올리는 명령어

    `**Working Directory -> Staging Area**`
```python
# 특정 파일
 git add a.txt

# 특정 폴더
git add my_folder/

# 현재 디렉토리에 속한 파일/폴더 전부
 git add 
```
- Git이 해당 파일을 추적(관리)할 수 있도록 만듭니다.
- Untracked, Modified → Staged 로 상태를 변경합니다.

4. Staging Area에 올라온 파일의 변경 사항을 하나의 버전(커밋)으로 저장하는 명령어

    `**staging Area -> Commits**`
```python
git commit -m "first commit"
[master (root-commit) c02659f] first commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.tx
 ```
-  "first commit" 사용목적에 맞게 이름 설정
- 커밋 메세지는 현재 변경 사항들을 잘 나타낼 수 있도록 의미 있게 작성하는 것을 권장합니다.

5. 커밋의 내역(ID, 작성자, 시간, 메세지 등)을 조회할 수 있는 명령어

    `**comits 목록 출력**`
```python
git log --oneline
eeb0a45 (HEAD -> master, origin/master) first day
5e21088 git_day01
9266d3c first commit
```
- --oneline : 한 줄로 축약해서 보여줍니다.
- --all : 현재 브랜치를 포함한 모든 브랜치의 내역을 보여줍니다.
- -p : 파일의 변경 내용도 같이 보여줍니다
- --reverse : 커밋 내역의 순서를 반대로 보여줍니다. (최신이 가장 아래)
