---
layout: post
title: "DBF files and the pandas DataFrame"
description: ""
category: 
tags: [pandas, pysal, dataIO]
---
{% include JB/setup %}

DBF files and the pandas DataFrame

For the last few days, I have been playing with
[pandas](http://pandas.pydata.org), a Python library that
provides very nice data structures. If you are familiar with the R dataframe,
pandas has a similar class that gives you most of the sweetness from R in
Python, and some more. Check out the project site and have a look at [Wes'
site](http://blog.wesmckinney.com/), because it is under heavy development, constantly adding new features and improvements.

Anyhow, the other day I was extracting some Census data to dump it from a csv
into a dbf (so I could link it to a shapefile) and thought it would be useful
to write a little interface from the DBF file format in and out to a
pandas.DataFrame, using the easy API that PySAL provides. The [code](https://github.com/GeoDaSandbox/sandbox/blob/master/pyGDsandbox/dataIO.py) is already
on GitHub under the dataIO module, so please go ahead and check it out. If you
have the sandbox folder setup (see [here](http://geodasandbox.github.com/2012/03/28/how-to-get-up-and-running-with-the-geoda-center-sandbox/)), just import the functions:

    {% highlight python %}
    from pyGDsandbox.dataIO import df2dbf, dbf2df
    {% endhighlight %}

Right now it is mostly two functions:

    {% highlight python %}
    df2dbf(df, dbf_path)
    {% endhighlight %}

This allows you to quickly write out a DataFrame into a dbf file. Just pass in the DataFrame object and the desired path for the new dbf file to be created and you are good to go (if you are interested in specifying the DBF field specs yourself there is an option too, have a look at the documentation on the code). Note the DataFrame object needs to be "squared", that is every column has to have the same number of rows. Combined with the nice alignment, join and merge options that pandas offers, it is pretty powerful to easily join data to a shapefile for instance.

    {% highlight python %}
    dbf2df(dbf_path)
    {% endhighlight %}

The second option reads in a file straight into a DataFrame. Very straight forward, the header becomes the name of the columns and the whole file is read in. If you are interested only in a few columns, you can pass those in and only they will be read. The following command will only read 'VAR1' and 'VAR2' from 'dbf_path':

    {% highlight python %}
    dbf2df(dbf_path, cols=['VAR1', 'VAR2'])
    {% endhighlight %}

Finally, if you want any of the columns to be used as the DataFrame index, just pass it like this:

    {% highlight python %}
    dbf2df(dbf_path, index='my_index_var')
    {% endhighlight %}

This is a start for me to get familiar with the pandas data structures and it is by no means optimized or super efficient, so any idea or suggestion in that direction will be most welcome. Happy hacking!!!


