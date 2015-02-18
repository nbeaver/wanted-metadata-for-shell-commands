I'm looking for a way to store and query shell commands and give them metadata to make querying easier.

There are plenty of projects that try to make remembering and using shell commands easier:

<https://github.com/chrisallenlane/cheat>

<https://github.com/lucaswerkmeister/cheats>

<https://github.com/tldr-pages/tldr>

<http://bropages.org/>

However, they are limited to categorizing under single commands. Does counting files with `find . -type f | wc -l` go under `find` or `wc`?

There's also got an online, searchable repository of shell commands:

<http://www.commandlinefu.com/commands/browse>

But there's no separation between the command and the metadata, which makes efficient querying difficult.

For example, a search for `exec` returns results for the word "execute", the shell builtin `exec`, and the `find` command flag `-exec`.

<http://www.commandlinefu.com/commands/matching/exec/ZXhlYw==/sort-by-votes>

There's adequate information in the man pages, but man pages don't tell you how to use commands and shell variables together, like this:

    chsh --shell $(which zsh) $USER

Man pages don't document all behavior, either; `date -I` works just fine, but it's
[undocumented](https://lists.gnu.org/archive/html/bug-coreutils/2006-01/msg00155.html).

Finally, search engines are great, but searching for shell commands is a nuisance. All major search engines ignore most punctuation even when it's quoted. Trying to find out what this command does by using a web search is non-trivial:

    mv -- * .[^.]* ..

<https://www.google.com/search?q=mv+--+*+.[^.]*+..>

<https://duckduckgo.com/?q=mv+--+*+.[^.]*+..>

<http://www.bing.com/search?q=mv+--+*+.[^.]*+..>

(It moves all files in the current directory, including hidden files, to the parent directory, by the way.)

Search engines have other drawbacks; they require an internet connection and don't have all the one might need commands.

Here's an example of a one-liner with some useful metadata:

* command:
 
`ping -i 2 localhost | sed -u 's/.*/ping/' | espeak`

* command with long flags:

`ping -i 2 localhost | sed --unbuffered 's/.*/ping/' | espeak`

* description: generates voice that says "ping" every 2 seconds.

* commands: ping, sed, espeak

* compatible with shells: bash, dash, zsh, fish

* requires internet connection: no

* command to end: ctrl-c

* requires sudo: no

* informational URL: <http://ftp.arl.mil/mike/ping.html>

* thread-safe: yes

* current working directory matters: no

* affects other processes: no

* modifies filesystem: no

* byte count: 51
 
* CRC checksum: 3025175151

Related discussion:

<https://www.reddit.com/r/fossconfession/comments/2gjwhw/i_cant_remember_how_to_use_bash_process/>

<https://unix.stackexchange.com/questions/26245/how-to-quickly-store-and-access-often-used-commands>

Suggests using comments in shell history as tags or making a bunch of aliases, but this has the same problem with finding things later.

<https://www.reddit.com/r/linux4noobs/comments/1k8etl/whats_the_best_way_to_rememberstore_commands/>

Same suggestions with shell history or using `--help` and `man`.