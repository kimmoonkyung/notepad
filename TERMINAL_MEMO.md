### 디렉토리 생성
    mkdir '폴더명'

### 폴더 이동
    mv 폴더(파일) 이동경로

### 현재 경로
    pwd

### 현재 경로 폴더 열기
    open .

### 새 탭 열기
    cmd + T

### 파일 복사
    cp orginal_file copied_file

### 파일, 디렉토리 삭제
    rm text.txt
    text.txt 파일 지우기.

### rm -f text.txt
    text.txt 파일을 묻지 않고 지우기.

### $rm *
    현재 작업중이 directory의 모든 파일 지우기.

### $rm -f *
    묻지도 따지지도 않고 다 지우기.

### rm -i *
    파일 하나하나 물어보고 지우기.

### rm -I *
    전체 파일 한번만 물어보고 다 지우기.

### rm -r directory1
    directory1 폴더 및 안의 파일 다 지우기.

### rm -rf directory1
    묻지도 따지지도 않고 다 지우기. (-f 옵션 + -r 옵션)



### 커서 이동:
    Ctrl + a: 라인의 처음
    Ctrl + e: 라인의 끝
    Alt + b: 커서의 왼쪽 단어 (Option+Right-Arrow)
    Alt + f: 커서의 오른쪽 단어 (Option+Left-Arrow)
    Ctrl + f: 다음 캐릭터 (Right arrow)
    Ctrl + b: 이전 캐릭터 (Left arrow)
    Ctrl + xx: 라인의 처음과 현재 커서 위치를 토글

### 편집:
    삭제
    Alt + backspace: 커서의 왼쪽 단어를 삭제
    Alt + d: 커서의 오른쪽 단어를 삭제
    Ctrl + d: 커서가 위치한 곳의 캐릭터를 삭제
    Ctrl + h: 커서의 왼쪽에 있는 캐릭터를 삭제 (backspace)

### 잘라내기/붙여넣기
    Ctrl + w: 커서의 왼쪽에 있는 단어를 잘라내기
    Ctrl + k: 커서의 오른쪽을 모두 잘라내기
    Ctrl + u: 커서의 왼쪽을 모두 잘라내기
    Ctrl + y: 마지막으로 잘라냈던 걸 붙여넣기 (yank)

### 수정
    Ctrl + t: 커서아래의 캐릭터와 커서 바로 왼쪽의 캐릭터의 위치를 바꾸기
    Alt + t: 커서아래의 단어와 바로 이전 단어의 위치를 바꾸기
    Esc + t: 커서 왼쪽의 두 단어의 위치를 바꾸기
    Alt + u: 현재 커서위치에서 현재 단어의 끝까지의 캐릭터를 대문자로 바꾸기
    Alt + l: 현재 커서위치에서 현재 단어의 끝까지의 캐릭터를 소문자로 바꾸기
    Alt + c: 현재 커서위치의 캐릭터를 대문자로, 나머지 캐릭터는 소문자로 바꾸고 단어의 끝으로 커서를 이동

### 그 외
    Alt + r: (다음/이전 커맨드 사용중) 편집을 취소하고 히스토리의 초기 상태로 돌린다
    Ctrl + _: Undo (편집 한 것을 하나씩 취소)
    Ctrl + l: 화면을 클리어 (clear와 비슷함)
    TAB 파일/디렉터리 이름 자동완성

### 히스토리:
    Ctrl + p: 이전 커맨드 (Up arrow)
    Ctrl + n: 다음 커맨드 (Down arrow)
    Alt + .: 바로 이전 커맨드에서 마지막 단어를 가져오기
    Ctrl + r: 이전 커맨드 히스토리에서 커맨드 검색하기
    Ctrl + g: 검색모드에서 나오기
    Ctrl + o: 커맨드 실행하기
    초기 설정에서는 사용할 수 없다. ~/.bash_profile에 stty discard undef를 추가한 후 터미널 재시동이 필요하다
    return/enter 대신 사용할 수 있다

### 프로세스 컨트롤:
    Ctrl + c: 현재 화면에서 실행중인 프로세스를 Kill/Interrupt (SIGINT)
    Ctrl + d: (옵션에서 비활성화 되어있지 않다면) EOF 시그널을 보낸다. 현재 쉘이 닫힐 것이다 (EXIT)
    Ctrl + z: SIGTSTP 시그널로 현재 화면에서 실행중인 프로세스를 suspend 시킨다
    fg ‘프로세스 이름’ 으로 suspend 된 프로세스를 가져올 수 있다

### Emacs 모드 vs Vi 모드
    기본적으로 Bash에서 Emacs의 단축키를 지원하지만 Vi로 바꿀 수 있는 방법이 있다.

    - Vi 모드 변경
    $ set -o vi

    - Emacs 모드 변경
    $ set -o emacs

### 현재 실행중인 작업 확인
    jobs
    ps -ef | grep [pid or name]

### nohup
    sudo nohup java -jar backend.jar &
    --nohup 실행한것 죽이기
    sudo kill -9 [pid]

### jar 실행
    sudo java -jar aaa.jar


### zsh 설치
    brew install zsh
  
    - zsh 설치 경로 확인
      which zsh
    - 기본 쉘 변경
      chsh -s $(which zsh)
    - zsh 테마 변경
      cd .oh-my-zsh
      sudo code .zshrc

    - New Line 적용하기(옵션)
      vi ~/.oh-my-zsh/themes/agnoster.zsh-theme
    or
      open -a TextEdit ~/.oh-my-zsh/themes/agnoster.zsh-theme
    build_prompt() {
      RETVAL=$?
      prompt_status
      prompt_virtualenv
      prompt_context
      prompt_dir
      prompt_git
      prompt_bzr
      prompt_hg
      prompt_newline //이부분을 추가 꼭 순서 지켜서
      prompt_end
    }
    prompt_newline() {
      if [[ -n $CURRENT_BG ]]; then
        echo -n "%{%k%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR
    %{%k%F{blue}%}$SEGMENT_SEPARATOR"
      else
        echo -n "%{%k%}"
      fi
      echo -n "%{%f%}"
      CURRENT_BG=''
    }

### Syntax Hightlight 적용하기 (옵션)
    brew를 통해 설치해줍니다.
      brew install zsh-syntax-highlighting
    -->플러그인을 적용합니다.
      source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

    --플러그인 디렉토리로 이동
    cd /Users/kimmoonkyung/.oh-my-zsh/custom/plugins
    --zsh-syntax-highlighting 설치
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
    --zsh-autosuggestions 설치
    git clone https://github.com/zsh-users/zsh-autosuggestions

    vi ~/.zshrc
        > plugins=(git) 해당 부분 수정
            > plugins=(git zhs-syntax-highlighting zsh-autosuggestions)


  ### cat명령어에 코드 하이라이팅 + more 기능이 추가된 버전입니다.
    brew install bat
    ~/.zshrc에 cat 대신 사용하도록 설정할 수 있습니다.
    alias cat="bat"

  ### nivm 설치
    ~/.zshrc에
    alias vim="nvim"
    alias vi="nvim"
    alias vimdiff="nvim -d"
    export EDITOR=/usr/local/bin/nvim


  ### mysql 실행 및 중지
    mysqld
        kill -9 pid
    mysql.server start
    mysql.server stop