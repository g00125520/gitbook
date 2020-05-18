# vim 

## table of contents
## skills

- ctl+v,shift+i,esc,同时在多列插入
- :g/^/m 0，倒序文件，tac，依次找到每一行，并将之移到0行。
- :g/^/+1 d，删除偶数行，+1定位当前行的下一行，将第二行删除后，第二行标记消失，所以不删除第三行，同：:%norm jdd。
- :g/^/d|m.，删除奇数行，用move命令把偶数行的标记去掉，%norm dd，删除整个文件，%norm jkdd，删除奇数行。
- :g/^/t.，double所有行，同：:%s/.*/&r&/，t是copy到自己下面。
- :g/ccc/if getline(‘.’) !~ ‘ddd’ | s/aaa/bbb/g，将aaa替换成bbb，条件是该行中有ccc但不能有ddd
- :%s/ +/\r/g，按照空格分为多行；
- :g/^s*$/d，删除空行；


<!-- vim-markdown-toc GFM -->

* [handle markdown](#handle-markdown)
* [plugins](#plugins)
* [colors](#colors)
* [python](#python)
* [ref](#ref)

<!-- vim-markdown-toc -->
## handle markdown

- [syntax highlighting,matching rules and mappings for the original markdown and extensions](https://github.com/plasticboy/vim-markdown)
- [instantly preview finicky markdown files](https://github.com/suan/vim-instant-markdown)
- [preview markdown](https://github.com/iamcco/markdown-preview.nvim)

## plugins

- [a minimalist vim plugin manager](https://github.com/junegunn/vim-plug)
- [multi cursors](https://github.com/terryma/vim-multiple-cursors)
- [vim wiki](https://www.vim.org/scripts/script.php?script_id=2226)
- [vnote](https://github.com/lymslive/vnote)
- [use vimloo to write classes](https://github.com/lymslive/vimloo)
- [async run](https://github.com/skywind3000/asyncrun.vim)
- [terminal in vim ](https://github.com/ZSaberLv0/ZFVimTerminal)

## colors 

- [monokai theme for textmate](https://github.com/tomasr/molokai.git)

## python


## ref

- [vimplus](https://github.com/chxuan/vimplus)
- [galore](https://github.com/wsdjeg/vim-galore-zh_cn)
- [vim script](https://github.com/lymslive/vimllearn/blob/master/content.md)
