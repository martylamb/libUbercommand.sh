# libUbercommand.sh

> :warning: **This project is now retired.  I recommend you use the amazing [just](https://github.com/casey/just) tool instead.**
>
> For more details about project retirement, please see [RETIREMENT.md](RETIREMENT.md).

---

> :warning: On 2023/11/08, I cleaned up some incorrect contact information (user.name and user.email) in the commit history via [git-filter-repo](https://github.com/newren/git-filter-repo).
>
> If you have a clone that predates this change, you will need to run `git pull --rebase` to get the new history and allow git to work properly.  Clones made after this date don't need to do anything.

---

A bash tool similar to Slack's [magic-cli](https://github.com/slackhq/magic-cli) : A foundation for building your own suite of command line tools.

libUbercommand.sh exists to make it easy to create a set of tools that work together. It's not a tool you use as-is; it's here to offer a starting point for your own custom command line tools.

**The idea is to unify related tools under a single "ubercommand" in much the same way as `git`, making related tools easily discoverable.**

Building your ubercommand is trivial:

  1. Copy `libUbercommand.sh` to a well-known location on your system (e.g. `/usr/local/lib`)
  2. Create your ubercommand script wherever you want it to be.  In the script, set the environment variable UBERCOMMAND_DESC to a description of your command, and then source the library file (e.g. `. /usr/local/lib/libUbercommand.sh`)
  2. Create "subcommands" using the scripting language of your choice in the same directory as your ubercommand named using the pattern "UBERCOMMAND-SUBCOMMAND" (for example, if your ubercommand is `mycmd` and you have a subcommand `dostuff`,  then that subcommand should be named `mycmd-dostuff`
  3. Add summary text to your subcommand.  This is done by adding a line anywhere in your subcommand script that contains the text `# Summary: ` followed by summary text.  If your subcommand is a binary, you should implement a wrapper script to invoke it so that it can provide summary text.
  4. Implement a `--help` option in your subcommand that provides more detailed help than just usage information.

That's it.  Now you can:
  * get a list of your subcommands by just typing the name of your ubercommand (e.g. `mycmd`)
  * get help for any of your subcommands via `help` (e.g. `mycmd help dostuff`)
  * invoke your subcommands (e.g. `mycmd dostuff arg1 arg2 ...`)
