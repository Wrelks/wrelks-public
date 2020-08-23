---
layout: article
title: Superdense Coding
cover: /images/superdense-coding-circuit.png
key: aslkjdfgw9487o3289t6ry4gf
comment: true
aside:
  toc: true
author: Perry
---

>> #### Learn how to replicate the Superdense Coding Algorithm in qiskit

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

Superdense Coding in a nutshell is a quantum communication protocol that allows for a sender to send two classical bits of information to another person by utilizing only one qubit.

Superdense coding takes advantage of something called a 'bell circuit' 

> ##### A bell circuit is a combination of a Hadamard gate going into the control bit of the controlled not gate

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/bell-state-quantum-qiskit.png"/>
  </div>
</div>

<br>

A two qubit bell circuit in a perfect noiseless quantum computer will have an equal probability of getting either results, 00 or 11.

### How it works

In the superdense coding algorithm we have three different users.

* The first user shares the two outputs of a two qubit bell state with the receiver and the sender.

* The second user who is the sender, encodes the qubits 

* And the final user receives those qubits and decodes them

The final design looks a little like this

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/superdense-coding-circuit-1.png"/>
  </div>
</div>

>> Credit: Wikipedia.org

A good thing to try and think about is how a bell state truly works. Think about it, the control bit is entangled with the not gate. So when we set the control bit into a super position it also changes the target bit to a superposition as well, because they are entangled. 

We can denote the bell state mathematically like so,

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/quantum-bell-state.png"/>
  </div>
</div>

<br>

### The Encoder 

The encoders job is simple, take the first qubit from the bell state and apply a single gate operation to it. In the two qubit example of this algorithm there are four different ways for the encoder to encode their qubit. Either with a Identity gate (does no change), X-gate, Z-gate, or a combination of the Z and X-gate. Each of these four diffrent combinations represents an intended message. 

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/superdense-coding-protocol.png"/>
  </div>
</div>

>> Credit: Qiskit.org

So if I the sender wanted to pass on the message of 10 to my receiver, I would apply an X-gate.

<br>

### The Receiver 

The receivers job is bit easier. All they have to do is take the untouched second qubit from the initial bell state and the new encoded qubit from the sender and pass it through a 'reverse' bell circuit. 

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/superdense-coding-qiskit.png"/>
  </div>
</div>

the result will end up being what ever the sender has set their gate to. So in our example if the sender applied an X gate the receiver would decode the message and receive 10 as a result.

## Qiskit 

### Imports

    from qiskit import QuantumCircuit, execute, Aer, IBMQ
    from qiskit.visualization import plot_histogram

### Circuit

    qc = QuantumCircuit(2, 2)

    qc.h(0)
    qc.cx(0,1)

    qc.barrier()

    qc.x(0)

    qc.barrier()

    qc.cx(0,1)
    qc.h(0)

    for i in range(2):
      qc.measure(i, i)
    
### Printing Results

    sim_backend = BasicAer.get_backend('qasm_simulator')
    job = execute(qc, sim_backend, shots=1024)
    result = job.result()
    print('Simulator: ')
    counts = result.get_counts(qc) #just setting a var
    print(counts)
    plot_histogram(counts)

### Printing the circuit

    qc.draw(output="mpl")

If you did everything correctly your output should look like the following,

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/superdense-coding-experiment.png"/>
  </div>
</div>