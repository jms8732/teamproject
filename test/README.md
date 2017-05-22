# 테스트

테스트는`/ cmake / RunTests.cmake` 파일에 의해 실행됩니다.

## 디렉토리 구조

테스트가 있는 디렉토리 : 벤치 마크의 경우 / test / benchmark, 기능 테스트의 경우 / test / functional, 
단위 테스트의 경우 / test / unit. `/ test / config`는 `configure.file '을 사용하여
`* .lua` 파일로 변환되는`* .in` 파일 (현재 하나의 파일)을 포함합니다. 
CMake 명령 : 이것은 lua 테스트에서 CMake 변수를 처리하기 위한 것입니다. 
`/ test / includes`는 luajit`ffi.cdef`가 사용하는 include 파일을 포함합니다. 
C definitions parser :이 메카니즘을 통해 접근 할 수 없는 매크로를 다른 방법으로 접근 가능하게 만들 수 있습니다.

파일`/ test / * / preload.lua`는 `--helper` 옵션을 통해서 busted에 의해 미리 적재 될 모듈을 포함하고 있습니다.

`/ test / ** / helpers.lua`는 하나의 테스트가 아니라 여러 테스트에 의해 사용되기 위한 여러 개의 "라이브러리" 기능을 포함하고 있습니다.

`/ test / * / ** / * _ spec.lua`는 실제 테스트가 포함 된 파일입니다. 
`_spec.lua`로 끝나지 않는 파일들은 공통 주제를 제외하고`/ test / ** / helpers.lua`와 같은 라이브러리입니다.

`/ test / unit` 및`/ test / functional` 내부의 테스트는 일반적으로 테스트할 의미 구성 요소에 따라 그룹으로 나뉩니다.

## 환경 변수

Test 동작은 환경 변수의 영향을 받습니다.
Currently supported (Functional, Unit, Benchmarks) (when Defined; when set to _1_; when defined, 
treated as Integer; when defined, treated as String; when defined, treated as 
Number; !must be defined to function properly):

`GDB` (F) (D) :`gdbserver`에서 nvim 인스턴스가 실행되도록 합니다. 
`localhost : 7777 : `에서 접근 할 수 있습니다.
`gdb build / bin / nvim`을 사용하고 `target remote : 7777`을 안에 입력하십시오.


`GDBSERVER_PORT` (F) (I) :`GDB`에 사용 된 포트를 기각합니다.
`VALGRIND` (F) (D) :`valgrind`에서 nvim 인스턴스가 실행되도록 합니다.
이 경우 로그 파일 이름은 `valgrind- % p.log` 입니다.
비어 있지 않은 valgrind 로그는 실패한 테스트.
Valgrind 인수는`/ test / functional / helpers.lua`에 있습니다.
`GDB`와 함께 사용할 수 있습니다.

`VALGRIND_LOG` (F) (S) : VALGRIND에 사용되는 valgrind 로그 파일 이름을 덮어 씁니다.

`TEST_SKIP_FRAGILE` (F) (D) : test suite가 깨지기 쉬운 테스트를 건너 뛰도록 합니다.

`NVIM_PROG`,`NVIM_PRG` (F) (S) : Neovim 실행 파일의 경로를 덮어 씁니다 (기본값은`build / bin / nvim`입니다).

CC (U) (S) : 파일을 전처리하는데 사용할 C 컴파일러를 지정합니다. 
현재 gcc 호환 인수를 가진 컴파일러만 지원됩니다.

NVIM_TEST_MAIN_CDEFS` (U) (1) :`ffi.cdef`가 메인 프로세스에서 실행되도록 합니다.
이것은 카운터에도 불구하고 헤더 정의의 충돌로 인한 버그의 가능성을 높이지만 
C 문자열의 구문 분석을 수행하기 위한 `ffi.cdef` 를 요구하지 않음으로써 단위 테스트의 속도를 크게 높입니다.

NVIM_TEST_PRINT_I` (U) (1) :`cimport` 인쇄가 사전 처리되지만 `formatc` 헤더를 통해 아직 필터링되지 않습니다.
`formatc`를 디버그하는데 사용됩니다. 인쇄는 줄 번호로 수행됩니다.

NVIM_TEST_PRINT_CDEF` (U) (1) :`cimport`가`ffi.cdef`에 전달 할 최종 줄을 출력합니다.
`ffi.cdef`에서 가끔씩 발생하는 오류를 디버깅하는데 사용됩니다.

NVIM_TEST_PRINT_SYSCALLS` (U) (1) : syscall 래퍼가 호출 될 때 stderr로 출력하게 합니다. 
단위 테스트를 별도의 프로세스에서 실행하는 코드를 디버깅하는 데 사용됩니다.

NVIM_TEST_RUN_FAILING_TESTS` (U) (1) :`itp`가 실패한 것으로 알려진 테스트를 실행하게합니다.
(세번째 인자를 true로 설정하여 표시).

`LOG_DIR` (FU) (S!) : valgrind와 ASAN 로그 파일을 찾을 곳을 지정합니다.

NVIM_TEST_CORE_ * (FU) (S) : 코어 파일을 검색 할 위치를 지정하는 환경 변수 세트.
한 번에 모든 것을 정의해야합니다.

NVIM_TEST_CORE_GLOB_DIRECTORY (FU) (S) : 코어 파일이 위치한 디렉토리 `.` 일 수도 있습니다. 
이 디렉토리는 코어 파일을 재귀적으로 검색합니다. 
참고 : 이 변수는 다음 중 하나에 영향을 주기 위해 정의 되어야 합니다.

NVIM_TEST_CORE_GLOB_RE (FU) (S) : 코어 파일과 일치해야하는 정규식. 
예 : `/ core [^ /] * $`. 없을수도 있으며, 이 경우 파일이 일치하는 것으로 간주됩니다.

NVIM_TEST_CORE_EXC_RE (FU) (S) : 특정 디렉토리에서 코어 파일을 검색하지 못하도록 하는 정규식.
예 : `^ / %. deps $`를 사용하여 `/ .deps` 내부를 검색하지 마십시오. 없으면 아무것도 제외되지 않습니다.

NVIM_TEST_CORE_DB_CMD (FU) (S) : 디버거에서 백 트레이스를 가져 오는 명령.
예 : `gdb -n -batch -ex "쓰레드는 모두"% _NVIM_TEST_APP "-c"$ _NVIM_TEST_CORE "`를 모두 적용합니다. 
기본값은 example 명령입니다. 이 디버그 명령은 다음을 사용할 수 있습니다.
환경 변수`_NVIM_TEST_APP` (디버깅되고있는 응용 프로그램의 경로 : 일반적으로 nvim 또는 luajit)와
`_NVIM_TEST_CORE` (backtrace를 얻을 코어 파일).

NVIM_TEST_CORE_RANDOM_SKIP` (FU) (D) :`check_cores`가 테스트의 약 90 % 코어를 체크하지 않게 합니다.
어떤 이유로 든 코어를 찾을 수 없을 때 사용해야 합니다. 
일반적으로 (OS X에서 또는`NVIM_TEST_CORE_GLOB_DIRECTORY`가 정의되고 이 변수가 아닌 경우) 각 테스트 후에 코어가 검사됩니다

`NVIM_TEST_RUN_TESTTEST` (U) (1) :`test / unit / testtest_spec.lua`를 실행할 수 있습니다.
테스트 인프라가 어떻게 작동하는지 확인하는 데 사용됩니다.

NVIM_TEST_TRACE_LEVEL` (N) : 유닛 테스트 추적 레벨을 지정합니다 
`0` : 추적을 비활성화 합니다 (테스트가 충돌하고 코어 덤프가 생성되지 않으면 데이터를 얻지 못합니다),
`1` : 비어 있거나 정의되지 않은  C 함수만 트레이스에서 (모든 것을 기록하는 것보다 빠르다) 리턴합니다.
`2` : 모든 함수 호출, 리턴 및 루아 소스 행을 기록합니다.
