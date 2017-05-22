이 디렉토리에는 구문 강조를위한 Vim 스크립트가 들어 있습니다.

이 스크립트는 언어가 아니지만 Vim 자체에서 사용됩니다.

syntax.vim ": syntax on"명령에 사용됩니다. synload.vim을 사용합니다.

manual.vim ": syntax manual"명령에 사용됩니다. synload.vim 사용합니다.

synload.vim : 특정 파일 이름 (확장자)이 사용될 때 언어 파일을 자동 로드합니다.
GUI의 구문 메뉴를 설정합니다.

nosyntax.vim ": syntax off"명령에 사용됩니다. synload.vim의로드를 취소합니다.


몇 가지 특수 파일:

2html.vim 	강조 표시된 파일을 HTML로 변환합니다 (GUI 전용).
colortest.vim	 화면의 색상 이름과 실제 색상을 확인합니다
hitest.vim 	현재 강조 표시 설정을 봅니다.
whitespace.vim   탭 및 공백보기.


구문 파일을 작성하려면 ": help usr_44.txt"에있는 문서를 읽으십시오.

다른 사용자가 유용하게 사용할 수있는 새로운 구문 파일을 만들면 Bram@vim.org로 보내주십시오.
이 언어의 파일 형식을 파일 이름 확장명으로 검색하거나
파일의 몇 줄을 검사하여 지침을 포함하십시오.
파일을 이식성있는 방법으로 작성하십시오 ( ": help 44.12"참조).

기존 파일에 대한 의견이 있으면 해당 파일의 관리자에게 보내십시오.
응답이 없을 때만 Bram@vim.org로 메시지를 보내십시오.

구문 파일을 관리하고 개선 작업을 수행하는 경우 해당 새 버전을 Bram@vim.org로 보내주십시오.

더 자세한 정보는 Vim의 "help syntax"를 참조하세요.
