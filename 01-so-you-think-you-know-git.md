# So You Think You Know Git

Dump of all commands from "So You Think You Know Git - FOSDEM 2024":

- https://www.youtube.com/watch?v=aolI_Rz0ZqY

The full blog post: https://blog.gitbutler.com/git-tips-and-tricks/

## Some Helpful Config Stuff

### Some aliases

```sh
# All ignored and untracked files are also stashed and then cleaned up with `git clean`.
git config --global alias.staash 'stash --all'
```

```sh
# Download the script here: https://gist.github.com/schacon/e9e743dee2e92db9a464619b99e94eff

# To run an arbitrary shell script
git config --global alias.bb !better-git-branch.sh
```

### Conditional Configs

```yaml
[includeIf "gitdir:~/projects/work/"]
  path = ~/projects/work/.gitconfig

[includeIf "gitdir:~/projects/oss/"]
  path = ~/projects/oss/.gitconfig
```

## Oldies But Goodies

### Git blame a "L"ittle

```sh
# Blame a line range
git blame -L 15,26 path/to/file
```

...equivalent for `git log`:

```sh
# Inspect line range over time
git log -L 15,26:path/to/file
```

```sh
# Inspect a symbol called "Foo" (e.g. a class) over time
git log -L :Foo:path/to/file
```

```sh
# Ignore whitespace
git blame -w
```

```sh
# Ignore whitespace,
# and detect lines moved or copied in the same commit
git blame -w -C
```

```sh
# Ignore whitespace,
# and detect lines moved or copied in the same commit,
# or the commit that created the file
git blame -w -C -C
```

```sh
# Ignore whitespace,
# and detect lines moved or copied in the same commit,
# or the commit that created the file,
# or any commit at all
git blame -w -C -C -C
```

### The "pickaxe"

```sh
# Find all the commits where `<some-text>` appears in the diff
git log -S <some-text> -p
```

You can reverse it as well, to get the oldest commit first:
```sh
git log -S <some-text> -p --source --all --reverse
```

### Other

```sh
# Shows when the tips of branches and other references were updated in the local repository
git reflog
```

```sh
# When you want to look at diffs inside a line
git diff --word-diff
```

```sh
# (RE)use (RE)corded (RE)solution
# Remember how you solved conflicts, to reapply them later automatically
git config --global rerere.enabled true
```

## Some New Stuff (You May Not Have Noticed)

```sh
git branch --column
```

or enable it globally:
```sh
git config --global column.ui auto
```

```sh
# Sort branches by most recent commit first 
git config --global branch.sort -committerdate
```

```sh
# Safer force push
git push --force-with-lease
```

```sh
# Signing commits with SSH
git config gpg.format ssh
git config user.signingkey ~/.ssh/key.pub
```

```sh
# Not supported by GitHub or GitLab
git push --signed
```

```sh
# Building commit graph, prefetching, removing loose objects and incremental repack automatically
git maintenance start
```

## Big Repo Stuff

### Commit graph

```sh
# Faster `git log --graph --oneline`
git commit-graph write
```

```sh
# Write commit graph on fetch
git config --global fetch.writeCommitGraph true
```

### Filsystem monitor

```sh
# Filesystem monitor for faster `git status`
git config core.untrackedcache true
git config core.fsmonitor true
```

### Partial clone

```sh
# Do not clone blobs, and only do it on-demand
git clone --filter=blob:none
```

```sh
# Good for CI
git clone --filter=tree:0
```

### Sparse checkout

```sh
# Only checkout `build` and `base` folders
git sparse-checkout set build base
```

## Some New GitHub Stuff

```sh
# Fetch all PRs automatically on `git fetch`
git config remote.origin.fetch '+refs/pull/*:refs/remotes/origin/pull/*'
```
