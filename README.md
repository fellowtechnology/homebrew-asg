# homebrew-asg

Homebrew tap for `asg`, the command-line tool and background daemon for ASG (All Systems Go).

> **Early release.** `v0.1.0` is for the ASG team. It talks to an API on `http://localhost:8080`, so run the ASG stack locally to sign in. macOS only (Apple Silicon and Intel).

## Install

```sh
brew tap fellowtechnology/asg
brew trust fellowtechnology/asg
brew install asg
asg version
```

Recent Homebrew versions refuse to load formulae from a third-party tap until you trust it. Without `brew trust`, `brew install asg` fails with `Refusing to load formula ... from untrusted tap`.

Start the background daemon (it keeps your session fresh and restarts at login):

```sh
brew services start asg
asg status
```

## Sign in

Use the account you created on the ASG website.

```sh
asg login                  # asks for email and password
asg login --web            # device login: confirm a code in the browser
asg whoami
asg logout
```

Useful flags for `asg login`: `--email`, `--password-stdin` (for scripts), `--no-browser` (print the link instead of opening it).

Your session is stored in the macOS Keychain, never in a file.

## Commands

| Command | What it does |
| --- | --- |
| `asg version` | Print the version |
| `asg status` | Show whether the daemon is running |
| `asg login` / `logout` / `whoami` | Sign in, sign out, show the current account |
| `asg daemon run` | Run the daemon in the foreground (`brew services` does this for you) |
| `asg uninstall` | Sign out and delete asg's local data (keychain item, daemon files); add `-y` to skip the prompt |

## Update

```sh
brew update
brew upgrade asg
```

## Uninstall

```sh
brew services stop asg
asg uninstall
brew uninstall asg
brew untap fellowtechnology/asg
```

The daemon log is at `$(brew --prefix)/var/log/asg.log`.

## For maintainers

Releases are published by GoReleaser from the private `all-systems-go` repository when a `v*` tag is pushed. It uploads the archives to this repo's Releases and updates `Formula/asg.rb` here. Do not edit the formula by hand; the next release overwrites it.
