---
project: cacheable
stars: 1660
description: a robust, scalable, and maintained set of caching packages
url: https://github.com/jaredwray/cacheable
---

> Caching for Nodejs based on Keyv

With over `1bn downloads` a year the goal with the `Cacheable Project` is to provide a robust, scalable, and maintained set of caching packages that can be used in various projects. The packages in this repository are:

Package

Downloads

Description

cacheable

Next generation caching framework built from the ground up with layer 1 / layer 2 caching.

cache-manager

Cache Manager that is used in services such as NestJS and others with robust features such as `wrap` and more.

cacheable-request

Wrap native HTTP requests with RFC compliant cache support

flat-cache

Fast In-Memory Caching with file store persistence

file-entry-cache

A lightweight cache for file metadata, ideal for processes that work on a specific set of files and only need to reprocess files that have changed since the last run

@cacheable/node-cache

Maintained built in replacement of `node-cache`

The website documentation for https://cacheable.org is included in this repository here.

How to Use the Cacheable Mono Repo
==================================

-   CODE\_OF\_CONDUCT - Our code of conduct
-   CONTRIBUTING - How to contribute to this project
-   SECURITY - Security guidelines and supported versions

Open a Pull Request
-------------------

You can contribute changes to this repo by opening a pull request:

1.  After forking this repository to your Git account, make the proposed changes on your forked branch.
2.  You will need `docker` installed and running on your machine. Once it is installed run `pnpm test:services:start` to start the services needed for testing.
3.  Run tests and linting locally.
    -   Run `pnpm i && pnpm test`.
4.  Commit your changes and push them to your forked repository.
5.  Navigate to the main `cacheable` repository and select the _Pull Requests_ tab.
6.  Click the _New pull request_ button, then select the option "Compare across forks"
7.  Leave the base branch set to main. Set the compare branch to your forked branch, and open the pull request.
8.  Once your pull request is created, ensure that all checks have passed and that your branch has no conflicts with the base branch. If there are any issues, resolve these changes in your local repository, and then commit and push them to git.
9.  Similarly, respond to any reviewer comments or requests for changes by making edits to your local repository and pushing them to Git.
10.  Once the pull request has been reviewed, those with write access to the branch will be able to merge your changes into the `cacheable` repository.

If you need more information on the steps to create a pull request, you can find a detailed walkthrough in the GitHub documentation

Post an Issue
-------------

To post an issue, navigate to the "Issues" tab in the main repository, and then select "New Issue." Enter a clear title describing the issue, as well as a description containing additional relevant information. Also select the label that best describes your issue type. For a bug report, for example, create an issue with the label "bug." In the description field, Be sure to include replication steps, as well as any relevant error messages.

If you're reporting a security violation, be sure to check out the project's security policy.

Please also refer to our Code of Conduct for more information on how to report issues.

Ask a Question
--------------

To ask a question, create an issue with the label "question." In the issue description, include the related code and any context that can help us answer your question.

License
-------

MIT © Jared Wray
