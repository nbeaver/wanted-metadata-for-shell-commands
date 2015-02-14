I'm looking for a way to store and query command metadata.

There are lots of programs to help remember how to use commands:

<https://github.com/chrisallenlane/cheat>

<https://github.com/lucaswerkmeister/cheats>

<https://github.com/tldr-pages/tldr>

However, they tend to be limited to categorizing single commands. Does counting files with `find . -type f | wc -l` go under `find` or `wc`?

They also tend to lack metadata, which makes querying difficult.

For example, a search for `exec` might return information about the shell builtin, or it might return information about `-exec`, the `find` command flag.

As I've been learning the command line, I've been keeping notes on how to use various commands in a single long text file. It's commented like a shell script, e.g.

    # Find out what kind of files are in the current directory and its subdirectories.
    find . -type f -exec file '{}' \; | less

Unfortunately, this file is getting big (more than 1000 lines excluding blank lines and comments) and it's becoming hard to find things.

For example, if I'm looking for examples on how to use the `cut(1)` command and I search for "cut", I get matches for "executable" and "shortcut", and if I search for " cut " I exclude lines that start with "cut" and get matches for how to cut a word in `bash` (Ctrl-W).

Because it's hard to find commands, I sometimes accidentally add duplicate (or nearly duplicate) commands and don't realize it until much later.

Sure, plenty of the information is in the man pages, but sometimes things are (e.g. `date -I` is [undocumented](https://lists.gnu.org/archive/html/bug-coreutils/2006-01/msg00155.html)), and a lot of it is adapted to specific examples I've used before.

Finally, there is a lot of infrmation a search engine query away, but searching for shell commands is a nuisance. Google ignores most punctuation and DuckDuckGo interprets `!` as commands.

Related discussion:

<https://www.reddit.com/r/fossconfession/comments/2gjwhw/i_cant_remember_how_to_use_bash_process/>

<https://unix.stackexchange.com/questions/26245/how-to-quickly-store-and-access-often-used-commands>

Suggests using comments in shell history as tags or making a bunch of aliases, but this has the same problem with finding things later.

<https://www.reddit.com/r/learnprogramming/comments/1z6jd1/how_does_one_remember_commands_and_syntax/>

<https://www.reddit.com/r/linux4noobs/comments/1k8etl/whats_the_best_way_to_rememberstore_commands/>