---
title: "Audacity - Raising issues in Open Source project"
datePublished: Tue Dec 26 2023 18:30:12 GMT+0000 (Coordinated Universal Time)
cuid: clqmompdm000008l7538e92wy
slug: audacity-raising-issues-in-open-source-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693318398345/d4017761-4aff-4439-bc3d-0d116010e4bc.png
tags: opensource, open-source-community, open-source-beginners-guide, audacity

---

This article is useful for the open source beginners. Here I wrote about how I found some bugs/issues in the famous open-source software.

**About project**

Audacity is a famous Audio editing software available in cross-platform OSs. It is an Open source software where we can record, and edit files.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693226967555/c3f8793b-0ab1-4dde-b337-f394f739e7cb.png align="center")

How did I encounter multiple issues as a first-time user/contributor

**The first bug/issue: \[cosmetic issue\]**

Since I was enthusiastic about multimedia projects, I wanted to explore the Audacity code base to experience the software after locally building it in the development system. As per the build instructions, arranged the necessary packages needed for the application to build and stated the source compilations. After launching the program in debug mode and found that the welcome dialog had a small cosmetic issue. Text was not visible near the check box. After confirming the bug, reported it to the project GitHub ticket. [https://github.com/audacity/audacity/issues/5050](https://github.com/audacity/audacity/issues/5050)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693227025941/ddc7cad7-83d0-4a0e-8bd9-562b5a5f269a.png align="center")

Expected behavior

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693227208708/07653275-e47c-45f7-88d6-3707c81456b6.png align="center")

**Second bug/issue: \[behaviour issue\]**

I checked the basic functionality of the software and tried the save the recording of the mic in the file and found some glimpses in the TextBox of the filename and unable to view the audio file nametext. After confirming the behaviour and creating the issues in the project GitHub. A screen record has been attached to this ticket. [https://github.com/audacity/audacity/issues/5061](https://github.com/audacity/audacity/issues/5061)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693227133278/4dc7937d-59d5-44f2-8fad-c4f83a0f7f04.png align="center")

**Third bug/issue: \[source code quality\]**

My habit is always reading more from the closed issues. Will look for the ways of code is implemented and how the conversations went between the maintainer and developer. Thus, I looked into the codebase and found the boilerplate header comments are missing in the source code files. Also, read about the project coding standards and it was mentioned that the header comments are mandatory and it is part of the [Coding standard](https://audacity.gitbook.io/dev/getting-started/coding-standards#header_comments). Thus finally re-read the coding standard confirmed the issue and raised a ticket in GitHub. [https://github.com/audacity/audacity/issues/5077](https://github.com/audacity/audacity/issues/5077)

Key lessons:

* Any unexpected behaviour needs to be verified before confirming it as an issue.
    
* You are allowed to post an issue and it is reviewed by the maintainer. This is one of the coolest things in the open-source communities.
    
* You are starting to improve the quality of the open-source product. Small effort makes a good difference.
    

Disclaimer: I'm not promoting any products, Just writing about my experience in the open-source contribution journey.