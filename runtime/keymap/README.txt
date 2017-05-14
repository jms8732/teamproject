Vim 용 키 맵 파일

'keymap'옵션이 설정되면 파일 중 하나가 로드됩니다.

파일의 이름은 다음 부분으로 구성됩니다.

	{language}[-{layout}][_{encoding}].vim

{language} 언어 이름 (e.g., "hebrew", "greek")

{layout} 선택사항	: keyboard layout의 이름 (e.g., "spanish",
		"russian3").  생략하면 표준 US-english 키보드의 레이아웃이 사용됩니다.

{encoding}	선택사항 : 이 키 맵이 작동하는 문자 인코딩.
		생략되면 언어에 대한 normal 인코딩이 가정됩니다.
		인코딩 옵션의 값을 사용하십시오.  '_'대신 '-'를 사용하십시오.

각 파일은 관리자와 마지막으로 변경된 날짜를 지칭하는 헤더로 시작합니다.
키맵 파일에 문제가있는 경우 최신 버전인지 확인하십시오.
필요한 경우 유지 보수 담당자에게 문제점을 보고하십시오.

"loadkeymap"아래의 키맵 행의 형식은 Vim 도움말 파일에서 설명합니다 
( ": help keymap-file-format"참조).
