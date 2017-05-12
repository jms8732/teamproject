해당 디렉토리는 파일 유형에 대해 들여 쓰기를 자동으로 실행하는 파일을 포함합니다.

개인용으로 들여 쓰기 파일을 추가하려면 ":help indent-expression"에서 문서를 참조하십시오.
Looking at the existing files should give you inspiration.

다른 사람들에게 유용하게 사용할 수 있는 들여 쓰기 파일을 제작했다면 
Bram@vim.org로 보내주십시오. 이 언어의 파일 형식을 검색하기위해 지침을 포함시키고,
파일 이름 확장명을 확인하거나 파일의 몇 줄을 확인하십시오.
그리고 아래 규칙을 준수하십시오.

기존 파일에 대한 의견이 있으면 해당 파일의 관리자에게 보내십시오. 
응답이 없을 때만 Bram@vim.org로 메시지를 보내십시오.

들여 쓰기 파일을 관리하고 개선 작업을 수행하는 경우 
새 버전을 Bram@vim.org에 전자 메일로 보내십시오.

들여 쓰기 파일 작성 규칙:

You should use this check for "b:did_indent":

	" 다른 파일이 아직 로드되지 않은 경우에만 해당 들여 쓰기 파일을 로드하십시오.
	if exists("b:did_indent")
	  finish
	endif
	let b:did_indent = 1

항상 ": setlocal"을 사용하여 'indentexpr'을 설정하십시오. 
이렇게하면 다른 버퍼로 이월되지 않습니다.

"endif"와 같은 단어를 입력 한 다음 들여 쓰기를 실행하려면 
"cinkeys"옵션에 "+ ="와 함께 단어를 추가하십시오.

'indentexpr'을 설정하여 함수를 평가 한 다음 해당 함수를 정의합니다.
이 함수는 Vim이 실행되는 동안 한 번만 정의하면됩니다.
함수가 존재하는지 테스트하고 사용하십시오. ":finish", like this:
	if exists("*GetMyIndent")
	  finish
	endif

사용자가 몇 가지 옵션을 설정할 수 있습니다. 
옵션 설정과 함께 파일을 작성하십시오. 
