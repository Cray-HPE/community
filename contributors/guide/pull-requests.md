This doc explains the process and best practices for submitting a pull request to the Shasta CSM project or any of the additional repositories in the Cray-HPE Github organization. You will note

It should serve as a reference for all contributors, and be useful especially to new and infrequent submitters.

- [Before You Submit a Pull Request](#before-you-submit-a-pull-request)
- [The Pull Request Submit Process](#the-pull-request-submit-process)
  - [Marking Unfinished Pull Requests](#marking-unfinished-pull-requests)
  - [Pull Requests and the Release Cycle](#pull-requests-and-the-release-cycle)
  - [Automation](#automation)
- [Why was my pull request closed?](#why-was-my-pull-request-closed)
- [Why is my pull request not getting reviewed?](#why-is-my-pull-request-not-getting-reviewed)
- [Best Practices for Faster Reviews](#best-practices-for-faster-reviews)
  - [Familiarize yourself with project conventions](#familiarize-yourself-with-project-conventions)
  - [Is the feature wanted? File an Enhancement Proposal](#is-the-feature-wanted-file-a-kubernetes-enhancement-proposal)
  - [Smaller Is Better: Small Commits, Small Pull Requests](#smaller-is-better-small-commits-small-pull-requests)
  - [Open a Different Pull Request for Fixes and Generic Features](#open-a-different-pull-request-for-fixes-and-generic-features)
  - [Comments Matter](#comments-matter)
  - [Test](#test)
  - [Squashing](#squashing)
  - [Commit Message Guidelines](#commit-message-guidelines)
  - [KISS, YAGNI, MVP, etc.](#kiss-yagni-mvp-etc)
  - [It's OK to Push Back](#its-ok-to-push-back)
  - [Common Sense and Courtesy](#common-sense-and-courtesy)
  - [Trivial Edits](#trivial-edits)
- [The Testing and Merge Workflow](#the-testing-and-merge-workflow)
  - [More About `Ok-To-Test`](#more-about-ok-to-test)


# Before You Submit a Pull Request

This guide is for contributors who already have a pull request to submit. 

First-time contributors should head to the [Contributor Guide](/contributors/guide/README.md) to get started.

**Make sure your pull request adheres to our best practices. 

These include following project conventions, making small pull requests, and commenting thoroughly. Please read the more detailed section on [Best Practices for Faster Reviews](#best-practices-for-faster-reviews) at the end of this doc.**

# The Pull Request Submit Process

Merging a pull request requires the following steps to be completed before the pull request will be merged automatically.

- [Open a pull request](https://help.github.com/articles/about-pull-requests/)
- Get all necessary approvals from reviewers and code owners

## Marking Unfinished Pull Requests

If you want to solicit reviews before the implementation of your pull request is complete, you should hold your pull request to ensure that Tide does not pick it up and attempt to merge it. 
There are two methods to achieve this:

1. You may add the `/hold` or `/hold cancel` comment commands
2. You may add or remove a `WIP` or `[WIP]` prefix to your pull request title

The GitHub robots will add and remove the `do-not-merge/hold` label as you use the comment commands and the `do-not-merge/work-in-progress` label as you edit your title. 
While either label is present, your pull request will not be considered for merging.

Merging a pull request requires the following steps to be completed before the pull request will be merged automatically.

- [Open a pull request](https://help.github.com/articles/about-pull-requests/)
- Get all necessary approvals from reviewers and code owners

## Pull Requests and the Release Cycle

If a pull request has been reviewed but held or not approved, it might be due to the current phase in the [Release Cycle](/contributors/devel/sig-release/release.md). 
Occasionally, a SIG may freeze their own code base when working towards a specific feature or goal that could impact other development. 
During this time, your pull request could remain unmerged while their release work is completed.

If you feel your pull request is in this state, contact the appropriate [SIG](https://git.k8s.io/community/sig-list.md) for clarification.

## Automation

Pull request processing is not currently automated during the initial roll out of the CSM Project, however automation related to pull requests will begin to phase in over the course of calendar 2021.

# Why was my pull request closed?

Pull requests older than 90 days will be closed. 
Exceptions can be made for pull requests that have active review comments, or that are awaiting other dependent pull requests. 
Closed pull requests are easy to recreate, and little work is lost by closing a pull request that subsequently needs to be reopened. 
We want to limit the total number of pull requests in flight to:
* Maintain a clean project
* Remove old pull requests that would be difficult to rebase as the underlying code has changed over time
* Encourage code velocity

# Why is my pull request not getting reviewed?

A few factors affect how long your pull request might wait for review.

If it's the last few weeks of a milestone, we need to reduce churn and stabilize.

Or, it could be related to best practices. 
One common issue is that the pull request is too big to review.  
When your would-be reviewers pull up the diffs, they run away - this pull request is going to take 4 hours to review and they don't have 4 hours right now. 
They'll get to it later, just as soon as they have more free time (ha!).

There is a detailed rundown of best practices, including how to avoid too-lengthy pull requests, in the next section.

But, if you've already followed the best practices and you still aren't getting any pull request love, here are some things you can do to move the process along:

   * Make sure that your pull request has an assigned reviewer (assignee in GitHub). If not, reach out to the Team Admin for your repo and request a review. 

   * Ping the assignee (@username) on the pull request comment stream, and ask for an estimate of when they can get to the review.

   * Ping the assignee on Slack. Remember that a person's GitHub username might not be the same as their Slack username. Note hat Cray-HPE OSS slack is not yet deployed, but will be soon..

   * Ping the assignee by email (many of us have publicly available email addresses).

   * If you have fixed all the issues from a review, and you haven't heard back, you should ping the assignee on the comment stream with a "please take another look" (`PTAL`) or similar comment indicating that you are ready for another review.

   * If you still don't hear back, email the Cray-HPE OSS coordinator for your project.

Read on to learn more about how to get faster reviews by following best practices.

# Best Practices for Faster Reviews

Most of this section is not specific to Kubernetes, but it's good to keep these best practices in mind when you're making a pull request.

You've just had a brilliant idea on how to make Kubernetes better. 
Let's call that idea Feature-X. 
Feature-X is not even that complicated.
You have a pretty good idea of how to implement it. 
You jump in and implement it, fixing a bunch of stuff along the way. 
You send your pull request - this is awesome! 
And it sits.
And sits.
A week goes by and nobody reviews it.
Finally, someone offers a few comments, which you fix up and wait for more review. And you wait.
Another week or two go by. This is horrible.

Let's talk about best practices so your pull request gets reviewed quickly.

## Familiarize yourself with project conventions

Formalized conventions will be developed over time and linked to here as the OSS footprint evolves. 


## Is the feature wanted? File an Enhancement Proposal

Are you sure Feature-X is something the project team wants or will accept? 
Is it implemented to fit with other changes in flight? 
Are you willing to bet a few days or weeks of work on it?

It's better to get confirmation beforehand.

When you want to make a large or otherwise significant change, you should follow the [Project Enhancement Proposal process](https://github.com/Cray-HPE/community/blob/main/contributors/design-proposals/README.md).

Even for small changes, it is often a good idea to gather feedback on an issue you filed, or even simply ask in the appropriate SIG's Slack channel to invite discussion and feedback from code owners. 
Here's a [list of SIGs](/sig-list.md), this includes their public meetings.

## KISS, YAGNI, MVP, etc.

Sometimes we need to remind each other of core tenets of software design - Keep It Simple, You Aren't Gonna Need It, Minimum Viable Product, and so on.
Adding a feature "because we might need it later" is antithetical to software that ships. 
Add the things you need NOW and (ideally) leave room for things you might need 
later - but don't implement them now.

## Smaller Is Better: Small Commits, Small Pull Requests

Small commits and small pull requests get reviewed faster and are more likely to be correct than big ones.

Attention is a scarce resource.
If your pull request takes 60 minutes to review, the reviewer's eye for detail is not as keen in the last 30 minutes as it was in the first.
It might not get reviewed at all if it requires a large continuous block of time from the reviewer.

**Breaking up commits**

Break up your pull request into multiple commits, at logical break points.

Making a series of discrete commits is a powerful way to express the evolution of an idea or the different ideas that make up a single feature. 
Strive to group logically distinct ideas into separate commits.

For example, if you found that Feature-X needed some prefactoring to fit in, make a commit that JUST does that prefactoring.
Then make a new commit for Feature-X.

Strike a balance with the number of commits. 
A pull request with 25 commits is still very cumbersome to review, so use your best judgment.

**Breaking up Pull Requests**

Or, going back to our prefactoring example, you could also fork a new branch, do the prefactoring there and send a pull request for that.
If you can extract whole ideas from your pull request and send those as pull requests of their own, you can avoid the painful problem of continually rebasing.

Kubernetes is a fast-moving codebase - lock in your changes ASAP with your small pull request, and make merges be someone else's problem.

Multiple small pull requests are often better than multiple commits.
Don't worry about flooding us with pull requests. We'd rather have 100 small,obvious pull requests than 10 unreviewable monoliths.

We want every pull request to be useful on its own, so use your best judgment on what should be a pull request vs. a commit.

As a rule of thumb, if your pull request is directly related to Feature-X and nothing else, it should probably be part of the Feature-X pull request. 
If you can explain why you are doing seemingly no-op work ("it makes the Feature-X change easier, I promise") we'll probably be OK with it.
If you can imagine someone finding value independently of Feature-X, try it as a pull request. 
(Do not link pull requests by `#` in a commit description, because GitHub creates lots of spam. 
Instead, reference other pull requests via the pull request your commit is in.)

## Open a Different Pull Request for Fixes and Generic Features

**Put changes that are unrelated to your feature into a different pull request.**

Often, as you are implementing Feature-X, you will find bad comments, poorly named functions, bad structure, weak type-safety, etc.

You absolutely should fix those things (or at least file issues, please) - but not in the same pull request as your feature. Otherwise, your diff will have way too many changes, and your reviewer won't see the forest for the trees.

**Look for opportunities to pull out generic features.**

For example, if you find yourself touching a lot of modules, think about the dependencies you are introducing between packages. 
Can some of what you're doing be made more generic and moved up and out of the Feature-X package? 
Do you need to use a function or type from an otherwise unrelated package?
If so, promote!
We have places for hosting more generic code.

Likewise, if Feature-X is similar in form to Feature-W which was checked in last month, and you're duplicating some tricky stuff from Feature-W, consider prefactoring the core logic out and using it in both Feature-W and
Feature-X.
(Do that in its own commit or pull request, please.)

## Comments Matter

In your code, if someone might not understand why you did something (or you won't remember why later), comment it. Many code-review comments are about this exact issue.

If you think there's something pretty obvious that we could follow up on, add a TODO.

Depending on the language in which you are developing, follow the language idiomatic/best practices for code comments. For example:

Read up on [GoDoc](https://blog.golang.org/godoc-documenting-go-code) - follow those general rules for comments.

## Test

Nothing is more frustrating than starting a review, only to find that the tests are inadequate or absent.
Very few pull requests can touch the code and NOT touch tests.

If you don't know how to test Feature-X, please ask!
We'll be happy to help you design things for easy testing or to suggest appropriate test cases.

## Squashing

Your reviewer has finally sent you feedback on Feature-X.

Make the fixups, and don't squash yet.
Put them in a new commit, and re-push.
That way your reviewer can look at the new commit on its own, which is much faster than starting over.

We might still ask you to clean up your commits at the very end for the sake of a more readable history, but don't do this until asked: typically at the point where the pull request would otherwise be tagged `LGTM`.

Each commit should have a good title line (<70 characters) and include an additional description paragraph describing in more detail the change intended.

For more information, see [squash commits](./github-workflow.md#squash-commits).

**General squashing guidelines:**

* Sausage => squash

 Do squash when there are several commits to fix bugs in the original commit(s), address reviewer feedback, etc. 
 Really we only want to see the end state and commit message for the whole pull request.

* Layers => don't squash

 Don't squash when there are independent changes layered to achieve a single goal.
 For instance, writing a code munger could be one commit, applying it could be another, and adding a precommit check could be a third.
 One could argue they should be separate pull requests, but there's really no way to test/review the munger without seeing it applied, and there needs to be a precommit check to ensure the munged output doesn't immediately get out of date.

## Commit Message Guidelines

PR comments are not represented in the commit history. 
Commits and their commit messages are the _"permanent record"_ of the changes being done in your PR and their commit messages should accurately describe both _what_ and _why_ it is being done.

Commit messages are comprised of two parts; the subject and the body.

The subject is the first line of the commit message and is often the only part
that is needed for small or trivial changes.
Those may be done as "one liners" with the `git commit -m` or the `--message` flag, but only if the what and especially why can be fully described in that few words. 

The commit message body is the portion of text below the subject when you run 
`git commit` without the `-m` flag which will open the commit message for editing
in your [preferred editor].
Typing a few further sentences of clarification is a useful investment in time both for your reviews and overall later project maintenance.

```
This is the commit message subject

Any text here is the commit message body
Some text
Some more text
...

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch example
# Changes to be committed:
#   ...
#
```

Use these guidelines below to help craft a well formatted commit message. 
These can be largely attributed to the previous work of [Chris Beams], [Tim Pope],
[Scott Chacon] and [Ben Straub].

- [Try to keep the subject line to 50 characters or less; do not exceed 72 characters](#try-to-keep-the-subject-line-to-50-characters-or-less-do-not-exceed-72-characters)
- [The first word in the commit message subject should be capitalized unless it starts with a lowercase symbol or other identifier](#the-first-word-in-the-commit-message-subject-should-be-capitalized-unless-it-starts-with-a-lowercase-symbol-or-other-identifier)
- [Do not end the commit message subject with a period](#do-not-end-the-commit-message-subject-with-a-period)
- [Use imperative mood in your commit message subject](#use-imperative-mood-in-your-commit-message-subject)
- [Add a single blank line before the commit message body](#add-a-single-blank-line-before-the-commit-message-body)
- [Wrap the commit message body at 72 characters](#wrap-the-commit-message-body-at-72-characters)
- [Do not use GitHub keywords or (@)mentions within your commit message](#do-not-use-github-keywords-or-mentions-within-your-commit-message)
- [Use the commit message body to explain the _what_ and _why_ of the commit](#use-the-commit-message-body-to-explain-the-what-and-why-of-the-commit)

<!-- omit in toc -->
### Try to keep the subject line to 50 characters or less; do not exceed 72 characters

The 50 character limit for the commit message subject line acts as a focus to
keep the message summary as concise as possible.
It should be just enough to describe what is being done.

The hard limit of 72 characters is to align with the max body size. 
When viewing the history of a repository with `git log`, git will pad the body text with additional blank spaces.
Wrapping the width at 72 characters ensures the body text will be centered and easily viewable on an 80-column terminal.

<!-- omit in toc -->
#### Providing additional context

You can provide additional context with fewer characters by prefixing your
commit message with the [kind] or [area] that your PR is impacting.
These are commonly used labels that other members of the Kubernetes community will
understand.

**Examples:**
- `cleanup: remove unused portion of script foo`
- `deprecation: add notice for bar feature removal in future release`
- `etcd: update default server to 3.4.7`
- `kube-proxy: add a test case for HostnameOverride`

These can serve as a good subject before expanding further on the what and why
within the commit message body.


<!-- omit in toc -->
### The first word in the commit message subject should be capitalized unless it starts with a lowercase symbol or other identifier

The commit message subject is like an abbreviated sentence.
The first word should be capitalized unless the message begins with symbol, acronym or other identifier such as [kind] or [area] that would regularly be lowercase.


<!-- omit in toc -->
### Do not end the commit message subject with a period

This is primary intended to serve as a space saving measure, but also aids in
driving the subject line to be as short and concise as possible.


<!-- omit in toc -->
### Use imperative mood in your commit message subject

Imperative mood can be be thought of as a _"giving a command"_; it is a
**present-tense** statement that explicitly describes what is being done.

**Good Examples:**
- Fix x error in y
- Add foo to bar
- Revert commit "baz"
- Update pull request guidelines

**Bad Examples**
- Fixed x error in y
- Added foo to bar
- Reverting bad commit "baz"
- Updating the pull request guidelines
- Fixing more things

A general guideline from [Chris Beams] on forming an imperative commit subject
is it should complete this sentence:
```
If applied, this commit will <your subject line here>
```

**Examples:**
- _If applied, this commit will_ **Fix x error in y**
- _If applied, this commit will_ **Add foo to bar**
- _If applied, this commit will_ **Revert commit "baz"**
- _If applied, this commit will_ **Update the pull request guidelines**


<!-- omit in toc -->
### Add a single blank line before the commit message body

Git uses the blank line to determine which portion of the commit message is the
subject and body.
Text preceding the blank line is the subject, and text following is considered the body.

<!-- omit in toc -->
### Wrap the commit message body at 72 characters

The default column width for git is 80 characters. 
Git will pad the text of the message body with an additional 4 spaces when viewing the git log.
This would leave you with 76 available spaces for text, however the text would be "lop-sided".
To center the text for better viewing, the other side is artificially padded
with the same amount of spaces, resulting in 72 usable characters per line. 
Think of them as the margins in a word doc.


<!-- omit in toc -->
### Do not use GitHub keywords or (@)mentions within your commit message

<!-- omit in toc -->
#### GitHub Keywords

Using [GitHub keywords] followed by a `#<issue number>` reference within your
commit message will automatically apply the `do-not-merge/invalid-commit-message`
label to your PR preventing it from being merged. 

[GitHub keywords] in a PR to close issues is considered a convenience item, but
can have unexpected side-effects; often closing something they shouldn't. 

**Blocked Keywords:**
- close
- closes
- closed
- fix
- fixes
- fixed
- resolve
- resolves
- resolved


<!-- omit in toc -->
#### (@)Mentions

(@)mentions within the commit message will send a notification to that user, and
will continually do so each time the PR is updated.


<!-- omit in toc -->
### Use the commit message body to explain the _what_ and _why_ of the commit

Commits and their commit messages are the _"permanent record"_ of the changes
being done in your PR. 
Describing why something has changed and what effects it may have.
You are providing context to both your reviewer and the next person that has to touch your code.

If something is resolving a bug, or is in response to a specific issue, you can
link to it as a reference with the message body itself. 
These sorts of breadcrumbs become essential when tracking down future bugs or regressions and further help explain the _"why"_ the commit was made.


**Additional Resources:**
- [How to Write a Git Commit Message - Chris Beams](https://chris.beams.io/posts/git-commit/)
- [Distributed Git - Contributing to a Project (Commit Guidelines)](https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project)
- [What’s with the 50/72 rule? - Preslav Rachev](https://preslav.me/2015/02/21/what-s-with-the-50-72-rule/)
- [A Note About Git Commit Messages - Tim Pope](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)

## It's OK to Push Back

Sometimes reviewers make mistakes.
It's OK to push back on changes your reviewer requested.
If you have a good reason for doing something a certain way, you are absolutely allowed to debate the merits of a requested change. 
Both the reviewer and reviewee should strive to discuss these issues in a polite and respectful manner.

You might be overruled, but you might also prevail. 
We're pretty reasonable people.

Another phenomenon of open-source projects (where anyone can comment on any issue)
is the dog-pile - your pull request gets so many comments from so many people it
becomes hard to follow.
In this situation, you can ask the primary reviewer (assignee) whether they want you to fork a new pull request to clear out all the comments.
You don't HAVE to fix every issue raised by every person who feels like commenting, but you should answer reasonable comments with an explanation.

## Common Sense and Courtesy

No document can take the place of common sense and good taste. 
Use your best judgment, while you put a bit of thought into how your work can be made easier to review. 
If you do these things your pull requests will get merged with less friction.

## Trivial Edits

Each incoming Pull Request needs to be reviewed, checked, and then merged.

While automation helps with this, each contribution also has an engineering cost.
Therefore it is appreciated if you do NOT make trivial edits and fixes, but
instead focus on giving the entire file a review.

If you find one grammatical or spelling error, it is likely there are more in
that file, you can really make your Pull Request count by checking the formatting,
checking for broken links, and fixing errors and then submitting all the fixes
at once to that file.

**Some questions to consider:**

* Can the file be improved further?
* Does the trivial edit greatly improve the quality of the content?

# The Testing and Merge Workflow

The Kubernetes merge workflow uses labels, applied by [commands](https://prow.k8s.io/command-help) via comments. 
These will trigger actions on your pull request. 
Different Kubernetes repositories may require different labels on the path to approval. 
A generic explanation of how labels are used in pull requests can be found [here](/contributors/guide/owners.md#code-review-using-owners-files). 
The pull request bot will also automatically apply and/or suggest labels.

_Example:_ To apply a SIG label, you would type in a comment:
```
/sig apps
```

*NOTE: For pull requests that are in progress but not ready for review,
prefix the pull request title with `WIP` or `[WIP]` and track any remaining TODOs
in a checklist in the pull request description.*

Here's the process the pull request goes through on its way from submission to merging:


[GitHub keywords]: https://help.github.com/articles/closing-issues-using-keywords