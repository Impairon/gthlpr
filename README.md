                                                    ﷽ 
# gthlpr

`gthlpr` is a small Bash-based Git credential helper for Linux.

It manages Git credentials in a local protected database and integrates with Git's credential-helper protocol. The goal is to make working with repository tokens simple while keeping the credentials encrypted and out of normal Git configuration files.

## What it does

* Stores credentials per repository.
* Supports Git's `get`, `store`, and `erase` operations.
* Encrypts stored tokens with GPG.
* Uses the user's sudo password as the current master password.
 
**- ⚠️ take care that if you lose your sudo password without a recovery file, you will not be able to recover your credentials.**
* Provides an interactive repository selector when Git does not provide a repository path.
* Supports `fzf` as an alternative repository selector.
* Provides credential export functionality.
* Provides password-recovery functionality.

## Git integration

gthlpr follows Git's credential-helper protocol.

Git can send information such as:

```text
protocol=https
host=github.com
path=owner/repository.git
username=username
password=token
```

For `get`, gthlpr returns:

```text
username=username
password=token
```

For `store` and `erase`, Git does not require credential output.

The repository path is important because it allows credentials to be associated with individual repositories.

## Interactive selection

If Git does not provide a repository path, gthlpr can display the repositories stored in the database.

The selector supports:

* `↑` / `↓` — move through repositories
* `Enter` — select
* `z+Enter` — use `fzf`

The terminal UI is drawn directly on `/dev/tty` so Git's credential protocol output remains separate from the interactive interface.

## Commands

```text
gthlpr get
gthlpr store
gthlpr erase
gthlpr export
gthlpr passwd_rec
gthlpr setup
gthlpr -h
```

### `get`

Retrieve a credential for Git.

### `store`

Encrypt and store a Git credential.

### `erase`

Remove a stored credential.

### `export`

Export the credential database either as a direct copy or as decrypted plaintext.

### `passwd_rec`

Provides the password-recovery functionality.

### `setup`

Sets up the environment and required dependencies.

### `-h`

Display the help message.

## Terminal messages

gthlpr keeps its UI separate from Git's protocol output.

## Requirements

Current versions require:

* Bash
* `sudo`
* `gpg`
* `base64`

Optional:

* `fzf`
