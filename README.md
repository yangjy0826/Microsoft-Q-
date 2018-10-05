 # Quantum Computing Programming with Microsoft Q#
*Last updated: 2018-10-05*
***
Q# is the language developed by Microsoft, which can be used on many quantum algorithms. It should be driven by C#, and works on Visual Studio 2017. This project is based on the [Q# tutorial document](https://docs.microsoft.com/en-us/quantum/quantum-writeaquantumprogram?view=qsharp-preview&tabs=tabid-vs2017) given by Microsoft. I met some problems running the project, even though most of the work was only copy-paste. What is more, I would like to include some knowledge on quantum computing during the process. These are the main purposes of this md file.</br>
I will start by introducing how to setup the environment of Q#, and then explain the process of writing a first code in Q#.

## Contents
* [1 Before installation](#1-before-installation)
* [2 Installing Visual Studio and setting the environment](#2-installing-visual-studio-and-setting-the-environment)
* [3 Create a Bell state](#3-create-a-bell-state)
    * 3.1 Create a new project
    * 3.2 The first programme in Q#
    * 3.3 Create superposition -- Single quantum computing
        * 3.3.1 Pauli-X Gate
        * 3.3.2 Hadamard Gate
    * 3.4 Create entanglement -- Multiple quantum computing

## 1 Before installation
Q# can work on different operating systems including Windows, Linux and Mac, but make sure that it is 64-bit and has [.NET Core SDK 2.0](https://www.microsoft.com/net/learn/dotnet/hello-world-tutorial) or higher version installed.</br>
The simulator of Q# uses the instruction set of AUX, so if your CPU does not support AUX, the calculation speed will be not good enough. By using the sofware [CPU-Z](https://www.cpuid.com/softwares/cpu-z-android.html), you are able to figure out if your CPU sipport AUX.
After installing and opening CPU-Z, you can check by whether there is  `AUX` under `Instructions`, which is shown in Pic 1 below.</br>
</br>
![Pic 1](https://github.com/yangjy0826/Microsoft-Q-/blob/master/img/CPU.PNG)

## 2 Installing Visual Studio and setting the environment
Firstly download Visual Stuio 2017 from [Microsoft's official webpage](https://visualstudio.microsoft.com/downloads/), and make sure that it is the right version (2017).</br>
During the installation, at least the `Universal Windows Platform development` and `.NET desktop development` shuld be chosen.</br>
After the installation of Visual Studio, it is also necessary to install another extension software [Microsoft Quantum Development Kit](https://marketplace.visualstudio.com/items?itemName=quantum.DevKit). It can be finished by downloading the Q# VSIX file in the link, followed by double clicking.

## 3 Create a Bell state
Bell state specifies the quantum states of two qubits that represent the simplest examples of quantum entanglement. It can be realized by using Hadamard gate and CNOT gate, which will be introduced later.
### 3.1 Create a new project
Open the Visual Studio 2017, and then click  `File`-> `New`->`Project`. Then choose `Q# Application`, as is shown in the Pic 3.1 below.</br>
</br>
![Pic 3.1](https://github.com/yangjy0826/Microsoft-Q-/blob/master/img/new_project.PNG)</br>
Then you can find that Visual Studio automatically generate two files, one is `Operation.qs`, which is a Q# file, the other is `Driver.cs`, which is a C# file. We should first rename the Q# file into `Bell.qs`. </br>
Right now, the code in `Bell.qs` and `Driver.cs` is automatically generated when creating the new project, which is like this:</br>
**Code in `Bell.qs` is:**</br>
```C#
namespace Quantum.Bell 
{
    open Microsoft.Quantum.Primitive;    
    open Microsoft.Quantum.Canon;
    operation Operation () : ()    
    {
        body
        {
        }
    }
}
```
**Code in `Driver.cs` is:**</br>
```C#
using Microsoft.Quantum.Simulation.Core;
using Microsoft.Quantum.Simulation.Simulators;

namespace Quantum.Bell
{
    class Driver
    {
        static void Main(string[] args)
        {

        }
    }
}
```

### 3.2 The first programme in Q#
By following the step 1 to step 4 in the [tutorial document](https://docs.microsoft.com/en-us/quantum/quantum-writeaquantumprogram?view=qsharp-preview&tabs=tabid-vs2017), you are able to add content into the `Bell.qs` and `Driver.cs`, which is like this:</br>
**Code in `Bell.qs` is:**</br>
```C#
namespace Quantum.Bell
{
    open Microsoft.Quantum.Primitive;
    open Microsoft.Quantum.Canon;
    operation Set (desired: Result, q1: Qubit) : ()
    {
        body
        {
            let current = M(q1);            // The 'let' keyword binds mutable variables
            if (desired != current)
            {
              X(q1); // NOT gate
            }
        }
    }

    operation BellTest (count : Int, initial : Result) : (Int, Int) 
    {
        body
        {
          mutable numOnes = 0;
      using (qubits = Qubit[1])
      {
          for (test in 1..count)
          {
              Set (initial, qubits[0]);
              let res = M (qubits[0]);
              // Count the number of ones we saw:
              if (res == One)
{
                  set numOnes = numOnes + 1;
              }
          }
          Set(Zero, qubits[0]);
      }
      // Return number of times we saw a |0> and number of times we saw a |1>
      return (count-numOnes, numOnes);
        }
    }
}

```
Above we add two `operation` into the `Bell.qs`. `operation` is the basic execution unit in Q#, just like the `function` in C, C++ and Java. </br>
**Code in `Driver.cs` is:**</br>
```C#
using Microsoft.Quantum.Simulation.Core;
using Microsoft.Quantum.Simulation.Simulators;
namespace Quantum.Bell
{
    class Driver
    {
        static void Main(string[] args)
        {
            using (var sim = new QuantumSimulator()) // sim is the Q# quantum similator
            {
                // Try initial values
                Result[] initials = new Result[] { Result.Zero, Result.One };
                foreach (Result initial in initials)
                {
                    var res = BellTest.Run(sim, 1000, initial).Result;  // Run is the method to run the quantum simulation
                    var (numZeros, numOnes) = res;
                    System.Console.WriteLine($"Init:{initial,-4} 0s={numZeros,-4} 1s={numOnes,-4}");
                }
            }
            System.Console.WriteLine("Press any key to continue...");
            System.Console.ReadKey();
        }
    }
}
```
Press `Debug`->`Start debugging`(F5) or `start without debugging`(Ctrl+F5), the code above will be built and executed. </br>
Sometimes there may be an error saying `the name XX does not exist in the current context unity`, which means that there is something wrong with the `References` of this project. The fastest solution to this error is by downloading [this repository](https://github.com/yangjy0826/Microsoft-Q-) and making changes in the dowloaded `Bell.qs` and `Driver.cs` files.
The correct result for this part is:</br>
```
Init:Zero 0s=1000 1s=0
Init:One  0s=0    1s=1000
Press any key to continue...
```
The result shows that the observation is 100% the same with the initial value. If the initial state is `Zero`, we will observe `Zero` state all the time; while if the initial state is `One`, we will observe `One` all the time.

### 3.3 Create superposition -- Single quantum computing
In this part, by following the step 5 in the [tutorial document](https://docs.microsoft.com/en-us/quantum/quantum-writeaquantumprogram?view=qsharp-preview&tabs=tabid-vs2017), we can make some changes of the code in part 3.2 to create superposition for a qubit.</br>
#### 3.3.1 Pauli-X Gate
If we add an Pauli-X Gate (X Gate) in the operation `BellTest`:
```diff
+ X(qubits[0]);
let res = M (qubits[0]);
```
We can get a result  which is totally in contrast with that in part 3.2:
```
Init:Zero 0s=0    1s=1000
Init:One  0s=1000 1s=0
```
Now if the initial state is `Zero`, we will observe `One` state all the time; while if the initial state is `One`, we will observe `Zero` all the time.That is because X gate is similar to the logical NOT in classical computing. It can map `Zero` to `One`, and `One` to `Zero`.
#### 3.3.2 Hadamard Gate
If we delete the X Gate, and add a Hadamard Gate (H Gate) in the same position:
```diff
- X(qubits[0]);
+ H(qubits[0]);
let res = M (qubits[0]);
```
The result becomes:
```
Init:Zero 0s=484  1s=516
Init:One  0s=522  1s=478
```
Now if the initial state is `Zero`, we have 50% probability to observe `Zero` and 50% probability to observe `One`, and vice versa. This is because the H Gate is used to create superposition, 
### 3.4 Create entanglement -- Multiple quantum computing
