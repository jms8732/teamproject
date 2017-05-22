# Neovim 기여

Neovim 시작하기
---------------


처음 시작하는 사용자는 위험성이 적은 아래 작업부터 진행해보십시오

- Help us [review pull requests](#reviewing)!
- [Vim patch]병합.
- [complexity:low] 이슈 시도.
- Fix [clang-scan] 또는 [coverity](#coverity)경고 수정.

문제 보고
------------------

- [**FAQ**][wiki-faq] 체크.
- [existing issues][github-issues] 참조
- Neovim을 최신 버전으로 업데이트하여 문제가 지속되는지 확인하십시오.
- 플러그인 관리자를 사용하는 경우 플러그인을 주석으로 처리 한 다음 
  하나씩 다시 추가하여 문제의 원인을 찾습니다.
- stacktrace를 포함한 문제보고는 neovim을 발전시킵니다.
- [Bisecting][git-bisect] 원인을 이원화하면 즉각적인 수정이 이루어집니다.

Pull requests ("PRs")
---------------------

- 중복 작업을 피하기 위해 다른 사람들이 현재 작업하고있는 것을 알 수 있도록`[WIP]`pull 요청을 만들 수 있습니다.
- 동일한 커밋 내 관련없는 파일에 대한 변경을 피하십시오.
- master 브랜치 대신 [feature branch] [git-feature-branch]를 사용하십시오.
- [Rebase your feature branch][git-rebasing] PR을 열기 전에 기능 브랜치를 마스터에 rebase 하십시오.
- 검토 주석을 처리 한 후에는 force-push 하십시오.
- [history][git-history-rewriting] 관련 commit을 대화형 리베이스, 개별 monolithic commit으로 결합하십시오.

### 단계: WIP, RFC, RDY

Pull requests는 세가지 단계를 가집니다: `[WIP]` (Work In Progress), `[RFC]` (Request
For Comment) and `[RDY]` (Ready).

- Untagged PR은`[RFC]`로 간주됩니다.
- 진행중인 작업이 피드백을 요구하지 않고 유동적이라면`[WIP]`을 PR 제목 앞에 추가하십시오.
- PR을 마치고 병합을 기다리는 중일 때 PR 제목 앞에`[RDY]`를 앞에 붙이십시오.

예를들어, 일반적인 작업의 흐름은 다음과 같습니다:

1. 피드백 준비가되지 않은 `[WIP]`PR 문은 다른 사람들에게 자신이하는 일을 알리는 결과만 도출합니다.
2. PR이 검토 될 준비가되면 제목의`[WIP]`를`[RFC]`로 대체하십시오. 
   검토 중 발생하는 문제를 해결하기 위해 커밋을 수정할 수 있습니다
3. PR이 병합 될 준비가되면, 작업을 적절하게 rebase / squash 한 다음 제목에있는 [[RFC]`를`[RDY]`로 대체하십시오.

### 메세지 Commit

[commit message hygiene][hygiene]을 따라 리뷰를 더 쉽게 만들고 * VCS / git 로그를 더 가치있게 만드십시오.

- 첫 줄을 72 문자 이하로 유지하십시오.
- ** 커밋 주제 앞에 _scope _ : **`doc :`,`test :`,`foo.c :`,`runtime :`, ...을 붙입니다.
    - 스타일 / lint 변경을 포함하는 커밋의 경우 style 또는 lint가 사용됩니다.
- 빈 줄은 제목과 설명을 구분해야합니다.
- "Fixed bug"나 "Fixes bug" 대신 "Fix bug"를 사용하세요

### 자동 빌드 (CI)

각각의 pull request는 자동 빌드 ([travis CI] 및 [quickbuild])를 통과해야합니다.

- CI 빌드는 [`-Werror`] [gcc-warnings]로 컴파일되므로 PR이 컴파일러 경고를 발생 시키면 빌드가 실패합니다.
- 테스트가 실패하면 빌드도 실패합니다.
  테스트를 로컬에서 실행하려면 [Building Neovim#running-tests][wiki-run-tests]를 참조하십시오.
  테스트 된 다른 컴파일러와 플랫폼 때문에 로컬전달이 CI의 빌드를 보장하지 않습니다
- CI는 [ASan] 및 기타 분석기를 실행합니다. valgrind를 로컬에서 실행하려면 : 'VALGRIND = 1 make test`
- `lint` 빌드 ([# 3174] [3174])는 수정 된 행과 그 인접한 인접 행렬을 검사합니다.
  이는 legacy style을 점진적으로 업데이트하여 스타일 가이드 라인을 충족시킵니다.
    - 단일 단어 (`lint` 또는 `style`)가 스타일 변경만 포함하는 경우 커밋의 제목에 명시하면 됩니다.
- [QuickBuild 실패를 조사하는 방법](https://github.com/neovim/neovim/pull/4718#issuecomment-217631350)

QuickBuild는 해당 호출을 사용합니다.:

    mkdir -p build/${params.get("buildType")} \
    && cd build/${params.get("buildType")} \
    && cmake -G "Unix Makefiles" -DBUSTED_OUTPUT_TYPE=TAP -DCMAKE_BUILD_TYPE=${params.get("buildType")}
    -DTRAVIS_CI_BUILD=ON ../.. && ${node.getAttribute("make", "make")}
    VERBOSE=1 nvim unittest-prereqs functionaltest-prereqs


### Coverity

[Coverity](https://scan.coverity.com/projects/neovim-neovim)는 마스터 빌드에 대해 실행됩니다.
 defect를 참조하고 싶으면 Contributor 레벨에서 액세스 권한을 요청하십시오.
 관리자가 권한을 부여합니다.

coverity 수정을 위해 해당 commit-message format을 사용하십시오:

    coverity/<id>: <description of what fixed the defect>

where `<id>` is the Coverity ID (CID). 예를들어 [#804](https://github.com/neovim/neovim/pull/804)를 참조하십시오.

검토
---------

pull request를 검토하려면 [review-checklist]로 시작하십시오.

검토는 GitHub에서 수행 할 수 있지만 로컬에서 수행하는 것이 더 쉽습니다.

[hub]을 사용하여 pullrequest의 내용으로 새로운 브랜치를 생성 할 수 있습니다. [# 1820] [1820] 

    hub checkout https://github.com/neovim/neovim/pull/1820

[`git log -p master..FETCH_HEAD`] [git-history-filtering]를 사용하여 
`master` 브랜치에 없는 커밋을 모두 나열하십시오; 
`-p`는 각 커밋의 차이점을 보여줍니다.
변경의 모든 주변 기능을 컨텍스트로 표시하려면`-W` 명령어를 사용하십시오.

[gcc-warnings]: https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html
[git-bisect]: http://git-scm.com/book/tr/v2/Git-Tools-Debugging-with-Git
[git-feature-branch]: https://www.atlassian.com/git/tutorials/comparing-workflows
[git-history-filtering]: https://www.atlassian.com/git/tutorials/git-log/filtering-the-commit-history
[git-history-rewriting]: http://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
[git-rebasing]: http://git-scm.com/book/en/v2/Git-Branching-Rebasing
[github-issues]: https://github.com/neovim/neovim/issues
[1820]: https://github.com/neovim/neovim/pull/1820
[hub]: https://hub.github.com/
[hygiene]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[style-guide]: http://neovim.io/develop/style-guide.xml
[ASan]: http://clang.llvm.org/docs/AddressSanitizer.html
[wiki-run-tests]: https://github.com/neovim/neovim/wiki/Building-Neovim#running-tests
[wiki-faq]: https://github.com/neovim/neovim/wiki/FAQ
[review-checklist]: https://github.com/neovim/neovim/wiki/Code-review-checklist
[3174]: https://github.com/neovim/neovim/issues/3174
[travis CI]: https://travis-ci.org/neovim/neovim
[quickbuild]: http://neovim-qb.szakmeister.net/dashboard
[Vim patch]: https://github.com/neovim/neovim/wiki/Merging-patches-from-upstream-Vim
[clang-scan]: https://neovim.io/doc/reports/clang/
[complexity:low]: https://github.com/neovim/neovim/issues?q=is%3Aopen+is%3Aissue+label%3Acomplexity%3Alow
