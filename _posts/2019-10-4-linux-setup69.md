---
layout: post
title: Linux setups for kernel development
date: 2019-10-4 17:8:00 +0900
categories: [unix, linux]
---

# Linux setups for kernel development

## 서론
최근 나는 리눅스 커뮤니티 등지에서 활동하는 오픈소스 개발자가 되는것을 목표로 운영체제 공부를 시작했다. APUE(Advanced Programming in the UNIX Environment)와 공룡책(Operating System Concepts)책을 읽기 시작한것도 그 때문이다.

최근 너무 이론 공부만 한것같아 코드를 작성하고 싶어서, 개발 환경을 구축하고싶었다.  
일단 나는 macOS를 사용하고 있기 때문에 VMware위에 Ubuntu 18.04.3 LTS를 설치했다. 그러니 배경이 되는 환경은 Ubuntu 18.04.3 LTS 이다.

## 현재 만들어진 환경
0. TMUX + SSH + Disabled GUI
- macOS의 셸에서 네이티브로 개발하는 느낌을 내기 위해서
- GUI 리소스를 줄이기 위해서
1. Nvim + Vundle
- ycm
- auto-pairs
- autocomplpop
- vim-airline
- vim-airline-themes
- vim-easytags
- vim-misc
2. ssh 자동로그인

## Step-by-step
### 일단 프로그램 설치부터!
SSH, TMUX, nvim을 설치하고, 필요없는 패키지들을 삭제하는 명령어이다.
```bash
sudo apt update;sudo apt upgrade;sudo apt install -y clang openssh-server tmux neovim python3-neovim python3-dev;sudo apt remove -y --purge firefox libreoffice*; sudo apt clean -y;sudo apt autoremove -y;
```

### SSH 서버 설정
나는 기본 설정을 그대로 사용할것이라서 그냥 다음의 명령어로 서비스만 켜주었다.
```bash
sudo service ssh start
```

### TMUX 사용법 익히기
https://seulcode.tistory.com/144  
이곳의 설명을 참고하면서 잘 쓰고 있다.

### Nvim 설정
#### 실행시키기 편하게!
일단 .bashrc에
```bash
alias "vi"="nvim"
alias "vim"="nvim"
```
을 적어둠으로써 기존에 vim을 실행시키듯 nvim을 실행시킬 수 있도록 하였다.

#### init.vim 설정
macOS에서 쓰던 init.vim을 그대로 넣어주었다.
```
colorscheme kalisi
set t_Co=256
set number
set hlsearch
set ruler
set ignorecase
set showcmd
set wildmenu
set nocompatible
set autoindent
set cindent
set laststatus=2
set tabstop=4
set showmatch
set fileencodings=utf-8,euc-kr
set shiftwidth=4
set noexpandtab
set backspace=indent,eol,start
set nowrap
set nobackup
set smartindent
set background=dark
set encoding=utf-8
set nocompatible
filetype off
filetype plugin on
set tags+=/usr/include/tags
set rtp+=~/.config/nvim/bundle/Vundle.vim
call vundle#begin('~/.config/nvim/bundle')
 
Plugin 'VundleVim/Vundle.vim'
Plugin 'Valloric/YouCompleteMe'
Plugin 'jiangmiao/auto-pairs'
Plugin 'AutoComplPop'
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
Plugin 'xolox/vim-easytags'
Plugin 'vim-misc'

call vundle#end()

autocmd FileType html :AcpDisable
"ycm
let g:ycm_global_ycm_extra_conf = '/Users/yeongyu/.config/nvim/bundle/YouCompleteMe/.ycm_extra_conf.py'
let g:ycm_confirm_extra_conf = 0
let g:ycm_key_list_select_completion = ['', '']
let g:ycm_key_list_previous_completion = ['', '']
let g:ycm_autoclose_preview_window_after_completion = 1
let g:ycm_warning_symbol = '>*'
let g:ycm_server_python_interpreter = '/usr/local/bin/python3'
"AutoComplPop
function! InsertTabWrapper()
let col = col('.') - 1
if !col || getline('.')[col-1]!~'\k'
return "\<TAB>"
else
if pumvisible()
return "\<C-N>"
else
return "\<C-N>\<C-P>"
end
endif
endfunction

"inoremap <tab> <c-r>=InsertTabWrapper()<cr>

hi Pmenu ctermbg=blue
hi PmenuSel ctermbg=yellow ctermfg=black
hi PmenuSbar ctermbg=blue

set tags=./tags,tags
```
이걸 ~/.config/nvim/init.vim 에 넣어주었다.

#### 플러그인 설치: Vundle부터!
```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.config/nvim/bundle/Vundle.vim
```
이후에, nvim을 실행한뒤  
:PluginInstall  
명령어를 실행하면 플러그인들이 다 설치가 된다. 그러나 아직 하나 문제가있는데, 그것은 바로 ycm(You Complete Me)가 아직 컴파일 되지 않았다는 점.

##### YCM 설정
ycm이 설치된 폴더인 ~/.config/nvim/bundle/YouCompleteMe 에 들어가서 다음의 명령어로 실행을 한다.
```bash
python3 install.py --clang-completer
```
그러면 이제 문제없이 설정이 된 모습을 볼 수 있다.

### GUI Disable
일단 나의 경우에는 '혹시나' GUI가 필요한 환경이 생길 수 있을까봐 (동아리에서 리눅스를 사용해야하는 경우가 있어서) 서버 버전으로 굳이 설치하지 않았는데, 그런 나를 위해서 평소에는 gui를 꺼둘 필요가 있었다. 이 역시 다음의 명령어로 가능하다.
```bash
sudo systemctl set-default multi-user.target
```

만약 필요할 경우에는 다음의 명령어로 gui를 다시 활성화 해주도록 하자.
```bash
sudo systemctl set-default graphical.target
```

# SSH 자동로그인
```bash
scp ~/.ssh/id_rsa.pub <계정명>@<ip>:~/.ssh/authorized_keys
```