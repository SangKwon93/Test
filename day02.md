# 2일차 정리


## **1. git clone <내 컴퓨터에 복사본>**
 - 원격 저장소의 커밋 내역을 모두 가져와서, 로컬 저장소를 생성하는 명령어
 - 원격 저장소 -> 내 컴퓨터   
 **형태** : **git clone 주소url**
```python
git clone https://github.com/SangKwon93/TIL.git
Cloning into 'TIL'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```  
-> **`git init`과 `git remote add`는 이미 수행완료!!**  
  

## **2. git pull <로컬 저장소와 원격저장소 동기화>**
 - 원격 저장소(변경사항)-> 로켈 저장소 업데이트
 **형태** : **git<저장소 이름><브랜치 이름>**
 ```python
 $ git pull origin master
From https://github.com/edukyle/git-practice
 * branch            master     -> FETCH_HEAD
Updating 6570ecb..56809a9
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
 ```
-> origin이라는 원격 저장소의 master 브랜치의 내용을 가져온다.    
## **3. git branch**
- 브랜치 조회,생성,삭제 등과 관련된 Git 명령어 
- 나뭇가지처럼 여러 작업 공간을 나누어 독립적으로 작업할 수 있게 도와주는 공간.
- 사용이유 : 브랜치는 독립 공간이라 원본(master)이 안전. 
```python
# 브랜치 목록 확인
  git branch

# 원격 저장소의 브랜치 목록 확인
  git branch -r

# 새로운 브랜치 생성
 git branch <브랜치 이름>

# 특정 커밋 기준으로 브랜치 생성
 git branch <브랜치 이름> <커밋 ID>

# 특정 브랜치 삭제
  git branch -d <브랜치 이름> # 병합된 브랜치만 삭제 가능
  git branch -D <브랜치 이름> # (주의) 강제 삭제 (병합되지 않은 브랜치도 삭제 가능)
```

## **4. git switch**
- 현재 브랜치에서 다른 브랜치로 이동시키는  명령어

```python
$ git switch <다른 브랜치 이름>
```
- git switch -c <브랜치 이름> :
브랜치를 새로 생성과 동시에 이동

- git switch -c <브랜치 이름> <커밋 ID> :
 특정 커밋 기준으로 브랜치 생성과 동시에 이동

## **5. Branch Merge**
- 분리된 브랜치 공간을 하나로 합치는 명령어
- **형태** : **git merge <합칠 브랜치 이름>**
- Merge하기 전에 일단 다른 브랜치를 합치려고 하는, 즉 메인 브랜치로 switch 해야합니다.

``` python

# 1.HEAD가 가리키는 곳은 branch1 입니다.
  git branch
* branch1
  branch2

# 2. branch2를 branch1에 합친다.
  git merge branch2

# 3. branch1을 branch2에 합친다.
  git switch branch2
  git merge branch1
``` 
## **6. Git workflow**
**1> 원격 저장소 소유권이 있는 경우** 
- 원격 저장소가 자신의 소유이거나 collaborator로 등록되어 있는 경우
- master에 직접 개발하는 것이 아니라, 기능별로 브랜치를 따로 만들어서 개발
- Pull Request를 같이 사용하여 팀원 간 변경 내용에 대한 소통을 진행

1) 소유권이 있는 원격 저장소-> 로컬 저장소로 clone

``` python
git clone https://github.com/SangKwon93/TIL.git
```

2) 사용자는 내 작업할 공간 브랜치를 생성 및 기능 구현

``` python
git switch - c SangKwon93
```

3) 기능 구현 완료 후 원격저장소에 해당 브랜치 `push`
``` python
git push origin SangKwon93
```

4) 원격 저장소에 master와 각 기능 브랜치 반영

5) Pull Request를 통해 브랜치를 master에 반영해달라는 요청을 보냄
(팀원과 코드리뷰 소통 가능)

6) 병합 완료되면 원격 저장소에서 병합이 완료된 브랜치는 삭제(불필요)

7) master에 브랜치가 병합되면 각 사용자는 로컬의 master 브랜치로 이동
```python
git switch master
```
8) 병합으로 인해 변경된 원격 저장소의 master 내용을 로컬저장소에 받아온다.

```python
git pull origin master
```
9) 병합이 완료된 master의 내용을 받았으면 기존 로컬 브랜치는 삭제

```python
git branch -d SangKwon93
```
10) 새로운 기능 추가를 위해 동일 과정 반복
```python
git switch -c SangKwon93_1
```

**2> 원격 저장소 소유권이 없는 경우 (Fork & Pull model)**
- 오픈 소스 프로젝트와 같이, 자신의 소유가 아닌 원격 저장소인 경우 사용
- 원본 원격 저장소를 그대로 내 원격 저장소에 `복제`  (이 행위를 `fork`라고 합니다.)
- 기능 완성 후 `Push는 복제한 내 원격 저장소에 진행`
- 이후 `Pull Request`를 통해 원본 원격 저장소에 반영될 수 있도록 요청

1. 소유권이 없는 원격 저장소를 `fork`를 통해 내 원격 저장소로 복제

2. `fork` 후, 복제된 내 원격 저장소를 로컬 저장소에 `clone` 받음
```python
git clone https://github.com/edukyle/kakao_clone.git
```
3. 로컬 저장소와 원본 저장소를 동기화 하기 위해 연결
``` python
# 원본 원격 저장소에 대한 이름은 upstream으로 붙이는 것이 일종의 관례

git remote add upstream https://github.com/AlexKwonPro/kakao_clone.git
```
4. 사용자는 자신이 작업할 기능에 대한 브랜치를 생성하고, 그 안에서 기능을 구현
```python
git switch -c SangKwon93
```
5. 기능 구현이 완료되면, 복제 원격 저장소(orign)에 해당 브랜치를 `push`
```python
git push origin SangKwon93
```
6.복제 원격 저장소(origin)에는 master와 브랜치가 반영

7.Pull Request를 통해 복제 원격 저장소(origin)의 브랜치를 원본 원격 저장소(upstream)의 master에 반영해달라는 요청 
(원본 원격 저장소의 관리자가 코드 리뷰를 진행하여 반영 여부를 결정)

8. 원본 원격 저장소(upstream)의 master에 브랜치가 병합되면 복제 원격 저장소(origin)의 브랜치는 삭제, 사용자는 로컬에서 master 브랜치로 이동
```python
git switch master
```

9. 병합으로 인해 변경된 원본 원격 저장소(upstream)의 master 내용을 로컬에 받아오고 기존 로컬 브랜치 삭제 
```python
 git pull upstream master
 git branch -d SangKwon93
 ```
 10. 새로운 기능 추가를 위해 위 과정을 반복

 ```python
  git switch -c SangKwon93_1
  ```

  **3> Pull Request 자세히 알아보기**

1. 브랜치를 Push 하면 Compare & pull request 라는 알림 버튼이 나타나는데, 이를 누르면 됩니다.
  ![사진1](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8e93888e-c19b-4c07-ac2e-d58e03ee7e1d%2FUntitled.png?table=block&id=7630a86c-b38f-439c-95d3-d4f727bc2909&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

2. 혹은 원격 저장소 상단 바에서 Pull requests → New pull request을 통해서도 가능합니다.
  ![사진2](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcd42e34a-aae5-42ff-95cb-efa5226e2eb9%2FUntitled.png?table=block&id=9b9f7f99-db49-4825-a779-998f47579524&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

3. base는 병합될 대상입니다. master를 base로 두면 됩니다.
compare는 병합할 대상입니다. 우리가 만든 feature/login 브랜치를 compare로 두면 됩니다. 그리고 아래쪽에서 비교 내용을 확인하고 Create pull request를 클릭합니다.
![사진3](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F16d746e2-6f1d-4272-912f-ccfe7f4580f3%2FUntitled.png?table=block&id=10228144-a044-47ba-a5ba-17474b9d98c3&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

4. Pull Request에 대한 제목과 내용, 각종 담당자를 지정하는 페이지가 나옵니다.
모두 작성했다면 Create pull request를 눌러서 PR을 생성합니다.
![사진4](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ffed29aad-7ec5-4f93-8afd-684afc195e65%2FUntitled.png?table=block&id=fdf393b9-c20f-4716-98f7-697418a73f5b&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

5. PR이 생성되면 다음과 같은 화면이 나타납니다. 빨간 표시가 된 세 부분을 살펴보겠습니다.
![사진5](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe2ba1dd2-57ff-40f4-9f58-1053f1c00ccc%2FUntitled.png?table=block&id=49b779ea-e9a2-4afc-9145-7aed60ed6043&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

6. Conversation : 아래 Write 부분에서 comment를 별도로 작성할 수도 있습니다. 그리고 Merge pull request 버튼을 누르면 병합이 시작됩니다. (충돌(conflict) 상황에서는 충돌을 해결하라고 나옵니다.)
![사진6](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0e1a6f87-17b2-4c79-8ab6-879b1891aa8e%2FUntitled.png?table=block&id=7519aa27-d255-4451-8cdc-c3ff5bbb4f5e&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

7. Commits : PR을 통해 반영될 커밋들을 볼 수 있습니다.
![사진7](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3c37c888-187a-47c2-b945-94fb440f6a88%2FUntitled.png?table=block&id=b14f2dc6-6ebf-4db2-bd6d-ea5e209efd83&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

8. Files changed : 파일의 변화 내역들을 볼 수 있습니다.
![사진8](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9ac9ad6e-63e9-431c-8757-a92778b169a2%2FUntitled.png?table=block&id=4e542e36-1d1b-4872-b7ca-2fd5972a74d7&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

9. 코드리뷰를 원하는 라인에서 `+` 를 눌러서 해당 라인에 리뷰를 남길 수 있습니다.  
빨간 사각형으로 표시된 작은 아이콘을 클릭하면, **`suggestion 기능`(코드를 이렇게 바꾸라고 추천하는 기능)**을 넣을 수도 있습니다.
![사진9](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1cd52944-6941-4302-b520-c54eac4f2447%2FUntitled.png?table=block&id=71f4b8b7-7606-448d-beff-68e4014464a8&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

10. 코드 리뷰를 끝내려면 Finish your review 버튼을 누르면 됩니다. 
그리고 옵션을 선택하고 Submit review를 클릭합니다.
![사진10](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc69d4afa-c6df-4b42-8226-cb51c2f45ef0%2FUntitled.png?table=block&id=4f003585-5362-4497-92f9-e1850852b326&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)
- Comment: 추가적인 comment를 작성할 경우 선택
- Approve: merge를 승인하는 경우 선택
- Request change : 수정해야 하는 사항이 있을 경우 선택

11. 다시 conversation으로 가보면 진행했던 리뷰가 이렇게 나타난 것을 확인할 수 있습니다.
![사진11](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fefb77ecb-305a-472d-9414-ece0ec9192b8%2FUntitled.png?table=block&id=f25a8f07-ca99-4129-9e0b-bf87f8d1c3ac&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

12. 병합을 하게 되면 아래와 같이 보라색으로 병합이 완료되었다고 나오면 성공입니다.  `Delete branch` 버튼을 통해 병합된 `feature/login` 브랜치를 지울 수 있습니다. (원격 저장소에서만 지워집니다.)
![사진12](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F311953ae-acc1-4393-9f28-c724efc92aee%2FUntitled.png?table=block&id=4ada51de-20e6-460e-bc68-e7cd6769763d&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

13. master를 확인해보면 feature/login의 내용이 master에 병합된 것을 확인할 수 있습니다.
![사진13](https://hphk.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0c856336-d306-4e59-bc39-6d60d5a390de%2FUntitled.png?table=block&id=d1106ab2-3740-459b-a6bf-efa41d1cdd62&spaceId=daa2d103-3ecd-4519-8c30-4f55e74c7ef4&width=1490&userId=&cache=v2)

14. 이후 로컬 저장소의 master 브랜치에서 git pull을 이용해 로컬과 원격을 동기화 합니다.