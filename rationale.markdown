# Metadata for shell commands. #

I'm looking for a way to store and query shell commands and give them metadata to make querying easier.

## Motivation ##

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

We have  [`.desktop` files](http://standards.freedesktop.org/desktop-entry-spec/latest/ar01s05.html) for assigning metadata to applications, but there's no convenient way to interactively query them and they don't have nearly the metadata that would be useful for shell commands (see below).

There's adequate information in the man or info pages, but they don't tell you how to use commands and shell variables together, like this:

    chsh --shell $(which zsh) $USER

Man pages and info pages don't document all behavior, either; `date -I` works just fine, but it's
[undocumented](https://lists.gnu.org/archive/html/bug-coreutils/2006-01/msg00155.html).

Finally, search engines are great, but searching for shell commands is a nuisance. All major search engines ignore most punctuation even when it's quoted. It's non-trivial to figure out what this command does using only a search engine:

    mv -- * .[^.]* ..

<https://www.google.com/search?q=mv+--+*+.[^.]*+..>

<https://duckduckgo.com/?q=mv+--+*+.[^.]*+..>

<http://www.bing.com/search?q=mv+--+*+.[^.]*+..>

<http://explainshell.com/explain?cmd=mv+--+*+.[^.]*+..>

(In case you're curious, it moves all files in the current directory, including hidden files, to the parent directory.)

Search engines have other drawbacks; they require an internet connection and can't be easily customized.

## Requirements ##

I want to be able to search though a list of candidate shell commands based on metadata that is not part of the command.

For example, I want to be able to search for `exec` without getting matches for a `find -exec` command or a command with `execute` in the description, and I want to be able to do a search that distinguishes between the shell builtin `echo` and the coreutils `echo`. (Try comparing `echo --help` and `/bin/echo --help` to see what I mean.)

Ideally this would be a textual database with commands indexed by e.g. CRC checksum for things like linking to related commands.

Incremental search would be nice, too, but not mandatory.

I've been trying to find existing software that meets most of these requirements, and I haven't had much luck. I'd prefer not to start from scratch.

## Example metadata ##

Here's an example of a one-liner with some useful metadata to show what I mean:

* command:
 
`ping -i 2 localhost | sed -u 's/.*/ping/' | espeak`

* command with long flags:

`ping -i 2 localhost | sed --unbuffered 's/.*/ping/' | espeak`

* description: Generates audible voice that says "ping" every 2 seconds.

* commands: `ping`, `sed`, `espeak`

* command types: `file`, `file`, `file`
(this is the output of `type -t`, so `cd` is a `builtin` but `if` is a `keyword`)

* changeable argument: localhost

* argument type: IPv4 address or fully qualified domain name.

* changeable argument: 2

* argument type: Time interval in seconds.

* compatible with shells: bash, dash, zsh, fish

* requires internet connection: maybe

* keystroke to end: ctrl-c

* requires sudo: no

* informational URL: <http://ftp.arl.mil/mike/ping.html>

* thread-safe: yes

* uses pipes: yes

* current working directory matters: no

* modifies other processes: no

* modifies filesystem: no

* creates subshell: no

* creates subprocess: no

* byte count: 51
 
* CRC checksum: 3025175151

* related commands: 1234567890, 0987654321

## Example queries ##

A search in commands for `ping espeak` should return this candidate.

A a search in commands for `ping` and in description for `voice` should return this candidate.

A search in commands for `ping` and in `uses pipes` for `yes` or `true` or `maybe` should return this candidate.

A search in commands for `ping` and in command-type for `file` should return this candidate.

## Related discussion ##

<https://www.reddit.com/r/fossconfession/comments/2gjwhw/i_cant_remember_how_to_use_bash_process/>

The difficulties of remembering how to use shell commands; process substitution, in this case.

<https://unix.stackexchange.com/questions/26245/how-to-quickly-store-and-access-often-used-commands>

Suggests using comments in shell history as tags or making a bunch of aliases, but this has the same problem with finding things later.

<https://www.reddit.com/r/linux4noobs/comments/1k8etl/whats_the_best_way_to_rememberstore_commands/>

Same suggestions with shell history or using `--help` and `man`.

<http://forums.debian.net/viewtopic.php?f=30&t=111063>

Some good suggestions, but nothing about metadata.