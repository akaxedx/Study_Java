# nvim配置

## 依赖

node 16.x

npm 8.x

```shell
curl -sL https://deb.nodesource.com/setup_16.x|sudo -E bash -
sudo apt-get install -y nodejs
node -v #查看版本
npm -v #查看版本
```

curl

```shell
sudo apt install curl
```

git

```shell
sudo apt install git
```

clang

```shell
sudo apt-get update
sudo apt-get install clang
clang --version
```

ccls

```shell
sudo apt install ccls
```

nvim

```shell
sudo apt install nvim
```

yarn

```shell
sudo apt install yarn
```

另外需要加速器全局代理

pigcha可用

## 对nvim进行配置

创建文件夹~/.config/nvim/

新建文件init.vim

配置后的操作如下

缩进使用空格，tab会警告

已配置()[]{}’’””的自动补全

按a、i、o键进入插入模式

连续按jk进入普通模式（原版按esc）

在普通模式下按\e进入文件树目录

按^Ww切换操作窗口

普通模式下：被替换为空格

代码补全通过TAB进行向下选择，shift+TAB进行向上补全

nvim基础操作：

普通模式下：

保存：:w

退出：:q

保存并退出：:wq

强制退出：:q!

下载插件：:PlugInstall

进入服务器配置文件：:CocConfig

```shell
imap jk <Esc>
nmap <space> :
inoremap ( ()<ESC>i
inoremap { {}<ESC>i
inoremap [ []<ESC>i
inoremap ' ''<ESC>i
inoremap " ""<ESC>i
set number
set relativenumber
set expandtab
set tabstop=2
set shiftwidth=2
set softtabstop=2
set ignorecase
set smartcase
set notimeout

if empty(glob('~/.config/nvim/autoload/plug.vim'))
  :exe '!curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs
              \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
  au VimEnter * PlugInstall --sync | source $MYVIMRC
endif


" =======================
" ===  plugins  begin ===
" =======================
call plug#begin('~/.config/nvim/plugged')
" file explorer
  Plug 'preservim/nerdtree'
" highlight
  Plug 'cateduo/vsdark.nvim'
  Plug 'jackguo380/vim-lsp-cxx-highlight'
" lsp
  Plug 'neoclide/coc.nvim', {'branch': 'release'}

call plug#end()
" =======================
" ===   plugins  end  ===
" =======================
" ==== preservim/nerdtree ====

nnoremap <LEADER>e :NERDTreeToggle<CR>
" ==== cateduo/vsdark.nvim ====

set termguicolors
let g:vsdark_style = "dark"
colorscheme vsdark


" ==== jackguo380/vim-lsp-cxx-highlight ====

hi default link LspCxxHlSymFunction cxxFunction
hi default link LspCxxHlSymFunctionParameter cxxParameter
hi default link LspCxxHlSymFileVariableStatic cxxFileVariableStatic
hi default link LspCxxHlSymStruct cxxStruct
hi default link LspCxxHlSymStructField cxxStructField
hi default link LspCxxHlSymFileTypeAlias cxxTypeAlias
hi default link LspCxxHlSymClassField cxxStructField
hi default link LspCxxHlSymEnum cxxEnum
hi default link LspCxxHlSymVariableExtern cxxFileVariableStatic
hi default link LspCxxHlSymVariable cxxVariable
hi default link LspCxxHlSymMacro cxxMacro
hi default link LspCxxHlSymEnumMember cxxEnumMember
hi default link LspCxxHlSymParameter cxxParameter
hi default link LspCxxHlSymClass cxxTypeAlias

" ==== neoclide/coc.nvim ====

" coc extensions
let g:coc_global_extensions = [
      \ 'coc-json',
      \ 'coc-tsserver',
      \ 'coc-css',
      \ 'coc-html',
      \ 'coc-vimlsp',
      \ 'coc-cmake',
      \ 'coc-highlight',
      \ 'coc-pyright'
      \ ]

set signcolumn=number
" <TAB> to select candidate forward or
" pump completion candidate
inoremap <silent><expr> <TAB>
      \ pumvisible() ? "\<C-n>" :
      \ <SID>check_back_space() ? "\<TAB>" :
      \ coc#refresh()
" <s-TAB> to select candidate backward
inoremap <expr><s-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"
function! s:check_back_space() abort
  let col = col('.')-1
  return !col || getline('.')[col - 1] =~# '\s'
endfunction

" <CR> to comfirm selected candidate
" only when there's selected complete item
if exists('*complete_info')
  inoremap <silent><expr> <CR> complete_info(['selected'])['selected'] != -1 ? "\<C-y>" : "\<C-g>u\<CR>"
endif

nnoremap <silent> K :call <SID>show_documentation()<CR>
function! s:show_documentation()
  if(index(['vim', 'help'], &filetype) >= 0)
    execute 'h '.expand('<cword>')
  elseif (coc#rpc#ready())
    call CocActionAsync('doHover')
  else
    execute '!' . &keywordprg . " " . expand('<cword>')
  endif
endfunction

" highlight link CocHighlightText Visual
" autocmd CursorHold * silent call CocActionAsync('highlight')   " TODO

nmap <leader>rn <Plug>(coc-rename)
xmap <leader>f <Plug>(coc-format-selected)
command! -nargs=0 Format :call CocAction('format')

augroup mygroup
  autocmd!
  autocmd FileType typescript,json setl formatexpr=CocAction('formatSelected')
  autocmd User CocJumpPlaceholder call CocActionAsync('showSignatureHelp')
augroup end

" diagnostic info
nnoremap <silent><nowait> <LEADER>d :CocList diagnostics<CR>
nmap <silent> <LEADER>- <Plug>(coc-diagnostic-prev)
nmap <silent> <LEADER>= <Plug>(coc-diagnostic-next)
nmap <LEADER>qf <Plug>(coc-fix-current)

" Remap <C-f> and <C-b> for scroll float windows/popups.
if has('nvim-0.4.0') || has('patch-8.2.0750')
  nnoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? coc#float#scroll(1) : "\<C-f>"
  nnoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? coc#float#scroll(0) : "\<C-b>"
  inoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? "\<C-r>=coc#float#scroll(1)\<CR>" : "\<Right>"
  inoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? "\<C-r>=coc#float#scroll(0)\<CR>" : "\<Left>"
  vnoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? coc#float#scroll(1) : "\<C-f>"
  vnoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? coc#float#scroll(0) : "\<C-b>"
endif

" statusline support
" set statusline^=%{coc#status()}%{get(b:,'coc_current_function','')}  "TODO

" GoTo code navigation.
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gD :tab sp<CR><Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

function! s:generate_compile_commands()
  if empty(glob('CMakeLists.txt'))
    echo "Can't find CMakeLists.txt"
    return
  endif
  if empty(glob('.vscode'))
    execute 'silent !mkdir .vscode'
  endif
  execute '!cmake -DCMAKE_BUILD_TYPE=debug
      \ -DCMAKE_EXPORT_COMPILE_COMMANDS=1 -S . -B .vscode'
endfunction
command! -nargs=0 Gcmake :call s:generate_compile_commands()

```

:wq保存后在普通模式下输入:PlugInstall下载插件，此处需要魔法上网

完成后需要配置clang,ccls

再次打开配置文件

普通模式下输入:CocConfig进入配置文件，输入以下代码

## clang那里的路径需要填写自己安装的clang路径

```shell
{
"languageserver": {
    "ccls": {
      "command": "ccls",
      "filetypes": [ "c", "cc", "cpp", "c++", "objc", "objcpp" ],
      "rootPatterns": [ "compile_commands.json", ".git/", ".hg/", ".vscode", ".vim/" ],
      "initializationOptions": {
        "highlight": {"lsRanges": true},
        "cache": {
          "directory": "/tmp/ccls"
        },
        "clang": {
          "resourceDir": "/usr/bin/clang"
        },
        "completion": {
          "detailedLable": true,
          "placeholder": true
        },
        "index": {
          "onChange": false,
          "initialNoLinkage": true,
          "threads": 2
        },
        "compilationDatabaseDirectory": ".vscode/"
      }
    }
  }
}
```

wq保存，nvim配置完毕

如果在创建cpp等文件出现rootURL的报错将文件中的rootPatterns删除，这个模块是用来管理一些cpp大项目的文件的，学习阶段可以删除，本文档并没有对后续操作进行配置



















