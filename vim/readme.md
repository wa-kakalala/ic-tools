# vim configuration file

## reference

@reference: https://github.com/RongyeL/ryGvim

@note: https://rongyel.top/posts/f60848c2.html

感谢原作者**Rongye**👍

## how to use 

Extract the files in the current directory to the root directory for use (Linux).
Some plug-in functions need to be supplemented by the installation of iverilog and ctags.

```shell
sudo apt install iverilog
sudo apt install ctags
```

**plugs info**

| 名称               | 功能                 | git clone链接                                                |
| :----------------- | :------------------- | :----------------------------------------------------------- |
| nerdtree           | 文件目录树           | https://github.com/preservim/nerdtree.git                    |
| nerdcommenter      | 快速注释             | https://github.com/preservim/nerdcommenter.git               |
| vim-airline        | 状态栏美化           | https://github.com/vim-airline/vim-airline.git               |
| vim-snippets       | 代码片段库           | https://github.com/honza/vim-snippets.git                    |
| vim-snipmate       | 代码片段展开         | https://github.com/garbas/vim-snipmate.git                   |
| vim-addon-mw-utils | vim-snipmate依赖插件 | https://github.com/MarcWeber/vim-addon-mw-utils.git          |
| tlib_vim           | vim-snipmate依赖插件 | https://github.com/tomtom/tlib_vim.git                       |
| vim-easy-align     | 代码对齐             | https://github.com/junegunn/vim-easy-align.git               |
| neocomplcache      | 代码补全             | https://github.com/Shougo/neocomplcache.vim.git              |
| auto-pairs         | 自动配对括号         | https://github.com/jiangmiao/auto-pairs.git                  |
| ale                | 语法检查             | https://github.com/dense-analysis/ale.git                    |
| gruvbox            | 色彩空间             | https://github.com/morhetz/gruvbox.git                       |
| indentLine         | 缩进标识             | https://github.com/Yggdroot/indentLine.git                   |
| vlog_inst_gen      | Verilog自动例化      | https://github.com/vim-scripts/vlog_inst_gen.git             |
| ctags              | ctags模块标签        | 使用sudo apt install ctags 命令直接安装 官网：[Exuberant Ctags](https://ctags.sourceforge.net/) |

## description

> 👀可以直接查看**Rongye**的[博客](https://rongyel.top/posts/f60848c2.html), 介绍的很详细！

仅支持Gvim 8.0以上版本，基于VIM 8 pack特性进行插件管理。

ale需要补充安装iverilog才能进行语法检查, ctags也需要另外安装。

### nerdtree

文件目录树

```shell
"-----------------------------------------------------------------------------
" plugin: NERDTree
"-----------------------------------------------------------------------------
map <leader>ne :NERDTreeToggle<CR>
let g:NERDTreeWinSize = 25 " set nerdtree size
let NERDTreeIgnore=['\.pyc','\~$','\.swp'] " ignore the display of the following files
let NERDTreeShowHidden=1 " show hidden files
let g:NERDTreeDirArrowExpandable = '▸' " modify the default arrow symbol
let g:NERDTreeDirArrowCollapsible = '▾'
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
" nerdtree hot key mapping
map <F5> :NERDTreeMirror<CR>
map <F5> :NERDTreeToggle<CR>
map <leader>f :NERDTreeFind<CR>
```

- 按**ct**展开/关闭目录树
- 光标移动到需打开的文件
  - o：打开到当前窗口
  - t：打开并新建标签页到当前窗口，

### nerdcommenter

快速注释

```shell
"-----------------------------------------------------------------------------
" plugin: neocomplcache
"-----------------------------------------------------------------------------
let g:neocomplcache_enable_at_startup = 1 " auto start neocomplcache  
let g:neocomplcache_enable_auto_select = 1 " auto select the first item in the list
let g:neocomplcache_min_syntax_length = 2 " Set minimum syntax keyword length.
let g:neocomplcache_lock_buffer_name_pattern = '\*ku\*'
" inoremap <expr><CR>  neocomplcache#smart_close_popup() . "\<CR>"
inoremap <expr><C-Y>  neocomplcache#close_popup()
inoremap <expr><space>  neocomplcache#undo_completion()
inoremap <expr><Enter>  pumvisible() ? "\<C-Y>" : "\<Enter>"  
```

- cc : 注释
- cu: 取消注释
- c<空格>: 最常用的操作，可以自动判断是注释还是取消注释
- cA: 大写A，也就是shift + a, 在行末添加注释

### vim-airline

状态栏美化

```shell
"-----------------------------------------------------------------------------
" plugin: airline
"-----------------------------------------------------------------------------
let g:airline_theme='base16_gruvbox_dark_hard'
```

底部的状态栏美化

### vim-snippets

代码片段库

在`.vim\pack\default\start\vim-snippets`中可以添加自己的代码片段。

### vim-snipmate

代码片段展开

```shell
"-----------------------------------------------------------------------------
" plugin: snipmate
"-----------------------------------------------------------------------------
imap <tab> <Plug>snipMateTrigger " tab expand code snippets
imap <tab> <Plug>snipMateNextOrTrigger
imap <C-tab> <Plug>snipMateShow " tab expand code snippets list
```

在上面vim-snippets中添加了代码片段后, 输入代码片段的名字，按tab键可以展开该代码片段。

### vim-easy-align

代码对齐

```shell
"-----------------------------------------------------------------------------
" plugin: easyalign
"-----------------------------------------------------------------------------
" Start interactive EasyAlign in visual mode (e.g. vipga)
xmap ga <Plug>(EasyAlign)
" Start interactive EasyAlign for a motion/text object (e.g. gaip)
nmap ga <Plug>(EasyAlign)
```

一般依据空格，逗号, 等号来完成代码的对齐。

选中对齐的代码后，输入ga+对齐依据，例如ga=: 根据等号进行对齐。

建议不要全选代码对齐，效果不好。小范围对齐即可。

例子：先根据**“=”**进行对齐，再根据**“,”**进行对齐。

### neocomplcache

代码补全

```shell
"-----------------------------------------------------------------------------
" plugin: neocomplcache
"-----------------------------------------------------------------------------
let g:neocomplcache_enable_at_startup = 1 " auto start neocomplcache  
let g:neocomplcache_enable_auto_select = 1 " auto select the first item in the list
let g:neocomplcache_min_syntax_length = 2 " Set minimum syntax keyword length.
let g:neocomplcache_lock_buffer_name_pattern = '\*ku\*'
" inoremap <expr><CR>  neocomplcache#smart_close_popup() . "\<CR>"
inoremap <expr><C-Y>  neocomplcache#close_popup()
inoremap <expr><space>  neocomplcache#undo_completion()
inoremap <expr><Enter>  pumvisible() ? "\<C-Y>" : "\<Enter>"  
```

根据缓存信息，判断需要输入的内容是什么。

除了代码外，路径之类的也是可以补全的。

输入部分内容，会自动展开补全列表，ctrl+n下移，回车确定补全。

### auto-pairs

输入括号时自动成对出现。

### ale

语法检查

```shell
"-----------------------------------------------------------------------------
" plugin: ale
"-----------------------------------------------------------------------------
"keep the sign gutter open
let g:ale_sign_column_always = 1
let g:ale_sign_error = '>>'
let g:ale_sign_warning = '--'
" show errors or warnings in my statusline
let g:airline#extensions#ale#enabled = 1 
" use quickfix list instead of the loclist
let g:ale_set_loclist = 0
let g:ale_set_quickfix = 1
" only enable these linters
let g:ale_linters = {
\    'verilog': ['iverilog']
\}
nmap <silent> <C-k> <Plug>(ale_previous_wrap)
nmap <silent> <C-J> <Plug>(ale_next_wrap)
```

注意，需要补充安装iverilog才能使用

除了iverilog，还有其他语法工具可以使用，详见插件[github](https://github.com/dense-analysis/ale.git)。

### gruvbox

色彩空间, 作者Rongye的b站视频: [Gvim自定义色彩方案](https://www.bilibili.com/video/BV1sb4y1y78f/)

### indentLine

缩进标识

比较容易判断缩进情况，以4个空格为一个缩进单位。

### vlog_inst_gen

```shell
"-----------------------------------------------------------------------------
" plugin: vlogInst
"-----------------------------------------------------------------------------
so ~/.vim/pack/default/start/vlog_inst_gen/vlog_inst_gen.vim " set path

" key: (,ig)
```

- **,ig**: 生成当前文件的例化文件，会自动存储到剪贴板中。按esc退出冒出的信息，在需要例化的地方粘贴代码。

### ctags

模块标签

该功能其实不是一个插件，需自行安装ctags。

- gi ：进入光标所在的未知的模块端口。
- go: 退出到上一级模块。

### matchit

matchit 是 Vim 的一个内置插件，默认已安装但未启用

在 vimrc 中添加以下代码以启用 matchit：

```shell
runtime macros/matchit.vim
```

```shell
let b:match_words='\<begin\>:\<end\>,' .
    \ '\<if\>:\<elseif\>:\<else\>,' .
    \ '\<module\>:\<endmodule\>,' .
    \ '\<task\>:\<endtask\>,' .
    \ '\<function\>:\<endfunction\>,' . 
    \ '\<program\>:\<endprogram\>,' .
    \ '\<ifdef\>:\<elsif\>:\<else\>:\<endif\>,' .
    \ '\<ifndef\>:\<endif\>,' .
    \ '\<class\>:\<endclass\>'
```

- 使用%可以在匹配词之间跳转跳转

