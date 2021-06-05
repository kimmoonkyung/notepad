### 설정
    cmd + ,

### 자동완성
    기본 cmd + i
        code > 기본설정 > 바로가기키 > 제안항목 트리거 수정
            (바로가기 키 단축키 cmd+K 후 cmd+s)

### 주석
    cmd + /

### 같은 단어 선택 (반복되는 코드 한번에 수정)
    cmd + d (연타)

### 여러 곳에 커서 두고 수정
    opt + 마우스 클릭
### 다중 커서 선택 수정
    cmd + opt + 위 아래 방향키

### 코드 맨 위 이동 및 맨 아래 이동
    cmd + 방향키 (윈도우에서는 Home, End 키 등으로 이동 됐었는데 MacOS는 그게 안 되어서 따로 메모함)

### 터미널에서 열기
    cd '폴더' -> code .

### 파일 삭제
    cmd + backspace

### 라인 삭제
    shift + cmd + k

## 깃 커밋
    1. git add .
    2. git commit -m "메시지"
    3. git push romote_name branch_name 
       : add하고 commit한 코드 git server에 보내기 
       (git push origin master >> 탭 눌러서 확인해보기 >>>> 현재 디렉토리 기준 git push notepad HEAD >>> 하니깐 올라감.)
       vs code 
        > 상단 ... 클릭 > Pull, Push > Push to 클릭

### react 미사용 import 제거
    cmd + .

## Prettier
    .prettierrc 파일 생성
    {
        trailingComma : "all",
        tabWidth : 4,
        semi : true,
        singleQuote : true
    }
        trailingComma
            > 객체 만들 때 컴마 자동
        tabWidth
            > 들여쓰기
        semi
            > ; 세미콜론 자동
        singleQuote
            > 자동 '' 

        > 포맷 단축키
            opt + shift + f
        > 저장시 포맷
            설정 -> format on save 검색 -> ON

### ESLint 자바스크립트 문법 검사 도구
    코딩 스타일을 통일시켜주는 도구랄까.

### Snippet 코드조각 ?
    https://snippet-generator.app/
        Description 설명
        Tab trigger 단축키(핫키)
        Your snippet 작성 코드
            import React from 'react';
            function ${TM_FILENAME_BASE}() {
                return ()
            }
            export default ${TM_FILENAME_BASE};
    
    맥 상단 -> Code -> 기본설정 -> 사용자 코드 조각 -> javascriptreact.json -> 붙여넣기
        > 참고) 하단에 Java Script 를 JavaScript React 로 바꿔야 함.

### md 작성시 이미지 복사 단축키
    cmd + opt + V

### md 작성시 분할 창 미리보기
    cmd + K, V