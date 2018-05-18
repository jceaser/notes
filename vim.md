# VIM Notes #
Some basic notes on how to use VIM

## Edit ##
* `vim scp://remoteuser@server.tld/relative/path/to/document`

## Split Screens ##
* `:split` - horizontal
* `:vsplit` - vertical split
* `<ctr-w> arrow` - to move to new screen

## buffers ##
* `:buffers` - list buffers
* `:bn` - next buffer
* `:bp` - previouse buffer
* `:e <file>` - edit file in new buffer
* `:bd` - delete buffer
* `:ls` - list current buffers

## tabs ##
* `:tabe` - edit in new tab

## Clipboard ##
* `y` - yank, copy before
* `yy` - yank, copy entire line
* `d` - delete, cut
* `p` - paste after
* `"ayy` - copy line to buffer "a"
* `"add` - cut line to buffer "a"
* `"ap` - paste line from buffer "a"
* `"Add` - cut and append to buffer "a"
* `:reg` - display registers

## other features ##
* `<ctr-r> =` - expression register (math)
* `:sh` - enter shell
* `:explore` - file explorer
* `:read !<cmd>` - appends cmd output
* `q:` - display command history
* `:nohlsearch` - clear highlighting
* `:set hlsearch` - turn search highlighting on
* `:set number` && `:set nonumber` - turn line number on and off
* `:set paste` && `:set nopaste` - turn paste mode on and off
* `au FileType script set makeprg=%` - configuration to set :make to run on current file

