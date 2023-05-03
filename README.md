Download Link: https://assignmentchef.com/product/solved-cs285-assignment-1-imitation-learning-2
<br>
The goal of this assignment is to experiment with imitation learning, including direct behavior cloning and the DAgger algorithm. In lieu of a human demonstrator, demonstrations will be provided via an expert policy that we have trained for you. Your goals will be to set up behavior cloning and DAgger, and compare their performance on a few different continuous control tasks from the OpenAI Gym benchmark suite. Turn in your report and code as described in Section 4. The starter-code for this assignment can be found at

<a href="https://github.com/berkeleydeeprlcourse/homework_fall2020">https://github.com/berkeleydeeprlcourse/homework_fall2020</a>

You have the option of running the code either on Google Colab or on your own machine. Please refer to the README for more information on setup.

1           Behavioral Cloning

<ol>

 <li>The starter code provides an expert policy for each of the MuJoCo tasks in OpenAI Gym. Fill in the blanks in the code marked with Todo to implement behavioral cloning. A command for running behavioral cloning is given in the Readme file.</li>

</ol>

We recommend that you read the files in the following order. For some files, you will need to fill in blanks, labeled TODO.

<ul>

 <li>scripts/run hw1 behavior cloning.py (you should read this file, but you don’t need to edit it)</li>

 <li>infrastructure/rl trainer.py</li>

 <li>agents/bc agent.py (another read-only file)</li>

 <li>policies/MLP policy.py</li>

 <li>infrastructure/replay buffer.py infrastructure/utils.py</li>

 <li>infrastructure/pytorch py See the homework pdf for more details.</li>

</ul>

<ol start="2">

 <li>Run behavioral cloning (BC) and report results on two tasks: the Ant environment, where where a behavioral cloning agent should achieve at least 30% of the performance of the expert, and one environment of your choosing where it does not. Here is how you can run the Ant task:</li>

</ol>

python cs285/scripts/run_hw1.py 

–expert_policy_file cs285/policies/experts/Ant.pkl 

–env_name Ant-v2 –exp_name bc_ant –n_iter 1 

–expert_data cs285/expert_data/expert_data_Ant-v2.pkl 

–video_log_freq -1

When providing results, report the mean and standard deviation of your policy’s return over multiple rollouts in a table, and state which task was used. When comparing one that is working versus one that is not working, be sure to set up a fair comparison in terms of network size, amount of data, and number of training iterations. Provide these details (and any others you feel are appropriate) in the table caption.

<strong>Note</strong>: What “report the mean and standard deviation”means is that your eval batch size should be greater than ep len, such that you’re collecting multiple rollouts when evaluating the performance of your trained policy. For example, if ep len is 1000 and eval batch size is 5000, then you’ll be collecting approximately 5 trajectories (maybe more if any of them terminate early), and the logged Eval AverageReturn and Eval StdReturn represents the mean/std of your policy over these 5 rollouts. Make sure you include these parameters in the table caption as well.

<strong>Tip</strong>: To generate videos of the policy, remove the flag –video log freq -1 However, this is slower, and so you probably want to keep this flag on while debugging.

<ol start="3">

 <li>Experiment with one set of hyperparameters that affects the performance of the behavioral cloning agent, such as the amount of training steps, the amount of expert data provided, or something that you come up with yourself. For one of the tasks used in the previous question, show a graph of how the BC agent’s performance varies with the value of this hyperparameter. In the caption for the graph, state the hyperparameter and a brief rationale for why you chose it.</li>

</ol>

<h1>2           DAgger</h1>

<ol>

 <li>Once you’ve filled in all of the TODO commands, you should be able to run DAgger.</li>

</ol>

python cs285/scripts/run_hw1.py 

–expert_policy_file cs285/policies/experts/Ant.pkl 

–env_name Ant-v2 –exp_name dagger_ant –n_iter 10 

–do_dagger –expert_data cs285/expert_data/expert_data_Ant-v2.pkl 

–video_log_freq -1

<ol start="2">

 <li>Run DAgger and report results on the two tasks you tested previously with behavioral cloning (i.e., Ant + another environment). Report your results in the form of a learning curve, plotting the number of DAgger iterations vs. the policy’s mean return, with error bars to show the standard deviation. Include the performance of the expert policy and the behavioral cloning agent on the same plot (as horizontal lines that go across the plot). In the caption, state which task you used, and any details regarding network architecture, amount of data, etc. (as in the previous section).</li>

</ol>