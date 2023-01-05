# Better(tm) and Smarter(tm) bash initialization

## Intro
Once upon a time, I needed smarter bash initialization scripts. Smarter in a lot of senses. Basically, something that could be handled more easily than a single `.bashrc` file.  
This is my current iteration.

## `.bashrc`: The very beginning
Everything starts from the `.bashrc` file, as usual. My current version just skips everything else in case it is not run in interactive mode.  
Otherwise it passes the control (via `source` *built-in*) to the actual initialization code, contained in the `.rc` file.

## `.rc`: Looping through initialization scripts
This *script* is run within the very same context as the original (login) shell and loops through the files contained within a cofigurable directory, `${HOME}/.rc.d` by default.  
All readable files are `source`d in the order defined by the current (default) locale.  
Unreadable files are simply skipped.  
In my example I prefix file names with two digits number to make sure I have proper order of execution. Anything else can also be OK: YMMV.

## Some examples
As an example, I have added a few files with some stuff I normally setup for my `bash`. Just a few notes.  
1. I have a fancy prompt setup. It basically is a plain old prompt withing narrow screens (<= 80 columns).  
With wider screens it adds some interesting details: last command timestamp, optional git branch, optional non-trivial return code from previous command, userid and hostname, current path.
2. My locale is setup in my mother language (Italian) but I like to keep error messages in English and old-fashioned `ls` file sorting (ASCII-based).
3. I try to keep consistent time and date display format via my `TIMEFORMAT` variable. `HISTTIMEFORMAT` (history timestamps) and `TIME_STYLE` (`ls` time/date output) are defined from there.
4. My own macro names all have a leading *comma* `,` (it can also be a *colon* `:`) to avoid any command name conflict. Aliases instead have no *comma* to overrule the corresponding command.
5. `pathupdate` macro adds directories to the `PATH` variables if they are not already there. It helps preventing its overgrowth.

## Notes
1. You can embedd the `.rc` file in the `.bashrc`. You won't gain any noticeable init speedup at the possible cost of lesser flexibility.
2. Those are not script in the "*usual*" sense as they are lacking the *shebang* prologue. This ensures all setup actions happen within the (same) main shell.

## References
- [Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)
- [ls(1)](https://man7.org/linux/man-pages/man1/ls.1.html)
- [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))