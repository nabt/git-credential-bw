# git-credential-bw
Git credential helper script that integrates with the Bitwarden CLI

## Installation
Add `git-credential-bw` script to a directory in your PATH.

## Configure git to use the helper
### Add to global config

```
git config --global credential.helper bw
```

### Add to local config

```
git config --local credential.username [username]
git config --local credential.helper bw
```

### Personal Access Tokens
If a perstonal access token is used, instead of a password, add a hidden field with a name of "pat" containing the token value to the Bitwarden entry.

### How it works
The helper first searches for entries in Bitwarden with a value matching the `host` of the git repository.

The helper then filters the list by the login name provided by git (credential.username or manually entered)

Once it finds a match, it provides the following back to `git-credential`:

```
protocol=[protocol passed by `git-credential`]
host=[host provided by `git-credential`]
username=[username provided by `git-credential`]
password=[pat field value, if it exists, or password value]
```

### Logging
Log output can be found at ${HOME}/tmp/logs/git-credential-bw.log

## Additional tools
### Add `bw-functions` to your bash config
Add the following to your shell login script:

```
source /path/to/bw-functions
```

Restart your shell session, and type `bw-unlock`.  The function will step you through the `bw` session creation process, and export the session token to a global environment variable, named `BW_SESSION`.  This is the variable that `bw` uses for session verification, and allows for use of the Bitwarden CLI without the need to provide a password every time."
