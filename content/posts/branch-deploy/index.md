---
title: "Branch Deploy Model"
author: "Grant Birkinbine" # can be an array or just a string
description: "Learn how to use the branch deploy model to ship code safely and quickly to production."

# The summary is for search engines and the main page
summary: "Learn how to use the branch deploy model to ship code safely and quickly to production."

date: 2023-08-10T00:00:00-00:00 # date of creation

categories: ["engineering", "open source", "devops"] # high level categories
tags: ["GitHub Actions", "deployment", "automation"] # micro level categories

# aliases: ["markdown-example"] # redirect, alias, shorthand url

ShowToc: true # show table of contents
TocOpen: true # auto open table of contents
searchHidden: false # hide from search

# blog post cover image
cover:
  image: "cover.svg" # the image name MUST ALWAYS be cover.[extension]
  alt: "develop, deploy, merge"
#   caption: "example" # optional caption text
  relative: true

# lower weight = higher precedence - 0 is interpreted as an unset weight
weight: 0
draft: false
---

## Intro 💡

The most common way developers deploy their changes to production is the merge → deploy model. However, there is a significantly better way to ship our code to production. Rather than smash the merge button, cross our fingers, and hold onto our butts... we can hit merge with confidence that our change works exactly as we expect it to!

**Introducing… the branch deploy model!**

> If you have already heard of the branch deploy model and are familiar with it, you can skip ahead to get to the part where we implement it with GitHub Actions and IssueOps for a project

## Models 🏗️

In this section, we will discuss the two most common ways developers deploy their changes to production:

- The _merge → deploy_ model
- The branch deploy model

### Merge → Deploy Model

To really understand the branch deploy model, lets first take a look at a traditional merge → deploy model. It goes like this:

1. Create a branch
2. Add commits to your branch
3. Open a pull request
4. Gather feedback + peer reviews
5. Merge your branch
6. A deployment starts from the `main` / `master` branch

This model is known as the merge → deploy model because when we "merge" our branch, that is when the deployment starts. This model is quite common in less mature projects because it is simple to implement and easy to understand.

### Branch Deploy Model

Here are the steps for the branch deploy model:

1. Create a branch
2. Add commits to your branch
3. Open a pull request
4. Gather feedback + peer reviews
5. Deploy your change
6. Validate your change
7. Merge your branch

With the branch deploy model, we deploy our changes _before_ we merge our branch. This allows us to fully validate our changes before we merge them. By doing this, we can ensure that our `main` / `master` branch is highly stable and always deployable.

It should be noted that some projects actually do a second deployment during step "_7: Merge your branch_" to ensure that changes are still deployable after merging. This is entirely optional and depends on your project's needs.

### Visualizing the Models 🗺️

---

![Merge Deploy Model](merge-deploy-model.webp)

---

![Branch Deploy Model](branch-deploy-model.webp)

---

As you can see, the merge deploy model is inherently riskier because the `main` branch is never truly a stable branch. If a deployment fails, or we need to roll back, we follow the entire process again to roll back our changes. However, in the branch deploy model, the `main` branch is always in a "good" state and we can deploy it at any time to revert the deployment from a branch deploy. In the branch deploy model, we only merge our changes into `main` the branch once it has been successfully deployed and validated.

> This is sometimes referred to as the [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)

## Pros and Cons 👍👎

Here is a quick summary of the pros and cons of each model:

**Merge Deploy Model**:

| Pros | Cons |
| :---: | :---: |
| ✅ Simple to implement | ❌ Risky |
| ✅ Easy to understand | ❌ Hard to rollback |
|| ❌ Difficult to preview changes |
|| ❌ Scales poorly on larger teams |
|| ❌ Places high ops load on maintainers |

**Branch Deploy Model**:

| Pros | Cons |
| :---: | :---: |
| ✅ Highly stable default branch | ❌ More complex to implement |
| ✅ Easy and reliable rollbacks ||
| ✅ Enables change previews ||
| ✅ Highly scalable for large teams ||
| ✅ Low ops load on maintainers ||
| ✅ Greater flexibility in configuration ||
| ✅ Higher deployment confidence ||
| ✅ Lower incident resolution time ||
| ✅ Increased deployment volume ||

## Key Takeaways ⭐

Key takeaways of the **branch deploy** model:

- The `main` branch is always considered to be a **stable and deployable branch**
- All changes are deployed to production **before** they are merged to the `main` branch
- To rollback a branch deployment, you deploy the `main` branch

Branch deployments are a battle tested way of deploying your changes to a given environment before merging them into your default branch.

Branch deployments allow you to do the following:

- Deploy your changes to production **before** merging
- Alternatively deploy changes to a staging, QA, or non-production environment

## Implementing Branch Deployments 🛠️

By taking the concepts learned in this post, you can implement branch deployments in pretty much any way you want. You can build solutions from scratch or use existing projects / tools to help you along.

Here is a list of links that will help you implement branch deployments in your own projects and take your deployments to the stars:

- [github/branch-deploy](https://github.com/github/branch-deploy) - A single GitHub Action that you can integrate into **any** repository to enable branch deployments
- [Enabling branch deployments through IssueOps with GitHub Actions](https://github.blog/2023-02-02-enabling-branch-deployments-through-issueops-with-github-actions/) - A blog post I wrote at GitHub about using IssueOps + Branch Deployments to leverage branch deployments

## Conclusion 🏁

If you are looking to enhance your DevOps experience, have better reliability in your deployments, or ship changes faster, then branch deployments are for you!

Whether you are a solo developer, a startup, or a massive enterprise, branch deployments are a truly battle tested way to confidently ship your code to production.

---

## References 📚

- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [GitHub Blog Post](https://github.blog/2023-02-02-enabling-branch-deployments-through-issueops-with-github-actions/)
- [Deploying branches to GitHub.com](https://github.blog/2015-06-02-deploying-branches-to-github-com/)
- [Deploying at GitHub](https://github.blog/2012-08-29-deploying-at-github/)
- [Deployments from Branches](https://confluence.atlassian.com/bamboo/deployments-from-branches-407724097.html)
- [Medium](https://medium.com/better-programming/branch-deployments-with-issueops-and-github-actions-d9405311ad8b) - My original article on Medium
