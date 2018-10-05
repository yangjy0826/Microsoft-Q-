# Quantum Computing Programming with Microsoft Q#
Q# is the language developed by Microsoft, which can be used on many quantum algorithms. It should be driven by C#. This project is based on the [Q# tutorial document](https://docs.microsoft.com/en-us/quantum/quantum-writeaquantumprogram?view=qsharp-preview&tabs=tabid-vs2017) given by Microsoft. I met some problems running the project, even though most of the work was only copy-paste. What is more, I would like to include some knowledge on quantum computing during the process. These are the main purposes of this md file.</br>
I will start by introducing how to setup the environment of Q#.
## Check the CPU
The simulator of Q# uses the instruction set of AUX, so if your CPU does not support AUX, the calculation speed will be not good enough. By using the sofware [CPU-Z](https://www.cpuid.com/softwares/cpu-z-android.html), you are able to figure out if your CPU sipport AUX. </br>
After installing and opening CPU-Z, you can check by whether there is 'AUX' under 'Instructions', which is shown in Pic 1 below.</br>
![image](https://github.com/yangjy0826/Microsoft-Q-/blob/master/img/CPU.PNG)
