---
layout: post
title: "How to get up and running with the GeoDa Center sandbox"
description: "Get setup to use this blog"
category: 
tags: [git]
---
{% include JB/setup %}

To kick things off, we are going to first explain how to check out the
repository we have setup on Github and get it up and running. You will only
have to do this once and then you will be able to easily stay up to date and
use all the code goodies we will be posting on the blog. Please note this is a
first introductory post to get everyone on the same page; if you are familiar
with version control software in general and git in particular, not much of
this will be new.

##Check out the code repository

Since we host the code on a Github repository, the first thing you need to do
is to install git. Go to the download section of the official website, grab
the binary that better suits your platform and follow the instructions, which
are not much harder than click, click and boom, done!!! Now you are ready to
check out the GeoDa Sandbox. Fire up a terminal and go to the folder where you
want to download the repository:

    cd /path/to_my_folder/

Then all the magic happens with the following command:

    git clone https://github.com/GeoDaSandbox/sandbox.git

This tells git to go to the Github server, grab the GeoDa Sandbox
folder and start a read-only copy in your local machine. You have now
all the code in your computer.

The sandbox is organized in different folders depending on the
programming language used to write the code. Since we are pretty much
a Python shop, one of the most important ones is 'pyGDsandbox'. If you
like Python as much as we do, you might want to add it to your python
path so you can easily import code from there in your scripts.

##Add the Python folder to your path

###\*nix systems (Linux/Mac)

Simply edit your 'bash_profile'/'bashrc' file adding the path. Since
it is hidden, you will have to use a terminal to uncover it. On the
Mac, type:

    open ~/.bash_profile

In linux you probably have to replace 'open' by 'gedit' or other
editor of choice. This will open the file where Python looks at
everytime you import a module. Add the following line at the
bottom:

    export PYTHONPATH=${PYTHONPATH}:"/path/to_my_folder/sandbox/"

Save and quit the file. Now go back to the terminal and source
it:

    source ~/.bash_profile

You are good to go! To make sure it works, open a python
session and try to import, you should see a confirmation
message like this:

    >>> from pyGDsandbox import install_test
         
             GeoDaSandbox Python module is up and running,
             happy hacking!!!
                  
    >>>

##Updating the repository

One of the nice things of version control is that once you have
checked out a repository, it is very easy to stay up to date and
be able to enjoy the latest developments. In our case, anytime
we add new code, you will only have update the folder with a simple
command and the code will be ready to use in your computer. To do
it, navigate to the folder on the terminal as before and type:

    git pull

This will go look at the server and bring any new change we have
commited. That easy!!!
