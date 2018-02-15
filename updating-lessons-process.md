## Lab Revisions

### Fixing an Issue

1. Ensure that you have an issue in the Github Issues for the [Lesson][]
1. Decide the magnitude of the work required:
  * Big Issues: Multiple weeks work, cross team collaboration, etc.
  * Local Issues: Text is confusing, etc.

### General Workflow

1. Create a new branch (not a fork!) **prefix it with `wip-`** ([why][wip])
   * [Prefix with][wip] `wip-` &mdash; yes, we just wrote that, but seriously, do it
   * Remainder should be a reasonable `dash-cased-title` derived from the issue
     name/summary
2. Fix the issue in your new [wip-branch][wip]. Try and keep any conversation
   around the issue in the issue so everyone can see it. Try to avoid emailing
   people outside of the GitHub environment.
3. The final commit that fixes the issue should make sure to mention the issue
   number in the commit message so it shows up in that issue. So a commit
   message of "fixed issue #4". The `#` is important, it signifies to GitHub to
   include that on the issue page.

### Addressing "Big Issues"

1. Move that issue to Doing in Trello and make yourself the member on that card
2. Move it to a list entitled "Assigned to `${YOUR_NAME_HERE}`" (create if
   not present)
3. Follow the same process for "[Local Issues](#local-issues)"
4. Move Trello card to "Pending Review"
5. Upon merge, move card to "Completed"

<a name="local-issues"></a>

### Addressing "Local Issues"

1. Create a pull request against the appropriate branch.
  * Changes to README or Starter Code
    * Make the change in the single branch. Submit one pull request.
    * Check your destination branch! You should be merging _into_ a branch in
      the `learn-co-curriculum` org.
  * Changes to Tests
    * Make the test changes in a new tests branch, make the appropriate changes in a new solution branch.
    * Submit two pull requests
  * Changes to Solution/Tutorial
    * Make the changes in a single branch.
    * Submit pull request *to the solution branch*
2. Add a GitHub comment mentioning a reviewer in your PR

### Acting as a Reviewer

1. Review the PR, read changes, give line notes, etc. using the GitHub review
   feature
2. When you have Reviewed the PR, Approve it
3. The process for carrying the issue forward will now fall back to the author

### Merging PRs

1. Awesome work, you have a blessed mergeable PR!
3. Check the destination branch
4. Hit the green "Merge" button.
5. If the change updated a README, `.learn` or starter code change, make sure
   you merge master into solution after hitting the green button
6. Close the associated issue
7. Delete the working branches. There should only be two branches left over,
   `master` and `solution`.

### Git History and `master` and `solution`

Let's take a moment to imagine an ideal learning experience._Ideally_ we have
work for the Lesson inside of the `master` branch. _Ideally_ a curriculum
developer would then branch `master` to `solution` and then work in a TDD
manner to meet the tests and have a beautifully green test suite and post
it as a branch.

So this is a great process for the _initial_ population of the lesson. But
let's consider that at some point later, we discover a typo in the `README.md`
file. Being customer-focused clever people, we make the change and merge it
into `master`. But now `solution` is out of sync.

Or imagine the addition of a test to expose "weaker" implementations. That gets
written in `solution` (so that the suite can be verified as green) but now it
needs to appear in both `solution` **and** `master`.

Ay-yay-yay.

There really isn't a hard and fast **rule** here. You need to reason through
what students need to see carefully. If in doubt, ask for help.

Here's the approach @sgharms and @curiositypaths are using at the moment.

#### Update To README Or a Test Or Changing A Solution Implementation

The general approach should be this:

1. Make a feature branch against `master`
2. Merge the fix into `master` with the power of a Pull Request
3. `git fetch origin` to update your SHAs
4. `git checkout -b wip-new-solution solution`
5. `git rebase master`
6. Run `learn`, make sure things are kosher
7. `git push origin wip-new-solution`
8. Merge the `wip-new-solution` into `solution` with the power of a Pull
   Request.
9. Back in your git repo make sure to git pull `master` and `solution` so that
   you're in sync.
10. _fin_: clean up `wip-` branches, pull origin/solution to local solution,
    etc.

The exact process may vary with your familiarity with `git`, but the essential
quality is that `solution` should be a descendant from `master`. The extra
overhead here ensures that the documentation stays synchornized and truthful to
the code.

### Things to Keep in Mind

* You shouldn't be force pushing updates to the Curriculum remote on GitHub
* If you have to rebase or squash commits, make sure that you are squashing or
  rebasing commits you've made **LOCALLY**; do not modify commits that have
  already been pushed up to the Curriculum remote
* If you end up force pushing commits that modify commits which previously
  existed on the Curriculum remote, this can potentially create nightmarish
  merge conflicts that we'd have to resolve manually.
* **SUMMARY**: Just like open source software work: you can modify your own
  history on your local branch until you have a pristine history that takes all
  the back-and-forth out. In fact, that's ideal. But don't try to rewrite
  published history.

[Lesson]: https://GitHub.com/learn-co-curriculum/curriculum-team/blob/master/glossary.md#lesson
[wip]: ./why-we-work-in-wip.md
