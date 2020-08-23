---
layout: article
title: How to write your first qiskit program! 
cover: /images/quantum-circuit qiskit.png
key: d9q8wtggadsia
aside:
  toc: true
author: Perry
comment: true
description: How to write your first qiskit circuit using jupyter notebook. Quantum computing a gentle introduction 
---

>> #### Learn how to create your first qiskit circuit!

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

Assuming that you are already at the jupyter notebook menu, locate yourself to the top right and create a new folder.
From there create a new python3 notebook file inside of the new folder.

#### Step 1
<div class="card">
  <div class="card__image">
    <img class="image" src="/images/jupyter-notebook-examples.png"/>
  </div>
</div>

#### Step 2
<div class="card">
  <div class="card__image">
    <img class="image" src="/images/jupyter-notebook-examples2.png"/>
  </div>
</div>

<br>

### The Code

In the first cell of the notebook create your imports 

    from qiskit import QuantumCircuit, execute, Aer, IBMQ
    from qiskit.providers.ibmq import least_busy
    from qiskit.tools.monitor import job_monitor
    from qiskit.visualization import plot_histogram

Afterwards press <strong>Shift</strong> & <strong>Enter</strong> at the same time to run the cell!

Now the quantum circuit can be defined

    n = 2 #number of qubits
    qc = QuantumCircuit(n, n)

This creates a circuit of 2 qubits in size

afterwards gates can then be added to the circuit

Lets say I want to add an X gate to qubit 0 and a Hadamard gate to qubit 1, I would enter the following 

    qc.x(0)
    qc.h(1)

A small loop can then be added to measure the circuit outputs 
 
    for i in range(n):
      qc.measure(i, i)

from here we can now tell qiskit to execute the circuit on a local simulator

    sim_backend = BasicAer.get_backend('qasm_simulator')
    job = execute(qc, sim_backend, shots=1024)
    result = job.result()
    print('Simulator: ')
    counts = result.get_counts(qc) 

> The 'shots=1024' variable tells qiskit how many times to run the circuit. In the example above, the circuit will run 1024 different times
> The reason we have quantum computers run a circuit many different times is because in real quantum computers noise occurs. Noise can interfere with the results so to find the the desirable output we run it many times and pick the most concurrent output as the official result.

>> The simulator does **NOT** simulate noise by default.

Qiskit gives us many different ways to print out the answers, for this circuit we will print it out as a bar chart 

    plot_histogram(counts)

<br>

### Putting it together!

The final code now looks like this 

    from qiskit import QuantumCircuit, execute, Aer, IBMQ
    from qiskit.providers.ibmq import least_busy
    from qiskit.tools.monitor import job_monitor
    from qiskit.visualization import plot_histogram

    n = 2 #number of qubits
    qc = QuantumCircuit(n, n)

    qc.x(0)
    qc.h(1)

    for i in range(n):
      qc.measure(i, i)

    sim_backend = BasicAer.get_backend('qasm_simulator')
    job = execute(qc, sim_backend, shots=1024)
    result = job.result()
    print('Simulator: ')
    counts = result.get_counts(qc) 
    plot_histogram(counts)

If you did everything right the following output should look a little like this :

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/qiskit-measurement.png"/>
  </div>
</div>

<br>

### Visualizing the circuit

The qiskit visualization library allows us to print out the circuit in either two ways, ascii text, or mpl.

#### Ascii Output

    print(qc)

The output:

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/qiskit-circuit-draw.png"/>
  </div>
</div>

---

#### Mpl Output

    qc.draw(output="mpl")

The output:

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/qiskit-circuit-draw2.png"/>
  </div>
</div>
<br>

## Using real Quantum Computers

### IBMQ API Token

The first step to getting your circuits to run on a real quantum computer is to create an account at the IBM Quantum Experience [here.](https://quantum-computing.ibm.com/)

Once you are all signed up ready to go head up to your profile icon and copy the API token 

#### Step 1

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/the-ibm-quantum-experience.png"/>
  </div>
</div>

#### Step 2

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/ibm-quantum-account.png"/>
  </div>
</div>

<br>

### The Code

The first thing that needs to be done is loading in your API token, and your provider

    IBMQ.enable_account("IBMQ_API_TOKEN")
    my_provider = IBMQ.get_provider()

>> #### NOTE: Once you run the program once with the IBMQ.enable_account("#########"), delete that line! The program will automatically remember your account credentials. Run this line each time you start up your environment!

<!--   save_account(IBMQ_API_TOKEN)

>> #### Then after running that once, delete it, and add this line in 

    load_account()

>> This will load in your **SAVED** Account credentials
--> 

Afterwards you can then configure the quantum computer you want to use. Because IBM's Quantum Computers get tons of requests per minute it's important to use the least busy feature that comes with the IBMQ library. This feature picks out the quantum computer that is currently getting the least number of requests.

    least_busy_device = least_busy(my_provider.backends(simulator=False))
    print("Least Busy:", least_busy_device)

> 'simulator=False' of course means that the code will look for a backend that is not a local simulator. In short it will look for **ANY** available quantum computer.

Now we can initialize the job to run on the new quantum backend

    backend = least_busy_device
    job = execute(qc, backend, shots=1024)
    result = job.result()
    print("Results: ")
    counts = result.get_counts(qc)
    plot_histogram(counts)

Now the entirety of the code looks like this 

    from qiskit import QuantumCircuit, execute, Aer, IBMQ
    from qiskit.providers.ibmq import least_busy
    from qiskit.tools.monitor import job_monitor
    from qiskit.visualization import plot_histogram

    n = 2 #number of qubits
    qc = QuantumCircuit(n, n)

    qc.x(0)
    qc.h(1)

    for i in range(n):
      qc.measure(i, i)

    least_busy_device = least_busy(my_provider.backends(simulator=False))

    print("Least Busy:", least_busy_device)

    backend = least_busy_device
    job = execute(qc, backend, shots=1024)
    result = job.result()
    print("Results: ")
    counts = result.get_counts(qc) 
    plot_histogram(counts)

Your result should look a little like this if you ran the example as written 

<div class="card">
  <div class="card__image">
    <img class="image" src="/images/quantum-noise-circuits.png"/>
  </div>
</div>

<br>

### Noise

You may've notice that 00 and 10 came out as a result to our circuit, but how can this be? Our provided circuit should make it impossible for those results?

The answer is **noise**, real quantum computers aren't perfect yet and so they experience noise which cause faulty answers. This is why how I was explaining earlier why we run a circuit thousands of different times to find the correct answers. I can look at this chart and see that 01 and 11 are the correct outputs because they were the highest probable outputs. 


<!-- backend = least_busy_device
job = execute(qc, backend, shots=1024)
result = job.result()
print('Simulator: ')
counts = result.get_counts(qc) 
plot_histogram(counts) -->

<!--example.pynb file-->