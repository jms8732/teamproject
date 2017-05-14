[![Neovim](https://raw.githubusercontent.com/neovim/neovim.github.io/master/logos/neovim-logo-600x173.png)](https://neovim.io)

[Wiki](https://github.com/jms8732/teamproject/wiki) |
[Documentation](https://neovim.io/doc) |
[Twitter](https://twitter.com/Neovim) |
[Community](https://neovim.io/community/) |
[Gitter **Chat**](https://gitter.im/neovim/neovim)

[![Travis Build Status](https://travis-ci.org/neovim/neovim.svg?branch=master)](https://travis-ci.org/neovim/neovim)
[![AppVeyor Build status](https://ci.appveyor.com/api/projects/status/urdqjrik5u521fac/branch/master?svg=true)](https://ci.appveyor.com/project/neovim/neovim/branch/master)
[![Pull requests waiting for review](https://badge.waffle.io/neovim/neovim.svg?label=RFC&title=RFCs)](https://waffle.io/neovim/neovim)
[![Coverage Status](https://img.shields.io/coveralls/neovim/neovim.svg)](https://coveralls.io/r/neovim/neovim)
[![Coverity Scan Build](https://scan.coverity.com/projects/2227/badge.svg)](https://scan.coverity.com/projects/2227)
[![Clang Scan Build](https://neovim.io/doc/reports/clang/badge.svg)](https://neovim.io/doc/reports/clang)
<a href="https://buildd.debian.org/neovim"><img src="https://www.debian.org/logos/openlogo-nd-25.png" width="13" height="15">Debian</a>

Neovim은 Vim을 적극적으로 Refactoring하여 다음과 같은 효과를 얻습니다:

- 유지보수를 단순화하며 사용자들의 기여를 장려합니다 [contributions](CONTRIBUTING.md)
- 여러 개발자간의 분할개발을 지원합니다
- core를 수정하지 않고 고급UI 사용을 지원합니다 [advanced UIs] 
- 확장성을 극대화합니다 [extensibility](https://github.com/neovim/neovim/wiki/Plugin-UI-architecture)

[위키(Wiki)](https://github.com/jms8732/teamproject/wiki/소개) 와 [로드맵]
을 사용하시면 더 많은 정보를 얻을 수 있습니다.

[![Throughput Graph](https://graphs.waffle.io/neovim/neovim/throughput.svg)](https://waffle.io/neovim/neovim/metrics)

설치 소스
-------------------

    make CMAKE_BUILD_TYPE=RelWithDebInfo
    sudo make install

 자세한 내용은 [위키(Wiki)](https:/github.com/neovim/neovim/wiki/Building-Neovim)를 참조하세요
 
설치 패키지
--------------------

패키지는 [Homebrew], [Debian], [Ubuntu], [Fedora], [Arch Linux], 및
[more](https://github.com/neovim/neovim/wiki/Installing-Neovim)를 참조하세요

설치 방법
--------------------
[1.알집으로 설치하는 방법](https://github.com/jms8732/teamproject/wiki/%EC%95%8C%EC%A7%91%EC%9C%BC%EB%A1%9C-%EC%84%A4%EC%B9%98%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)

[2.Git으로 설치하는 방법 ](http://github.com/jms8732/teamproject/wiki/설치방법-2)

[3.Git을 사용하지 않고 설치하는 방법]()

프로젝트 레이아웃
--------------

- `ci/`: 서버 스크립트 작성
- `cmake/`: 스크립트 작성
- `runtime/`: 응용 프로그램 파일
- [`src/`](src/nvim/README.md): 응용 프로그램 소스코드
- `third-party/`: 제3자의 종속성 Build를 위한 Cmake 하위 프로젝트 (만약
  `USE_BUNDLED_DEPS` 플래그가 정의되지 않았거나 `USE_BUNDLED` CMake 옵션이 false).
- [`test/`](test/README.md): 테스트 파일

지금까지 무슨일이 있었는지
-----------------------

- [MessagePack](https://msgpack.org)을 기반으로한 RPC API
- 임베디드 [terminal emulator](https://neovim.io/doc/user/nvim_terminal_emulator.html)
- 비동기 [job control](https://github.com/neovim/neovim/pull/2247)
- 여러 편집기 instance간의 [공유 데이터(shada)](https://github.com/neovim/neovim/pull/2506)
- [XDG 기본 디렉토리](https://github.com/neovim/neovim/pull/3470) 지원
- [libuv](https://github.com/libuv/libuv/)-기반 플랫폼/OS 계층
- [Pushdown automaton](https://github.com/neovim/neovim/pull/3413) 입력 모델
- 1000여 개의 새로운 테스트
- Legacy tests를 Lua tests로 변경

포괄적인 리스트를 보려면 [`:help nvim-features`][nvim-features]를 참조하세요

License
-------

Neovim은 Apache 2.0 라이센스의 조건에 따라 라이센스가 부여됩니다(Vim 라이선스에 따라 공헌 된 부분 제외)

- [b17d96][license-commit] 이전에 커밋 된 기여물은 Vim 라이센스에 남아 있습니다

- [b17d96][license-commit] 이후 커밋 된 기여물은 Vim에서 복사 된 것이 아니라면 아파치 2.0 하에서 라이선스가 허가됩니다 (`vim-patch` 토큰에 의해 커밋 로그에서 확인가능)

 자세한 내용은 `라이센스`를 참조하세요

   Vim은 Charityware(프리웨어)입니다. 원하는만큼 Vim을 사용하고 복사 할 수 있지만, 
   우간다의 가난한 어린이들을 위한 기부를 권장합니다. 
   vim 문서의 kcc 섹션을 보거나 다음 URL에있는 ICCF 웹 사이트를 방문하십시오.

            http://iccf-holland.org/
            http://www.vim.org/iccf/
            http://www.iccf.nl/

    당신은 Vim의 개발을 후원할 수도 있으며, Vim 후원자는 기능 투표 또한 가능합니다. 
    
    후원금은 모두 우간다에 기부됩니다.

[license-commit]: https://github.com/neovim/neovim/commit/b17d9691a24099c9210289f16afb1a498a89d803
[nvim-features]: https://neovim.io/doc/user/vim_diff.html#nvim-features
[로드맵]: https://neovim.io/roadmap/
[advanced UIs]: https://github.com/neovim/neovim/wiki/Related-projects#gui-projects
[Homebrew]: https://github.com/neovim/homebrew-neovim#installation
[Debian]: https://packages.debian.org/testing/neovim
[Ubuntu]: http://packages.ubuntu.com/search?keywords=neovim
[Fedora]: https://admin.fedoraproject.org/pkgdb/package/rpms/neovim
[Arch Linux]: https://www.archlinux.org/packages/?q=neovim

<!-- vim: set tw=80: -->
