---
layout: article
title: Quantum Teleportation
cover: /images/quantum-teleportation-protocol.png
key: asojufduhtaw783i6e
comment: true
aside:
  toc: true
author: Perry
mathjax: true
---

>> #### Learn how to replicate the Quantum Teleportation Algorithm in qiskit

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

## What is it?

The idea of the quantum teleportation is being able to *teleport* a qubit from one user to another while maintaining the qubit state. Unlike the previous algorithm, this algorithm uses a classical communication channel in it's design. The reason we use a classical channel is because of the no cloning theorem. As it sounds, the no cloning theorem states that you can't just clone and teleport a qubit state from point a to point b. As you'll see later this is why we implement a classical channel.

## How it works

As with the previous algorithm, this one also requires three different users. One user, the third party, prepares a set of two entangled qubits with a bell state. The two other users will of course be the sender and the receiver. The third party shares the two entangled qubits with the sender and the receiver.

The bell state as shown before is prepared like this 

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/bell-state-quantum-qiskit.png"/>
  </div>
</div>

This gives us the state of $$\vert\psi\rangle = \alpha\vert00\rangle + \beta\vert11\rangle$$ which in short means an equal probability to roll a \vert00\ or \vert11\

---

Next our sender prepares a bell measurement, however the target bit of this bell measurement is coming in from the control bit of the previous bell state.

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/quantum-teleportation-algorithm.png"/>
  </div>
</div>

<br>

Now we preform a measurement on q0 and q1 and send the results to the classical register of c0 and c1 

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/quantum-teleportation-article.png"/>
  </div>
</div>

Now we can implement the receiver 

The receiver will use the following gates if certain values are met, those values can be found here 

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/quantum-teleportation-experiment.png"/>
  </div>
</div>

>> <strong>Congratulations the algorithm is completed!</strong>

From here we measure the outputs then send add an X followed by a Z gate at the end of the whole circuit to represent the receiver

The final result of the circuit should look a little like this,

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/quantum-teleportation-and-entanglement.png"/>
  </div>
</div>




