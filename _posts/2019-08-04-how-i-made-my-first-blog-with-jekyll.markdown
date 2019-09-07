---
layout: post
title:  "How I made my first blog with Jekyll and why"
date:   2019-08-04 14:55:55 -0300
categories: jekyll
---
## Motivation

After wanting to make a blog and discuss it with my brother. I've got the conclusion that is necessary to have a blog to learn more about programming and to teach others that may be struggling with the same subject that I was. Now I'm gonna create a series of posts about Jekyll, Liquid templates and Css as I learn it and modify my blog to have more of me on it. In an article about [DevOps from Henry Quinn @quinncuatro](https://dev.to/quinncuatro/learning-devops-in-public-c26) on [dev.to](http://dev.to), I got really intrigued with Learning in Public.

## What is learning in public?

Is exposing for all what you are learning or developing in that moment. Why? Because, when you teach others you end up learning more about it and helping others with the same subject. It helps you to memorize and practice the subject.

## Benefits to learn in public

You would be helping others to not struggle as you when you were learning, you will be practicing journaling and maybe another language (my case).

## Let's do it

To begin, what I'm gonna be writing in this series are CSS, Liquid Template and Jekyll, because that's what I'm dealing with to build my personal blog. Feel free to give me a feedback in the end to help me more.

### Why Jekyll?

Didn't want to host my blog anywhere and didn't want to have cost and problems with infrastructure and security, I really just want to focus in programming with a simple and fast result, so I end up picking Jekyll (and it's recommended by Github Pages tutorial).

Jekyll is a generator of statics sites from a specific template.

It's created in Ruby, so you have to have installed on your computer. In Jekyll's site has a tutorial to install Ruby and Jekyll.

To initialize your project you have to execute the command below:

    jekyll new nome-do-blog

It will create the structure of your project in his own folder.

Jekyll default is to use Minimal template. To find where the files are, just use the command bellow:

    bundle show minimal

It will show you the directory of it.

If you want to change the template and have in your versioning program, then you should copy the files to your project directory.

To build and execute your site it was never that easy!! Only execute the commands bellow on your project main folder.

    bundle exec jekyll build

After built:

    bundle exec jekyll s

Now you have your personal blog with Minimal Template on localhost:4000.

As I learn more and modify my personal blog to have my own style, I'll be doing more posts and explain it. 

That's all folks.

Don't forget to drink water.
