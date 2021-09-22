---
layout: post
title: "Semantic Versioning"
date: 2019-07-05 19:33:00
author: Shehab
categories: Computer-Science
tags: Algorithms
cover: "/assets/posts/tries.png"
---

You and your team are maintaing a set of backend services for an online shopping application. Scenario A, your colleague is pushing a bug fix to <strong>Order Service</strong> that caused some problems in the <strong>Cart Service</strong>. This new push has changed the state of the service from the old buggy state to the new fixed state. But say there is another team who want to quickly identify the magnitude of your change, i.e. did you break any logic? did you remove a class, or did you change a function signature that was used in other services?, or did you just update a README file?

Another Scenario, Scenario B, you are importing a 3rd party service such as <strong>Payment Service</strong> with a version 3.2.0, you notice two new releases with versions; 3.2.1 and 4.0.0. What is the difference? What is the magnitude of change in the 3rd party service? Should you be worried when upgrading to this new version or not?

<p align="center"><img src="/assets/posts/service-versions.png"></p>

Given scenario A and B, the question we have here is, how can you assign a label of a certain service to keep track of its changes and its current state? That's where Semantic Version comes in.

<h4>What is Semantic Versioning?</h4>

It is a solution to a problem known in software management called "Dependency Hell" -- The bigger the system, the more packages needed to integrate in the ssytem. It is a set of rules to define how software should be versioned and how it should incremened based on the code changes.

<p align="center">MAJOR.MINOR.PATCH</p>

1. MAJOR version - when you make incompatible API changes.
2. MINOR version - when you add functionality in a backward-compatible manner.
3. PATCH version - when you make backward-compatible bug fixes.

<i>Documentation in (https://semver.org/)</i>

In this post I will show you to use a fully automated semantic versioning tool called (semantic-release) in a GitLab pipeline.

<i>Documentation in (https://semantic-release.gitbook.io/semantic-release/)</i>
<i>GitHub in (https://github.com/semantic-release/semantic-release)</i>

<h4>How to setup Release Stage in your GitLab pipeline</h4>

<ol>
    <li>Generate an access token and set it as an environment variable to you selected repository either (GL_TOKEN or GITLAB_TOKEN).</li>
    <li>Create .releaserc file in either format (JSON / YAML / YML) and include the plugin(s) needed based on your preferences.</li>
</ol>

Here is a sample .releaserc.json file you can start with:

{% highlight json %}
{
"branches": ["main"],
"prepare": false,
"plugins": [
["@semantic-release/commit-analyzer",
{ "releaseRules": [
{"type": "style", "release": "patch"},
{"type": "breaking", "release": "major"} ],
}],
"@semantic-release/release-notes-generator",
"@semantic-release/gitlab"
]
}
{% endhighlight %}

Notice in the sample file above, the commit-analyzer plugin has two custom releaseRules which checks for a new rlease on the main branch based on a message convention: <strong>type(scope): message</strong>

For example, the following commit message "style: repositioned the navbar" will trigger a <strong>PATCH<strong> release while the following commit message "breaking: deprecated the promocode API" will trigger a <strong>MAJOR</strong> release. If no rules match, it will search for the default releaseRules which you can find in semantic-release GitHub repo.

Create a .gitlab-ci.yml file and add the following stage:

{% hightlight yml %}
stages:

- Release

semantic-release:

stage: Release

variables:
GITLAB_TOKEN: ${GITLAB_TOKEN}
GIT_AUTHOR_NAME: ${GITLAB_USER_NAME}
GIT_AUTHOR_EMAIL: ${GITLAB_USER_EMAIL}
GIT_COMMITTER_NAME: ${GITLAB_USER_NAME}
GIT_COMMITTER_EMAIL: ${GITLAB_USER_EMAIL}

before_script:

- export PATH=$PATH:/usr/local/bin/npm
- npm install --loglevel=error --save-dev semantic-release @semantic-release/gitlab-config

script:

- npx semantic-release -e @semantic-release/gitlab-config

only:

- main

{% endhighlight %}
