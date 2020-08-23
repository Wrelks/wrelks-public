---
layout: article 
title: How to install Qiskit
cover: /images/qiskit-documentation.png
key: t487fy12123g
aside:
  toc: true
author: Perry
comment: true
description: How to install qiskit on windows and linux | quantum computing an applied approach 
#tags: [jekyll, tags, user-experience]
---
<!--https://hitcounter.pythonanywhere.com/--> 
<!--https://github.com/brentvollebregt/hit-counter
^^Docs for hit counter^^
-->

>> #### Installing qiskit on Windows & Linux

<!--work on adding a like button with firebase-->  
<!--https://console.firebase.google.com/u/0/project/wrelkss/overview-->
<!-- https://mazipan.space/create-simple-like-button-using-firebase-rtdb/en/ -->

<br>

<!--more-->

<!-- The core Firebase JS SDK is always required and must be listed first -->
<script src="https://www.gstatic.com/firebasejs/7.17.1/firebase-app.js"></script>

<!-- TODO: Add SDKs for Firebase products that you want to use
     https://firebase.google.com/docs/web/setup#available-libraries -->
<script src="https://www.gstatic.com/firebasejs/7.17.1/firebase-analytics.js"></script>

<script>
  // Your web app's Firebase configuration
  var firebaseConfig = {
    apiKey: "AIzaSyCGVCAZ6RL0Gjuc9sq6fdnAETbc1oDGLns",
    authDomain: "wrelkss.firebaseapp.com",
    databaseURL: "https://wrelkss.firebaseio.com",
    projectId: "wrelkss",
    storageBucket: "wrelkss.appspot.com",
    messagingSenderId: "170107683865",
    appId: "1:170107683865:web:3f40853c493c7929a9d688",
    measurementId: "G-26XJY2LG7G"
  };
  // Initialize Firebase
  firebase.initializeApp(firebaseConfig);
  firebase.analytics();
</script>

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

## Anaconda 

The first step is to install the latest python 3.x version of anaconda [here.](https://www.anaconda.com/products/individual)

**Windows Users:**

Once you've installed anaconda you need to locate your windows search bar and type "anaconda prompt"
<div class="card">
  <div class="card__image">
    <img class="image" src="/images/anaconda-windows-activate.png"/>
  </div>
</div>
Linux users can simply enter conda commands straight into the terminal

<br>

### Creating the Environment
Once anaconda has been installed, enter in the following command.

    conda create -n test python=3

This will create an environment in python version 3 with the name of "test"

Now you can activate your new environment with the following. Of course replacing "test" with the name of your env.

    conda activate test

<br>

## Installing Qiskit

Once inside your environment, enter the following. This will install qiskit into your environment.

    pip install qiskit

<br>

### Verify Installation

to verify the installation, first type "python" into your terminal

    python

this will open a python terminal, from where you can import qiskit

    from qiskit import *

if the console returns to a new line afterwards, it means that qiskit was installed successfully!

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/anaconda-install-qiskit.png"/>
  </div>
</div>

To exit the python terminal enter in the exit command 

    exit()

<br>

## Install Qiskit Visualization

Installing qiskit visualization adds tons of visualization features to jupyter notebooks for qiskit programs

I would **highly** recommend to install this extension

    pip install qiskit[visualization]

<br>

## Install qiskit_textbook

Installing the qiskit textbook allows you to create many more cool things inside of the qiskit framework such as quantum board games and a whole lot more. That's why I always recommend new users to install qiskit_textbook

**Windows Users need to install pywin32**

    pip install pywin32

then

    pip install git+https://github.com/qiskit-community/qiskit-textbook.git#subdirectory=qiskit-textbook-src

<br>

### Verify Installation

You can verify the installation the same way as before, by opening a python terminal and typing in the following 

    from qiskit_textbook.games import hello_quantum

if it returns a blank output then you have successfully installed the qiskit textbook library!

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/install-qiskit-on-windows.png"/>
  </div>
</div>

<!--more-->
