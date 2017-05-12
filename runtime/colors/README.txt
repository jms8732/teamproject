colorscheme 파일용 README.txt

해당 파일은 ":colorscheme" 명령에 사용합니다
GUI의 편집/colorscheme에 사용합니다


Hints for writing a color scheme file:

color scheme을 정의하는 두 가지 방법:

1. 새 표준 색상을 정의하고 이에 따라 배경옵션 설정
	set background={light or dark}
	highlight clear
	highlight Normal ...
	...

2. 기본색상을 사용하고 배경값으로 자동 조절
	highlight clear Normal
	set background&
	highlight clear
	if &background == "light"
	  highlight Error ...
	  ...
	else
	  highlight Error ...
	  ...
	endif

":highlight clear"를 사용해 모든 것을 기본값으로 재설정 할 수 있습니다, 또한
원하는 그룹을 변경할 수 있습니다. 이 기능은 Update된 Vim에서도 사용 가능합니다.
":highlight clear" 은 'background'값을 사용합니다
일부 속성은 색상 표에서 제거하려는 기본값으로 설정할 수 있습니다.
attributes를 제거하려면 "gui=NONE" 명령어를 사용하십시오

선택한 colorscheme에 따라 배경을 설정하려는 경우
아래의 자동작성이 유용하게 사용될 수 있습니다:
     autocmd SourcePre */colors/blue_sky.vim set background=dark
Replace "blue_sky" with the name of the colorscheme.

Colorcheme을 로드 한 후 조정하려는 경우 ColorScheme autocmd 이벤트를 확인하십시오.

하이라이트 그룹에 대한 정보는
"highlight-groups" 및 "group-name"에 대한 도움말을 찾으세요

You can use ":highlight"를 사용해 현재 사용하고있는 색상을 찾을 수 있습니다.  
예외 : ctermfg와 ctermbg 값은 숫자이며 현재 터미널에서만 유효합니다. 
Use the color names instead.  See ":help cterm-colors".

기본 색상 설정은 소스 파일 src / syntax.c에서 찾을 수 있습니다.
"highlight_init"를 검색하십시오.

다른 사용자들이 사용할 수있는 색 구성표가 있다고 생각하면,
다음 항목을 확인하십시오.:

- color terminal 뿐만아니라 GUI에서도 작동합니까?
- "g:colors_name"가 의미있는 값으로 설정되어있습니까? 해당 질문이 명확하지 않은 경우
   다음과 같이 할 수 있습니다 let g:colors_name = expand('<sfile>:t:r')
- '배경'이 사용되었거나 적절한 명도가 설정되어 있습니까??
- 'hlsearch'설정을 시도하고 패턴을 검색하면 일치하는 것이 쉽게 발견됩니까?
- ": split"및 ": vsplit"을 사용하여 창을 분할하십시오. 
  상태 표시 줄과 세로 구분 기호가 명확하게 표시됩니까?
- GUI에서 많은 구문 강조가있는 파일에서도 커서를 쉽게 찾을 수 있습니까?
- 하드 코딩 된 escape sequences를 사용하지 마십시오. 다른 터미널에서는 작동하지 않습니다. 
  GUI에는 항상 색상 이름 또는 #RRGGBB를 사용하십시오.
