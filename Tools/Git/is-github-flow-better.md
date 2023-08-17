# Is Github flow better than Git flow?

Table of Content

- Git flow or Github flow?
- Let's do it: Github flow
- What if we require versioned releases?
- Furthermore

## Git flow or Github flow?

The world of Git offers several collaboration strategies, including Github Flow, Git Flow, Gitlab Flow, and others. In this post, I'd like to share my thoughts on Github Flow specifically.

My team and I opted for Git Flow at the outset of our project, after a thorough discussion on which flow to adopt. We were all new to Git at the time, so we relied on [a post](https://techblog.woowahan.com/2553/) for guidance and diligently followed its advice.

## Let's do it: GitHub flow

As I continued to use Git Flow, I became aware of its limitations, particularly its complexity with the use of multiple branches - Master, Develop, Feature, Hotfix, and Release. However, this complexity can be mitigated through the use of Github Flow, which only requires two branches: Master and etc. As [Scott Chacon](https://scottchacon.com/2011/08/31/github-flow.html) stated, 

> Anything in the master branch is deployable.

Github Flow, first introduced by [Vincent Driessen](https://nvie.com/posts/a-successful-git-branching-model/), is a more suitable option for teams practicing [continuous delivery](https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment), as it provides a simpler workflow compared to Git Flow. 

> If your team is doing continuous delivery of software, I would suggest to adopt a much simpler workflow (like GitHub flow)

## What if we require versioned releases?

As previously mentioned, anything in the Master branch is deployable, but there are times when we need to maintain starting points for significant updates. This is where the [Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging) feature in Git comes in handy. By utilizing the git tag command, we can easily create versioned releases, such as

> $ git tag
v1.0
v2.0

## Furthermore

- [GitHub flow](https://scottchacon.com/2011/08/31/github-flow.html)
- [Get started GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [Git flow, GitHub flow, GitLab flow](https://ujuc.github.io/2015/12/16/git-flow-github-flow-gitlab-flow/)
