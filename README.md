Download Link: https://assignmentchef.com/product/solved-ee451-homework4-pass-message-in-a-ring
<br>
<h1>Examples</h1>

The “mpi examples” folder includes the source codes used in discussions and a pbs file ‘queue.pbs ’. To run an mpi program, for example, the ‘scatter.c’, follow the steps:

<ol>

 <li>login hpc-login3.usc.edu</li>

 <li>source /usr/usc/openmpi/default/setup.sh</li>

 <li>Go to your working directory which has ‘job.sl’ and ‘scatter.c’.</li>

 <li>mpicc -o go scatter.c</li>

 <li>sbatch job.sl</li>

 <li>After you get the email saying your job is completed, check ‘mpijob.out’ for output and ‘mpijob.err’ for any possible error.</li>

</ol>

For more information, you can visit https://hpcc.usc.edu/support/documentation/examples-of-mpi-programs/

<h1>1             Pass Message in a Ring</h1>

Write an MPI program that passes a value around a ring of 4 processes using the following steps.

<ol>

 <li>Process 0 initializes <em>Msg </em>= 451 and prints value of <em>Msg</em></li>

 <li>Process 0 sends the value of <em>Msg </em>to Process 1</li>

 <li>Process 1 receives the value of <em>Msg</em>, increases it by 1, prints the value and sends the current value of <em>Msg </em>to Process 2</li>

 <li>Process 2 receives the value of <em>Msg</em>, increases it by 1, prints the value and sends the current value of <em>Msg </em>to Process 3</li>

 <li>Process 3 receives the value of <em>Msg</em>, increases it by 1, prints the value and sends the current value of <em>Msg </em>to Process 0</li>

 <li>Process 0 receives the value of <em>Msg </em>from Process 3 and prints the value</li>

</ol>

Name this program as ‘p1.c’. Figure 1 illustrates the steps. The output messages look like:

<ul>

 <li>Process 0: Initially <em>Msg </em>= 451</li>

 <li>Process 1: <em>Msg </em>= 452</li>

 <li>Process 2: <em>Msg </em>= 453</li>

 <li>Process 3: <em>Msg </em>= 454</li>

 <li>Process 0: Received <em>Msg </em>= 454. Done!</li>

</ul>

Figure 1: Example diagram

<h1>2             Add 64 numbers using 4 processes</h1>

In the “number.txt” file, you can find 64 numbers. Your task is to write an MPI program with 4 processes to compute the sum of these 64 numbers. There are 3 approaches:

<ol>

 <li>Approach 1, name this program as p2 1.c:

  <ul>

   <li>Each process reads the entire <em>array</em>.</li>

   <li>Do in parallel: Process 0 computes]; Process 1 computes]; Process 2 computes]; Process 3 computes</li>

   <li>Process 1,2,3 send their partial <em>sum </em>to Process 0.</li>

   <li>Process 0 computes the sum of all the partial <em>sum</em>s and prints it out.</li>

  </ul></li>

 <li>Approach 2, name this program as p2 2.c:

  <ul>

   <li>Process 0 reads the <em>array</em></li>

   <li>Process 0 broadcasts the entire <em>array </em>to every process</li>

   <li>Do in parallel: Process 0 computes]; Process 1 computes]; Process 2 computes]; Process 3 computes</li>

   <li>Process 0 uses MPI SUM reduction to sum these partial <em>sum</em></li>

   <li>Process 0 prints out the result.</li>

  </ul></li>

 <li>Approach 3, name this program as p2 3.c:

  <ul>

   <li>Process 0 reads the array and scatters the entire <em>array </em>to every process using the <strong>scatter </strong></li>

   <li>Each process sums up the portion of the <em>array </em>it receives.</li>

   <li>Process 0 uses the <strong>gather </strong>operation to gather these partial <em>sum</em>s, computes the sum of all the partial <em>sum</em>s and prints it out.</li>

  </ul></li>

</ol>