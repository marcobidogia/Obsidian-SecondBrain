# ⌨️ Keymaps

**LazyVim** uses [which-key.nvim](https://github.com/folke/which-key.nvim) to help you remember your keymaps. Just press any key like `<space>` and you'll see a popup with all possible keymaps starting with `<space>`.

![image](https://user-images.githubusercontent.com/292349/211862473-1ff5ee7a-3bb9-4782-a9f6-014f0e5d4474.png)

- default `<leader>` is `<space>`
- default `<localleader>` is `\`

## General

|Key|Description|Mode|
|---|---|---|
|`j`|Down|**n**, **x**|
|`<Down>`|Down|**n**, **x**|
|`k`|Up|**n**, **x**|
|`<Up>`|Up|**n**, **x**|
|`<C-h>`|Go to Left Window|**n**, **t**|
|`<C-j>`|Go to Lower Window|**n**, **t**|
|`<C-k>`|Go to Upper Window|**n**, **t**|
|`<C-l>`|Go to Right Window|**n**, **t**|
|`<C-Up>`|Increase Window Height|**n**|
|`<C-Down>`|Decrease Window Height|**n**|
|`<C-Left>`|Decrease Window Width|**n**|
|`<C-Right>`|Increase Window Width|**n**|
|`<A-j>`|Move Down|**n**, **i**, **v**|
|`<A-k>`|Move Up|**n**, **i**, **v**|
|`<S-h>`|Prev Buffer|**n**|
|`<S-l>`|Next Buffer|**n**|
|`[b`|Prev Buffer|**n**|
|`]b`|Next Buffer|**n**|
|`<leader>bb`|Switch to Other Buffer|**n**|
|`` <leader>` ``|Switch to Other Buffer|**n**|
|`<leader>bd`|Delete Buffer|**n**|
|`<leader>bD`|Delete Buffer and Window|**n**|
|`<esc>`|Escape and Clear hlsearch|**i**, **n**|
|`<leader>ur`|Redraw / Clear hlsearch / Diff Update|**n**|
|`n`|Next Search Result|**n**, **x**, **o**|
|`N`|Prev Search Result|**n**, **x**, **o**|
|`<C-s>`|Save File|**i**, **x**, **n**, **s**|
|`<leader>K`|Keywordprg|**n**|
|`gco`|Add Comment Below|**n**|
|`gcO`|Add Comment Above|**n**|
|`<leader>l`|Lazy|**n**|
|`<leader>fn`|New File|**n**|
|`<leader>xl`|Location List|**n**|
|`<leader>xq`|Quickfix List|**n**|
|`[q`|Previous Quickfix|**n**|
|`]q`|Next Quickfix|**n**|
|`<leader>cf`|Format|**n**, **v**|
|`<leader>cd`|Line Diagnostics|**n**|
|`]d`|Next Diagnostic|**n**|
|`[d`|Prev Diagnostic|**n**|
|`]e`|Next Error|**n**|
|`[e`|Prev Error|**n**|
|`]w`|Next Warning|**n**|
|`[w`|Prev Warning|**n**|
|`<leader>uf`|Toggle Auto Format (Global)|**n**|
|`<leader>uF`|Toggle Auto Format (Buffer)|**n**|
|`<leader>us`|Toggle Spelling|**n**|
|`<leader>uw`|Toggle Word Wrap|**n**|
|`<leader>uL`|Toggle Relative Line Numbers|**n**|
|`<leader>ul`|Toggle Line Numbers|**n**|
|`<leader>ud`|Toggle Diagnostics|**n**|
|`<leader>uc`|Toggle Conceal|**n**|
|`<leader>uh`|Toggle Inlay Hints|**n**|
|`<leader>uT`|Toggle Treesitter Highlight|**n**|
|`<leader>ub`|Toggle Background|**n**|
|`<leader>gg`|Lazygit (Root Dir)|**n**|
|`<leader>gG`|Lazygit (cwd)|**n**|
|`<leader>gb`|Git Blame Line|**n**|
|`<leader>gf`|Lazygit Current File History|**n**|
|`<leader>gl`|Lazygit Log|**n**|
|`<leader>qq`|Quit All|**n**|
|`<leader>ui`|Inspect Pos|**n**|
|`<leader>uI`|Inspect Tree|**n**|
|`<leader>L`|LazyVim Changelog|**n**|
|`<leader>ft`|Terminal (Root Dir)|**n**|
|`<leader>fT`|Terminal (cwd)|**n**|
|`<c-/>`|Terminal (Root Dir)|**n**|
|`<c-_>`|which_key_ignore|**n**, **t**|
|`<esc><esc>`|Enter Normal Mode|**t**|
|`<C-/>`|Hide Terminal|**t**|
|`<leader>ww`|Other Window|**n**|
|`<leader>wd`|Delete Window|**n**|
|`<leader>w-`|Split Window Below|**n**|
|`<leader>w\|`|Split Window Right|**n**|
|`<leader>-`|Split Window Below|**n**|
|`<leader>\|`|Split Window Right|**n**|
|`<leader><tab>l`|Last Tab|**n**|
|`<leader><tab>f`|First Tab|**n**|
|`<leader><tab><tab>`|New Tab|**n**|
|`<leader><tab>]`|Next Tab|**n**|
|`<leader><tab>d`|Close Tab|**n**|
|`<leader><tab>[`|Previous Tab|**n**|

## LSP

|Key|Description|Mode|
|---|---|---|
|`<leader>cl`|Lsp Info|**n**|
|`gd`|Goto Definition|**n**|
|`gr`|References|**n**|
|`gD`|Goto Declaration|**n**|
|`gI`|Goto Implementation|**n**|
|`gy`|Goto T[y]pe Definition|**n**|
|`K`|Hover|**n**|
|`gK`|Signature Help|**n**|
|`<c-k>`|Signature Help|**i**|
|`<leader>ca`|Code Action|**n**, **v**|
|`<leader>cc`|Run Codelens|**n**, **v**|
|`<leader>cC`|Refresh & Display Codelens|**n**, **n**|
|`<leader>cR`|Rename File|**n**, **n**|
|`<leader>cA`|Source Action|**n**|
|`]]`|Next Reference|**n**|
|`[[`|Prev Reference|**n**|
|`<a-n>`|Next Reference|**n**|
|`<a-p>`|Prev Reference|**n**|
|`<leader>cr`|Rename|**n**|

## [bufferline.nvim](https://github.com/akinsho/bufferline.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>bl`|Delete Buffers to the Left|**n**|
|`<leader>bo`|Delete Other Buffers|**n**|
|`<leader>bp`|Toggle Pin|**n**|
|`<leader>bP`|Delete Non-Pinned Buffers|**n**|
|`<leader>br`|Delete Buffers to the Right|**n**|
|`[b`|Prev Buffer|**n**|
|`]b`|Next Buffer|**n**|
|`<S-h>`|Prev Buffer|**n**|
|`<S-l>`|Next Buffer|**n**|

## [conform.nvim](https://github.com/stevearc/conform.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>cF`|Format Injected Langs|**n**, **v**|

## [flash.nvim](https://github.com/folke/flash.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<c-s>`|Toggle Flash Search|**c**|
|`r`|Remote Flash|**o**|
|`R`|Treesitter Search|**o**, **x**|
|`s`|Flash|**n**, **o**, **x**|
|`S`|Flash Treesitter|**n**, **o**, **x**|

## [mason.nvim](https://github.com/williamboman/mason.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>cm`|Mason|**n**|

## [mini.pairs](https://github.com/echasnovski/mini.pairs.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>up`|Toggle Auto Pairs|**n**|

## [neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>be`|Buffer Explorer|**n**|
|`<leader>e`|Explorer NeoTree (Root Dir)|**n**|
|`<leader>E`|Explorer NeoTree (cwd)|**n**|
|`<leader>fe`|Explorer NeoTree (Root Dir)|**n**|
|`<leader>fE`|Explorer NeoTree (cwd)|**n**|
|`<leader>ge`|Git Explorer|**n**|

## [noice.nvim](https://github.com/folke/noice.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<c-b>`|Scroll Backward|**n**, **i**, **s**|
|`<c-f>`|Scroll Forward|**n**, **i**, **s**|
|`<leader>sna`|Noice All|**n**|
|`<leader>snd`|Dismiss All|**n**|
|`<leader>snh`|Noice History|**n**|
|`<leader>snl`|Noice Last Message|**n**|
|`<leader>snt`|Noice Telescope|**n**|
|`<S-Enter>`|Redirect Cmdline|**c**|

## [nvim-notify](https://github.com/rcarriga/nvim-notify.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>un`|Dismiss All Notifications|**n**|

## [nvim-spectre](https://github.com/nvim-pack/nvim-spectre.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>sr`|Replace in Files (Spectre)|**n**|

## [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter.git)

|Key|Description|Mode|
|---|---|---|
|`<bs>`|Decrement Selection|**x**|
|`<c-space>`|Increment Selection|**n**|

## [persistence.nvim](https://github.com/folke/persistence.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>qd`|Don't Save Current Session|**n**|
|`<leader>ql`|Restore Last Session|**n**|
|`<leader>qs`|Restore Session|**n**|

## [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<leader><space>`|Find Files (Root Dir)|**n**|
|`<leader>,`|Switch Buffer|**n**|
|`<leader>/`|Grep (Root Dir)|**n**|
|`<leader>:`|Command History|**n**|
|`<leader>fb`|Buffers|**n**|
|`<leader>fc`|Find Config File|**n**|
|`<leader>ff`|Find Files (Root Dir)|**n**|
|`<leader>fF`|Find Files (cwd)|**n**|
|`<leader>fg`|Find Files (git-files)|**n**|
|`<leader>fr`|Recent|**n**|
|`<leader>fR`|Recent (cwd)|**n**|
|`<leader>gc`|Commits|**n**|
|`<leader>gs`|Status|**n**|
|`<leader>s"`|Registers|**n**|
|`<leader>sa`|Auto Commands|**n**|
|`<leader>sb`|Buffer|**n**|
|`<leader>sc`|Command History|**n**|
|`<leader>sC`|Commands|**n**|
|`<leader>sd`|Document Diagnostics|**n**|
|`<leader>sD`|Workspace Diagnostics|**n**|
|`<leader>sg`|Grep (Root Dir)|**n**|
|`<leader>sG`|Grep (cwd)|**n**|
|`<leader>sh`|Help Pages|**n**|
|`<leader>sH`|Search Highlight Groups|**n**|
|`<leader>sj`|Jumplist|**n**|
|`<leader>sk`|Key Maps|**n**|
|`<leader>sl`|Location List|**n**|
|`<leader>sm`|Jump to Mark|**n**|
|`<leader>sM`|Man Pages|**n**|
|`<leader>so`|Options|**n**|
|`<leader>sq`|Quickfix List|**n**|
|`<leader>sR`|Resume|**n**|
|`<leader>ss`|Goto Symbol|**n**|
|`<leader>sS`|Goto Symbol (Workspace)|**n**|
|`<leader>sw`|Word (Root Dir)|**n**|
|`<leader>sW`|Word (cwd)|**n**|
|`<leader>sw`|Selection (Root Dir)|**v**|
|`<leader>sW`|Selection (cwd)|**v**|
|`<leader>uC`|Colorscheme with Preview|**n**|

## [todo-comments.nvim](https://github.com/folke/todo-comments.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>st`|Todo|**n**|
|`<leader>sT`|Todo/Fix/Fixme|**n**|
|`<leader>xt`|Todo (Trouble)|**n**|
|`<leader>xT`|Todo/Fix/Fixme (Trouble)|**n**|
|`[t`|Previous Todo Comment|**n**|
|`]t`|Next Todo Comment|**n**|

## [trouble.nvim](https://github.com/folke/trouble.nvim.git)

|Key|Description|Mode|
|---|---|---|
|`<leader>xL`|Location List (Trouble)|**n**|
|`<leader>xQ`|Quickfix List (Trouble)|**n**|
|`<leader>xx`|Document Diagnostics (Trouble)|**n**|
|`<leader>xX`|Workspace Diagnostics (Trouble)|**n**|
|`[q`|Previous Trouble/Quickfix Item|**n**|
|`]q`|Next Trouble/Quickfix Item|**n**|

## [CopilotChat.nvim](https://github.com/CopilotC-Nvim/CopilotChat.nvim.git)

Part of [lazyvim.plugins.extras.coding.copilot-chat](http://www.lazyvim.org/extras/coding/copilot-chat)

|Key|Description|Mode|
|---|---|---|
|`<leader>aa`|Toggle (CopilotChat)|**n**, **v**|
|`<leader>aq`|Quick Chat (CopilotChat)|**n**, **v**|
|`<leader>ax`|Clear (CopilotChat)|**n**, **v**|

## [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim.git)

Part of [lazyvim.plugins.extras.coding.copilot-chat](http://www.lazyvim.org/extras/coding/copilot-chat)

|Key|Description|Mode|
|---|---|---|
|`<leader>ad`|Diagnostic Help (CopilotChat)|**n**, **v**|
|`<leader>ap`|Prompt Actions (CopilotChat)|**n**, **v**|

## [mini.surround](https://github.com/echasnovski/mini.surround.git)

Part of [lazyvim.plugins.extras.coding.mini-surround](http://www.lazyvim.org/extras/coding/mini-surround)

|Key|Description|Mode|
|---|---|---|
|`gsa`|Add Surrounding|**n**, **v**|
|`gsd`|Delete Surrounding|**n**|
|`gsf`|Find Right Surrounding|**n**|
|`gsF`|Find Left Surrounding|**n**|
|`gsh`|Highlight Surrounding|**n**|
|`gsn`|Update `MiniSurround.config.n_lines`|**n**|
|`gsr`|Replace Surrounding|**n**|

## [yanky.nvim](https://github.com/gbprod/yanky.nvim.git)

Part of [lazyvim.plugins.extras.coding.yanky](http://www.lazyvim.org/extras/coding/yanky)

|Key|Description|Mode|
|---|---|---|
|`<leader>p`|Open Yank History|**n**|
|`<p`|Put and Indent Left|**n**|
|`<P`|Put Before and Indent Left|**n**|
|`=p`|Put After Applying a Filter|**n**|
|`=P`|Put Before Applying a Filter|**n**|
|`>p`|Put and Indent Right|**n**|
|`>P`|Put Before and Indent Right|**n**|
|`[p`|Put Indented Before Cursor (Linewise)|**n**|
|`[P`|Put Indented Before Cursor (Linewise)|**n**|
|`[y`|Cycle Forward Through Yank History|**n**|
|`]p`|Put Indented After Cursor (Linewise)|**n**|
|`]P`|Put Indented After Cursor (Linewise)|**n**|
|`]y`|Cycle Backward Through Yank History|**n**|
|`gp`|Put Yanked Text After Selection|**n**, **x**|
|`gP`|Put Yanked Text Before Selection|**n**, **x**|
|`p`|Put Yanked Text After Cursor|**n**, **x**|
|`P`|Put Yanked Text Before Cursor|**n**, **x**|
|`y`|Yank Text|**n**, **x**|

## [nvim-dap](https://github.com/mfussenegger/nvim-dap.git)

Part of [lazyvim.plugins.extras.dap.core](http://www.lazyvim.org/extras/dap/core)

|Key|Description|Mode|
|---|---|---|
|`<leader>da`|Run with Args|**n**|
|`<leader>db`|Toggle Breakpoint|**n**|
|`<leader>dB`|Breakpoint Condition|**n**|
|`<leader>dc`|Continue|**n**|
|`<leader>dC`|Run to Cursor|**n**|
|`<leader>dg`|Go to Line (No Execute)|**n**|
|`<leader>di`|Step Into|**n**|
|`<leader>dj`|Down|**n**|
|`<leader>dk`|Up|**n**|
|`<leader>dl`|Run Last|**n**|
|`<leader>do`|Step Out|**n**|
|`<leader>dO`|Step Over|**n**|
|`<leader>dp`|Pause|**n**|
|`<leader>dr`|Toggle REPL|**n**|
|`<leader>ds`|Session|**n**|
|`<leader>dt`|Terminate|**n**|
|`<leader>dw`|Widgets|**n**|

## [nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui.git)

Part of [lazyvim.plugins.extras.dap.core](http://www.lazyvim.org/extras/dap/core)

|Key|Description|Mode|
|---|---|---|
|`<leader>de`|Eval|**n**, **v**|
|`<leader>du`|Dap UI|**n**|

## [aerial.nvim](https://github.com/stevearc/aerial.nvim.git)

Part of [lazyvim.plugins.extras.editor.aerial](http://www.lazyvim.org/extras/editor/aerial)

|Key|Description|Mode|
|---|---|---|
|`<leader>cs`|Aerial (Symbols)|**n**|

## [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim.git)

Part of [lazyvim.plugins.extras.editor.aerial](http://www.lazyvim.org/extras/editor/aerial)

|Key|Description|Mode|
|---|---|---|
|`<leader>ss`|Goto Symbol (Aerial)|**n**|

## [dial.nvim](https://github.com/monaqa/dial.nvim.git)

Part of [lazyvim.plugins.extras.editor.dial](http://www.lazyvim.org/extras/editor/dial)

|Key|Description|Mode|
|---|---|---|
|`<C-a>`|Increment|**n**, **v**|
|`<C-x>`|Decrement|**n**, **v**|
|`g<C-a>`|Increment|**n**, **v**|
|`g<C-x>`|Decrement|**n**, **v**|

## [harpoon](https://github.com/ThePrimeagen/harpoon.git)

Part of [lazyvim.plugins.extras.editor.harpoon2](http://www.lazyvim.org/extras/editor/harpoon2)

|Key|Description|Mode|
|---|---|---|
|`<leader>1`|Harpoon to File 1|**n**|
|`<leader>2`|Harpoon to File 2|**n**|
|`<leader>3`|Harpoon to File 3|**n**|
|`<leader>4`|Harpoon to File 4|**n**|
|`<leader>5`|Harpoon to File 5|**n**|
|`<leader>h`|Harpoon Quick Menu|**n**|
|`<leader>H`|Harpoon File|**n**|

## [vim-illuminate](https://github.com/RRethy/vim-illuminate.git)

Part of [lazyvim.plugins.extras.editor.illuminate](http://www.lazyvim.org/extras/editor/illuminate)

|Key|Description|Mode|
|---|---|---|
|`[[`|Prev Reference|**n**|
|`]]`|Next Reference|**n**|

## [flit.nvim](https://github.com/ggandor/flit.nvim.git)

Part of [lazyvim.plugins.extras.editor.leap](http://www.lazyvim.org/extras/editor/leap)

|Key|Description|Mode|
|---|---|---|
|`f`|f|**n**, **o**, **x**|
|`F`|F|**n**, **o**, **x**|
|`t`|t|**n**, **o**, **x**|
|`T`|T|**n**, **o**, **x**|

## [leap.nvim](https://github.com/ggandor/leap.nvim.git)

Part of [lazyvim.plugins.extras.editor.leap](http://www.lazyvim.org/extras/editor/leap)

|Key|Description|Mode|
|---|---|---|
|`gs`|Leap from Windows|**n**, **o**, **x**|
|`s`|Leap Forward to|**n**, **o**, **x**|
|`S`|Leap Backward to|**n**, **o**, **x**|

## [mini.diff](https://github.com/echasnovski/mini.diff.git)

Part of [lazyvim.plugins.extras.editor.mini-diff](http://www.lazyvim.org/extras/editor/mini-diff)

|Key|Description|Mode|
|---|---|---|
|`<leader>go`|Toggle mini.diff overlay|**n**|

## [mini.files](https://github.com/echasnovski/mini.files.git)

Part of [lazyvim.plugins.extras.editor.mini-files](http://www.lazyvim.org/extras/editor/mini-files)

|Key|Description|Mode|
|---|---|---|
|`<leader>fm`|Open mini.files (Directory of Current File)|**n**|
|`<leader>fM`|Open mini.files (cwd)|**n**|

## [outline.nvim](https://github.com/hedyhli/outline.nvim.git)

Part of [lazyvim.plugins.extras.editor.outline](http://www.lazyvim.org/extras/editor/outline)

|Key|Description|Mode|
|---|---|---|
|`<leader>cs`|Toggle Outline|**n**|

## [refactoring.nvim](https://github.com/ThePrimeagen/refactoring.nvim.git)

Part of [lazyvim.plugins.extras.editor.refactoring](http://www.lazyvim.org/extras/editor/refactoring)

|Key|Description|Mode|
|---|---|---|
|`<leader>rb`|Extract Block|**n**|
|`<leader>rc`|Debug Cleanup|**n**|
|`<leader>rf`|Extract Block To File|**n**|
|`<leader>rf`|Extract Function|**v**|
|`<leader>rF`|Extract Function To File|**v**|
|`<leader>ri`|Inline Variable|**n**, **v**|
|`<leader>rp`|Debug Print Variable|**n**, **v**|
|`<leader>rP`|Debug Print|**n**|
|`<leader>rs`|Refactor|**v**|
|`<leader>rx`|Extract Variable|**v**|

## [trouble.nvim](https://github.com/folke/trouble.nvim.git)

Part of [lazyvim.plugins.extras.editor.trouble-v3](http://www.lazyvim.org/extras/editor/trouble-v3)

|Key|Description|Mode|
|---|---|---|
|`<leader>cs`|Symbols (Trouble)|**n**|
|`<leader>cS`|LSP references/definitions/... (Trouble)|**n**|
|`<leader>xL`|Location List (Trouble)|**n**|
|`<leader>xQ`|Quickfix List (Trouble)|**n**|
|`<leader>xx`|Diagnostics (Trouble)|**n**|
|`<leader>xX`|Buffer Diagnostics (Trouble)|**n**|
|`[q`|Previous Trouble/Quickfix Item|**n**|

## [nvim-ansible](https://github.com/mfussenegger/nvim-ansible.git)

Part of [lazyvim.plugins.extras.lang.ansible](http://www.lazyvim.org/extras/lang/ansible)

|Key|Description|Mode|
|---|---|---|
|`<leader>ta`|Ansible Run Playbook/Role|**n**|

## [markdown-preview.nvim](https://github.com/iamcco/markdown-preview.nvim.git)

Part of [lazyvim.plugins.extras.lang.markdown](http://www.lazyvim.org/extras/lang/markdown)

|Key|Description|Mode|
|---|---|---|
|`<leader>cp`|Markdown Preview|**n**|

## [nvim-dap-python](https://github.com/mfussenegger/nvim-dap-python.git)

Part of [lazyvim.plugins.extras.lang.python](http://www.lazyvim.org/extras/lang/python)

|Key|Description|Mode|
|---|---|---|
|`<leader>dPc`|Debug Class|**n**|
|`<leader>dPt`|Debug Method|**n**|

## [venv-selector.nvim](https://github.com/linux-cultist/venv-selector.nvim.git)

Part of [lazyvim.plugins.extras.lang.python](http://www.lazyvim.org/extras/lang/python)

|Key|Description|Mode|
|---|---|---|
|`<leader>cv`|Select VirtualEnv|**n**|

## [nvim-metals](https://github.com/scalameta/nvim-metals.git)

Part of [lazyvim.plugins.extras.lang.scala](http://www.lazyvim.org/extras/lang/scala)

|Key|Description|Mode|
|---|---|---|
|`<leader>mc`|Metals compile cascade|**n**|
|`<leader>me`|Metals commands|**n**|

## [neotest](https://github.com/nvim-neotest/neotest.git)

Part of [lazyvim.plugins.extras.test.core](http://www.lazyvim.org/extras/test/core)

|Key|Description|Mode|
|---|---|---|
|`<leader>tl`|Run Last|**n**|
|`<leader>to`|Show Output|**n**|
|`<leader>tO`|Toggle Output Panel|**n**|
|`<leader>tr`|Run Nearest|**n**|
|`<leader>ts`|Toggle Summary|**n**|
|`<leader>tS`|Stop|**n**|
|`<leader>tt`|Run File|**n**|
|`<leader>tT`|Run All Test Files|**n**|

## [nvim-dap](https://github.com/mfussenegger/nvim-dap.git)

Part of [lazyvim.plugins.extras.test.core](http://www.lazyvim.org/extras/test/core)

|Key|Description|Mode|
|---|---|---|
|`<leader>td`|Debug Nearest|**n**|

## [edgy.nvim](https://github.com/folke/edgy.nvim.git)

Part of [lazyvim.plugins.extras.ui.edgy](http://www.lazyvim.org/extras/ui/edgy)

|Key|Description|Mode|
|---|---|---|
|`<leader>ue`|Edgy Toggle|**n**|
|`<leader>uE`|Edgy Select Window|**n**|

## [nvim-treesitter-context](https://github.com/nvim-treesitter/nvim-treesitter-context.git)

Part of [lazyvim.plugins.extras.ui.treesitter-context](http://www.lazyvim.org/extras/ui/treesitter-context)

|Key|Description|Mode|
|---|---|---|
|`<leader>ut`|Toggle Treesitter Context|**n**|

## [mason.nvim](https://github.com/williamboman/mason.nvim.git)

Part of [lazyvim.plugins.extras.util.gitui](http://www.lazyvim.org/extras/util/gitui)

|Key|Description|Mode|
|---|---|---|
|`<leader>gg`|GitUi (Root Dir)|**n**|
|`<leader>gG`|GitUi (cwd)|**n**|

## [project.nvim](https://github.com/ahmedkhalf/project.nvim.git)

Part of [lazyvim.plugins.extras.util.project](http://www.lazyvim.org/extras/util/project)

| Key          | Description | Mode  |
| ------------ | ----------- | ----- |
| `<leader>fp` | Projects    | **n** |