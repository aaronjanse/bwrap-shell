This is an [ion shell](https://gitlab.redox-os.org/redox-os/ion) fork that runs every command in a sandbox containing only the current working directory (along with stuff like /dev, but we'll ignore that for now). So, programs can only operate upon the current working directory.

Some interesting consequences:
- `rm --no-preserve-root -rf /` only removes the current directory (well, /proc too...)
- `ls ..` doesn't list the parent directory, since the non-builtin `ls` does not have access to the parent directory (because no external commands do)
- `cd` is a builtin, so it works as expected
- `git`, `htop`, etc all work as expected, for the most part

Note that this does not create _secure_ sandboxes, due to [bubblewrap CVE-2017-5226](https://github.com/containers/bubblewrap/issues/142). I also carelessly mount stuff like `/lib` and `/proc`.

Dependencies:
- bubblewrap must be installed as setuid and in the `$PATH`

Attribute the shell features that work well to the Redox OS contributors. Broken features are likely due to my modifications, which is okay because this repo is just a proof-of-concept. 
