# Repro for git-lfs rebase issue

git-lfs fails to checkout new lfs objects after rebasing commits in which lfs objects were added.


Before repro'ing, it may be helpful to observe that:
* the test branch has two commits not on the `master` branch:
    * one that starts tracking png files with lfs
    * one that actually adds a png file as an lfs object
* the master branch has one commit not on the `test` branch

## Repro steps:

1. checkout the `test` branch
2. observe that `oops.png` is properly checked out:
    * run `git lfs ls-files`, which indicates `*` full object
    * run `file oops.png`, the result is an image
3. rebase the `test` branch onto the `master` branch
4. observe that `oops.png` is not properly checked out:
    * run `git lfs ls-files`, which incidates `-` LFS pointer
    * run `file oops.png`, the result is an ASCII text file
