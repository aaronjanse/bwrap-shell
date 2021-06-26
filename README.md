Inspiration: [Dot Dot Considered Harmful - Fuchsia](https://fuchsia.dev/fuchsia-src/concepts/filesystems/dotdot).

This is an [ion shell](https://gitlab.redox-os.org/redox-os/ion) fork that runs every command in a sandbox containing only the current working directory (along with stuff like /dev, but we'll ignore that for now), along with file paths passed as arguments. So, programs can only operate upon the current working directory.

Note that `git`, `htop`, etc all work as expected, for the most part, which is pretty cool.

Note that this does not create _secure_ sandboxes, due to [bubblewrap CVE-2017-5226](https://github.com/containers/bubblewrap/issues/142). I also carelessly mount stuff like `/lib` and `/proc`.

Dependencies:
- bubblewrap must be installed as setuid and in the `$PATH`

Attribute the shell features that work well to the Redox OS contributors. Broken features are likely due to my modifications, which is okay because this repo is just a proof-of-concept. 
