<!-- 
.. link: 
.. description: 
.. tags: git, release
.. date: 2011/10/01 10:34:00
.. title: Git 1.7.7 publiée
.. slug: git-1.7.7-publiee
-->

Reprenons la bonne habitude d'annoncer les nouvelles versions. Rien de bien
méchant dans cette 1.7.7, il faut attendre la 1.8 je pense pour des plus gros
changements.

Le changelog
------------

 * The scripting part of the codebase is getting prepared for i18n/l10n.

 * Interix, Cygwin and Minix ports got updated.

 * Various updates to git-p4 (in contrib/), fast-import, and git-svn.

 * Gitweb learned to read from /etc/gitweb-common.conf when it exists,
  before reading from gitweb_config.perl or from /etc/gitweb.conf
  (this last one is read only when per-repository gitweb_config.perl
  does not exist).

 * Various codepaths that invoked zlib deflate/inflate assumed that these
  functions can compress or uncompress more than 4GB data in one call on
  platforms with 64-bit long, which has been corrected.

 * Git now recognizes loose objects written by other implementations that
  use a non-standard window size for zlib deflation (e.g. Agit running on
  Android with 4kb window). We used to reject anything that was not
  deflated with 32kb window.

 * Interaction between the use of pager and coloring of the output has
  been improved, especially when a command that is not built-in was
  involved.

 * "git am" learned to pass the "--exclude=<path>" option through to underlying
  "git apply".

 * You can now feed many empty lines before feeding an mbox file to
  "git am".

 * "git archive" can be told to pass the output to gzip compression and
  produce "archive.tar.gz".

 * "git bisect" can be used in a bare repository (provided that the test
  you perform per each iteration does not need a working tree, of
  course).

 * The length of abbreviated object names in "git branch -v" output
  now honors the core.abbrev configuration variable.

 * "git check-attr" can take relative paths from the command line.

 * "git check-attr" learned an "--all" option to list the attributes for a
  given path.

 * "git checkout" (both the code to update the files upon checking out a
  different branch and the code to checkout a specific set of files) learned
  to stream the data from object store when possible, without having to
  read the entire contents of a file into memory first. An earlier round
  of this code that is not in any released version had a large leak but
  now it has been plugged.

 * "git clone" can now take a "--config key=value" option to set the
  repository configuration options that affect the initial checkout.

 * "git commit <paths>..." now lets you feed relative pathspecs that
  refer to outside your current subdirectory.

 * "git diff --stat" learned a --stat-count option to limit the output of
  a diffstat report.

 * "git diff" learned a "--histogram" option to use a different diff
  generation machinery stolen from jgit, which might give better
  performance.

 * "git diff" had a weird worst case behaviour that can be triggered
  when comparing files with potentially many places that could match.

 * "git fetch", "git push" and friends no longer show connection
  errors for addresses that couldn't be connected to when at least one
  address succeeds (this is arguably a regression but a deliberate
  one).

 * "git grep" learned "--break" and "--heading" options, to let users mimic
  the output format of "ack".

 * "git grep" learned a "-W" option that shows wider context using the same
  logic used by "git diff" to determine the hunk header.

 * Invoking the low-level "git http-fetch" without "-a" option (which
  git itself never did---normal users should not have to worry about
  this) is now deprecated.

 * The "--decorate" option to "git log" and its family learned to
  highlight grafted and replaced commits.

 * "git rebase master topci" no longer spews usage hints after giving
  the "fatal: no such branch: topci" error message.

 * The recursive merge strategy implementation got a fairly large
  fix for many corner cases that may rarely happen in real world
  projects (it has been verified that none of the 16000+ merges in
  the Linux kernel history back to v2.6.12 is affected with the
  corner case bugs this update fixes).

 * "git stash" learned an "--include-untracked option".

 * "git submodule update" used to stop at the first error updating a
  submodule; it now goes on to update other submodules that can be
  updated, and reports the ones with errors at the end.

 * "git push" can be told with the "--recurse-submodules=check" option to
  refuse pushing of the supermodule, if any of its submodules'
  commits hasn't been pushed out to their remotes.

 * "git upload-pack" and "git receive-pack" learned to pretend that only a
  subset of the refs exist in a repository. This may help a site to
  put many tiny repositories into one repository (this would not be
  useful for larger repositories as repacking would be problematic).

 * "git verify-pack" has been rewritten to use the "index-pack" machinery
  that is more efficient in reading objects in packfiles.

 * test scripts for gitweb tried to run even when CGI-related perl modules
  are not installed; they now exit early when the latter are unavailable.
