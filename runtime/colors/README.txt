color scheme 파일 용 README.txt

이 파일들은 ": color scheme" 명령에 사용됩니다.  GUI의 Edit / Color Scheme 메뉴에 나타납니다.

color scheme 파일 작성에 대한 힌트 :

color scheme 를 정의하는 두 가지 기본 방법이 있습니다 :
1. 새 표준 색상을 정의하고 이에 따라 '배경' 옵션을 설정하십시오.
	배경 설정 = {밝은 또는 어두운}
	highlight clear
	highlight Normal ...
	...

2. 기본 색상을 사용하고 자동으로 '배경' 값으로 조정합니다.
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

": highlight clear" 를 사용하여 모든 것을 기본값으로 재설정 한 다음
다르게 하길 원하는 그룹을 변경하십시오. 이것은 또한 Vim의 이후 버전에 추가 된 그룹들에 대해서도 작동합니다.
": highlight clear"는 'background' 값을 사용하므로 이 명령 앞에 설정하십시오.
일부 속성 (예 : 굵게 표시)은 색상 표에서 제거하려는 기본값으로 설정할 수 있습니다. 
특성을 제거하려면 "gui = NONE" 을 사용하십시오.

선택한 color scheme에 따라 'background'를 설정하려는 경우에 다음의 autocmd를 사용할 수 있습니다.
autocmd SourcePre */colors/blue_sky.vim set background=dark
"blue_sky"를 colorscheme의 이름으로 바꾸십시오.
Colorcheme을 로드 한 후 조정하려는 경우 ColorScheme autocmd 이벤트를 확인하십시오.

어딘가에 사용되는 highlight 그룹을 보려면 "highlight 그룹" 및 "그룹 이름"에 대한 도움말을 찾으십시오.

": highlight" 를 사용하여 현재 색상을 찾을 수 있습니다.  
예외 : ctermfg 및 ctermbg 값은 숫자이며 현재 터미널에서만 유효합니다.  
대신 색상 이름을 사용하십시오. ": help cterm-colors"를 참조하십시오.

기본 색상 설정은 소스 파일 src / syntax.c에서 찾을 수 있습니다.
"highlight_init"를 검색하십시오.

다른 사람들이 사용할 수있는 color scheme가 있다고 생각되면 다음 항목을 확인하십시오 :
- GUI뿐 아니라 컬러 터미널에서도 작동합니까?
- "g : colors_name"이 의미있는 값으로 설정 되었습니까?  다음의 명령어로 확인할 수 있습니다. :
  let g:colors_name = expand('<sfile>:t:r')
- '배경'이 사용되었거나 적절하게 '밝게'또는 '어둡게' 설정되어 있습니까?
- 'hlsearch'설정을 시도하고 패턴을 검색하면 일치하는 것이 쉽게 발견됩니까?
- ": split"및 ": vsplit"을 사용하여 창을 분할하십시오. 
   상태 표시 줄과 세로 구분 기호가 명확하게 표시됩니까?
- GUI에서 구문 강조가 많이 있는 파일에서도 커서를 쉽게 찾을 수 있습니까?
- 어렵게 코딩된 escape sequences를 사용하지 마십시오. 다른 터미널에서는 작동하지 않습니다. 
  GUI에는 항상 색상 이름 또는 #RRGGBB를 사용하십시오.
