I'm looking for a way to store and query commands and their metadata.

There are plenty of projects that try to make using shell commands easier:

<https://github.com/chrisallenlane/cheat>

<https://github.com/lucaswerkmeister/cheats>

<https://github.com/tldr-pages/tldr>

<http://bropages.org/>

However, they are limited to categorizing under single commands. Does counting files with `find . -type f | wc -l` go under `find` or `wc`?

We've also got an online, searchable repository of shell commands:

<http://www.commandlinefu.com/commands/browse>

But there's no separation between the command and the metadata, which makes efficient querying difficult.

For example, a search for `exec` returns results for the word "execute", the shell builtin `exec`, and the `find` command flag `-exec`.

<http://www.commandlinefu.com/commands/matching/exec/ZXhlYw==/sort-by-votes>

There's adequate information in the man pages, but man pages don't tell you how to use commands and shell variables together, like this:

    chsh --shell $(which zsh) $USER

Man pages don't document all behavior, either; `date -I` works just fine, but it's
[undocumented](https://lists.gnu.org/archive/html/bug-coreutils/2006-01/msg00155.html).

Finally, there is a lot of information a search engine query away, but searching for shell commands is a nuisance. Google ignores most punctuation and DuckDuckGo interprets `!` as commands.

Here's an example of a command with some useful metadata:

Related discussion:

<https://www.reddit.com/r/fossconfession/comments/2gjwhw/i_cant_remember_how_to_use_bash_process/>

<https://unix.stackexchange.com/questions/26245/how-to-quickly-store-and-access-often-used-commands>

Suggests using comments in shell history as tags or making a bunch of aliases, but this has the same problem with finding things later.

<https://www.reddit.com/r/learnprogramming/comments/1z6jd1/how_does_one_remember_commands_and_syntax/>

<https://www.reddit.com/r/linux4noobs/comments/1k8etl/whats_the_best_way_to_rememberstore_commands/>