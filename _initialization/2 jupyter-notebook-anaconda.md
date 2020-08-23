---
layout: article
title: How to install Jupter Notebook
key: ad8273tgdy8usad
cover: /images/jupyter-notebook-anaconda.png
aside:
  toc: true
author: Perry
comment: true
description: Learn how to install and configure jupyter notebook via anaconda / linux command line.
---

>> #### Installing Jupyter Notebook on Windows & Linux

<br>

<!--more-->

<!--<script>

  let xmlHttp = new XMLHttpRequest();
  xmlHttp.open('GET', 'https://hitcounter.pythonanywhere.com/count', false);
  xmlHttp.send(null);
  count = xmlHttp.responseText;

</script>

<center>
<div class="card">
  <div class="card__content">
    <p class="warning">
    Views: <Strong>
    <script type="text/javascript">
            document.write(count)
    </script>
    </Strong>
    </p>
  </div>
</div>
</center> -->

## Getting started 

First make sure that you are inside of your anaconda environment

    conda acitvate 'name'

Afterwards you can install jupyter notebook with either conda or pip

### Anaconda install

    conda install -c conda-forge notebook

### Pip install 

    pip install notebook 

**Congratulations** jupyter notebook is now installed 🎉

<br>

### Password Config

Now you can set your notebook password with the following command

> Make a easy to remember password

    jupyter notebook password

<br>

## Starting juypter notebook 

To start up a notebook session enter in the following command into your terminal 

    jupyter notebook

A new browser window should've been opened automatically pointing to the notebook Interface

If you weren't automatically directed, go to your browser can enter in the following url

    localhost:8888/

If this still didn't work double check the output in the terminal to see if any url was provided 

<img class="image image--xl" src="/images/jupyter-notebook-tutorial.png"/>

<br>

**Next tutorial shows how to create your first qiskit program inside of jupyter notebook**
