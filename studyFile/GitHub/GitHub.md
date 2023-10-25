> [!tip] This Post exists for #GitHub
> 이 글은 깃 허브를 조금 더 잘 활용할 수 있도록 만든 정리 글이며, 어떤 식으로 정보를 클라우드에 저장하며, 나의 코드를 다른 사람과 공유가 가능한지 알아볼 수 있다.

<br/>

# GitHub

- - - 
![[Pasted image 20230920180328.png]]

깃 허브는 정보를 올린 횟수와 업로드 된 정보들을 확인할 수 있으며, 자신이 분류한 레포지토리에 따라 정보를 달리 저장하여 공유 혹은 클라우드 형식의 정보 저장이 가능하다.

## GitHub 사용 방법
- - -
#### 1. Make Repositories 
![[Pasted image 20230920181717.png]]

- Repository의 이름을 설정한다.
( 단, blank space는 불가능 하니, '-'나 '\_'로 대체하면 된다. )
( 추천하는 Repository는 후에 명령어 칠 것을 생각하여, CamelCase 추천 )
- Public은 모두에게 공개가 가능하며, 모두에게 훈수를 가능하도록 하며, Private는 자신이 설정한 것에 따라서 보여주는 부분을 달리 한다.
- ReadME.md 파일은 프로젝트의 설명을 위한 것으로 만약 단일 프로젝트를 만들 예정이라면 반드시 만들어 두자.
- .gitignore 파일은 GitHub에 올리지 않을 파일을 지정하여, GitHub에 올리지 않도록 한다.
- license는 각 해당 라이센스마다 지정한 것이 있는 데 그것은 나중에 정리할 예정임.

#### 2. Make Repository Local File
![[Pasted image 20230920182612.png]]

- Repository를 만들면 매우 설명이 잘 되어있다. 해당 명령어만 잘 따라한다면 문제가 없음.


#### 3. Add Collaborator
![[Pasted image 20230920183027.png]]

- 상단의 Settings를 통해 Collaborators에 접근이 가능함
- Collaborators를 추가하기 위해서는 해당 Collaborators의 이메일이나, 사용자 닉네임을 알고 있으면, 추가가 가능하다.



## Fork & Pull
- - -

#### 1. Fork
 - 다른 계정의 Repository의 나의 Repository로 가져와 동기화 하는 작업
 - 중요한 점은 Fork를 한 계정에서 Code의 변화가 일어나면 그대로 동기화하여 나의 Repository에 적용이 됨.

#### 2. Pull
- 다른 계정의 Repository를 복사하여 가져오는 것임.
- 변화가 일어나도 동기화가 되지 않으며, origin repositor에 권한이 없는 경우 push가 불가능함.


# Fork
- - -
![[Pasted image 20230920183639.png]]

이때 우리가 가장 간편하게 Repository 관리를 할 수 있는 프로그램이 바로 Fork라고 하는 프로그램이다. 해당 프로젝트를 이용한다면, 얼마나 관여를 했는지 혹은, Branch가 어떻게 되었는지 시각적으로 확인이 가능하다.


![[Pasted image 20230920183805.png]]







