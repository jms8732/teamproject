# YouCompleteMe 통합

## 정의

이것은 vim의 YCM 플러그인을 구성하여 Neovim 프로젝트에서 작업하는 개발자에게 
C 의미론적인 지원(완료, 정의 이동)을 제공하는 데 필요한 코드를 제공합니다.

## 설치

### 1단계

  [YouCompleteMe](https://github.com/Valloric/YouCompleteMe)을 설치합니다.

### 2단계

```bash
cp contrib/YouCompleteMe/ycm_extra_conf.py .ycm_extra_conf.py
echo .ycm_extra_conf.py >> .git/info/exclude
make
```

팁 : 소스 코드 탐색을 개선하려면 다음과 같이 nvim 구성에 추가하면 됩니다.

```vim
au FileType c,cpp nnoremap <buffer> <c-]> :YcmCompleter GoTo<CR>
```

그리고 커서가 해당 위치에 있을 때 `ctrl + ]`를 사용하여 빠르게 정의나 선언으로 건너 뛸 수 있습니다.
