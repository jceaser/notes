# Learning TMUX #

## What is TMUX ##
A Terminal multiplexer: allowing you to have multiple terminal sessions within
a single terminal.

## Why ##
There are several reasons you might want to use tmux:
* running processes on a remote server
* switch from laptop to desktop and maintain remote terminal
* running related applications (web server, editor, log output)

## Installing ##
`brew install tmux`

For this example you will want to make sure you have at least version 2 of tmux. 

    >tmux -V
    tmux 2.7

# Basic Commands #
Tmux works by routing keyboard input and console output between you and the many
terminals you may be running. All keystrokes are passed through tmux to your
terminal, that is unless you use the "prefix". Typing `ctrl+b` will instruct tmux
that the following keystrokes are tmux commands. More on this latter, just about
everything here will be prefixed with this command, but first lets see how to get
in and out of tmux

## Attaching and detaching ##

Launch tmux with `tmux` - note the menu at the bottom. At this point you have one
terminal running, if you type `exit` you will be closing the only terminal tmux
is managing and tmux will exit out.

On the command line you can do the following:

* `tmux` - launch a new tmux session
* `tmux ls` - list existing tmux sessions
* `tmux a -t 0` - "attach" to the first session - more on this
* `tmux new -s <session name>` - create a new session, naming it

Once inside tmux you can "detach" (disconect but leave tmux running) by typing the following command:

* `ctrl+b d` - d for "detach"

Now create a named session with: `tmux new -s learning`.

To test things out run the following:

1. `watch date` or `cat /dev/random | strings` - something that runs forever
1. `ctrl+b d` - to detach
1. `tmux ls` - show running sessions
1. `tmux a -t learning` - connect to our running session
1. note that the command is still running 
1. `ctrl-c` - to kill the command at step 1.

Finally:
`tmux kill-session -t <session name>` - to destroy a session

## Creating Multiple Panels ##

Lets see how more then can be done at once. You can split the screen and run two terminals with the `ctrl+b %` command. This will split the screen vertically. To remember this I think of the % as two objects split by a pipe:

    o|o

Split the screen horizontally with `ctrl+b "`, I have no convent way to remember that one. One of the reasons I don't remember the horizontal split command is because I use the next command to "change the layout" of the panels. `ctrl+space` will arrange the panels into different layouts. Go ahead and add pannels till you have three or four (using `ctrl+b %`) and then use the `ctrl+b space` command. Each time you press the layout command you get a new layout, there are a few, cycle through them till you see them repeat or find one you like. For three panels I'm pretty fond of this one:

    |----------------------|----------------------|
    |>vim                  |>rails s              |
    |                      |                      |
    |                      |                      |
    |                      |                      |
    |                      |----------------------|
    |                      |>git                  |
    |                      |                      |
    |                      |                      |
    |                      |                      |
    |----------------------|----------------------|

Some commands will let you interact directly with panels, like moving them around or jumping directly to them. Each panel has a number, to see these numbers use `ctrl+b q`. 

## Navigation ##

Now that you have multiple panels, you'll need to know how to move around. This is pretty easy. Your primary panel will be the one you can type in. Sometimes (depending on terminal emulator and font) you can use the `ctrl+b m` to "mark" the panel your in by highligting all or some of it's borders. Once you figure out which panel your in, you can use `ctrl+b` plus an arrow key to switch to the panel in the direction of the arrow you selected. Panel order wrappes around the screen, so if your on the right hand side and you press right, you end up on the far left. If you get lost, try using `ctrl+b m` to "mark" the boarder of your active panel (sometimes it get's confused on vertical panels)

* `ctrl+b →` - right
* `ctrl+b ←` - left
* `ctrl+b ↑` - up
* `ctrl+b ↓` - down
* `ctrl+b q <number>` - panel number typed while numbers are visible

While not exactly navigation, you can "zoom" in to the active panel, that is expand it to the full size while still not loosing the other panels. Do this with `ctrl-b z`. Reverse it with the same command.

You can also swap out panels, use { and } to switch out pannels that are next to each other on the same row (right-left).

* `ctrl+b {` - swap left
* `ctrl+b }` - swap right

## Windows ##

So far we have been working with just one window, that is one set of panels you view at once. To "create" a new window for new panels use `ctrl-b c`. You should have a new view with just one panel, but also, the "tab bar" at the bottom should show a new entry on the left. These tabs start with a number, the window number with the active window ending with an asterisk. You can rename these windows to "name" your collection of panels with `ctrl-b ,`, at the prompt (in the tab bar) type in a name and hit enter. To switch back and forth use the window picker with `ctrl-b w`, then use the arrows to pick your session. Pressing enter will activate your selection. Depending on your version, you may also see other sessions. You can open or collapse these with the right and left arrow.

Each window will have a number before the name. You can jump directly to any of the first 10 by using it's number in `ctrl-b <number>` where 
"<number>" is the window number.

# Other #

For absolutly no reason, you can display a clock in a panel.

`ctrl+b t` - press the any key to exit

# Advanced #

## Advanced Panel Resize ##

All commands have a long form which can be entered into the command prompt. The command prompt allows you to type a more complicated command that normal and is activated when you press the enter key. To resize a panel down by two lines try the following:

`ctrl+b :` then `resize-pane -D 2`

# Problems #
So not everything goes well, here are some work arounds

## Scrolling ##

So scrolling can be an issue. There are some plugins that can be used in some xterm clients. But the most basic and built in way to deal with scrolling a panel is to use the scroll mode.

`ctrl+b [` - enter scroll mode, `esc` to return

Then you can use the arrow keys to go up and down, page up and page down also works. q gets you out.

## Clipboard ##

With virtical panels it can be hard to copy multiple lines as the mouse will select any terminal text on the same row. This is because the host terminal does not know how tmux has broken up the screen. To get around this, use the copy mode in tmux. Copy mode is the same mode used to scroll but with some extra commands.

1. `ctrl+b [` - enter copy mode
2. use arrows to position where you want to **start** copy
3. `space` - to start copy
4. use arrows to position where you want to **stop** copy
5. `enter` to end
6. `ctrl+b ]` - paste text from copy mode

# Commands Reference #

* `ctrl+b d` - detach
* `ctrl+b c` - create window
* `ctrl+b %` - split window vertically (add panel)
* `ctrl+b "` - split window horizontally (add panel)
* `ctrl+b space` - arrange panels
* `ctrl+b m` - mark the active panel ; highlight active panel borders
* `ctrl+b →` - move focus right
* `ctrl+b ←` - move focus left
* `ctrl+b ↑` - move focus up
* `ctrl+b ↓` - move focus down
* `ctrl+b q <number>` - panel number typed while numbers are visible
* `ctrl+b z` - zoom a panel
* `ctrl+b {` - swap left
* `ctrl+b }` - swap right
* `ctrl+b $` - rename session
* `ctrl+b ,` - rename window
* `ctrl+b w` - pick window
* `ctrl+b <number>` - jump to numbered window
* `ctrl+b :` - command mode
* `ctrl+b [` - copy mode / scroll mode
* `ctrl+b ]` - paste clipboard

* `ctrl+b t` - a clock

# Scripting #
TMUX commands can be written to file and loaded inside TMUX. You can do this to setup your windows and standard layouts if you have such a thing:

    start-server

    new-session a -s "remotes"
    rename-session "remotes"
    new-window -n "mdlb"
    select-pane -t 0
    split-window -t "serv1" -h
    split-window -t "serv2" -v
    split-window -t "serv3" -v
    select-layout tiled
Then the file can be loaded with the command:

`ctr-b :` -> `source-file <file>`

# Sharing Sessions #

add more content

/tmp/tmux-501/default

however just use `tmux -S ~/somefile` instead

# Further Reading #
* https://gist.github.com/MohamedAlaa/2961058

