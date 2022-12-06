# Git --no-ff demo

The purpose of this repository is to demonstrate the git's `--no-ff` feature,
and prove that it does not break the `git bisect` feature since git's version
2.29 thanks to `--first-parent` flag.

Feel free to experiment with this initial setup, so that you can get all the
pros and cons of the non-linear git history.

I can also strongly recommend [this](https://gist.github.com/canton7/3737126)
`gist` as it makes some really good points.

## git log

The repository consist of the following commits:

![git log --all --decorate --oneline --graph](git_log.png "git log --all --decorate --oneline --graph")

As you can see there are feature branches being merged to the `trunk`, including
the branches that diverted long time ago as e.g. `big_effort` and `middle`
branches.

If you want to see a flat history of the `trunk` branch you can use git log's
`--first-parent` feature as presented below:

```bash
~/Projects/no-ff$ (trunk) git log --decorate --oneline --graph --first-parent
* 9c23ba1 (HEAD -> trunk) Merge branch 'middle' into trunk
* 94ecbfc Merge branch 'big_effort'
* 56deb9c Merge branch 'lorem'
* 39dca96 Merge branch 'foobar'
* 9dddd43 Merge branch 'bar'
* 1d74cae Merge branch 'foo'
* 02b68fc A
```

## git bisect

If you want the git bisect to iterate only on the merge commits, you can now do
`git bisect start --first-parent` as shown below:

![git bisect start --first-parent 9c23ba1 02b68fc](git_bisect.png "git bisect start --first-parent 9c23ba1 02b68fc")
