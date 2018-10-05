# Quantum Computing Programming with Microsoft Q#
*last updated: 2018-10-05*
***
Q# is the language developed by Microsoft, which can be used on many quantum algorithms. It should be driven by C#, and works on Visual Studio 2017. This project is based on the [Q# tutorial document](https://docs.microsoft.com/en-us/quantum/quantum-writeaquantumprogram?view=qsharp-preview&tabs=tabid-vs2017) given by Microsoft. I met some problems running the project, even though most of the work was only copy-paste. What is more, I would like to include some knowledge on quantum computing during the process. These are the main purposes of this md file.</br>
I will start by introducing how to setup the environment of Q#.

## 1 Before installation
Q# can work on different operating systems including Windows, Linux and Mac, but make sure that it is 64-bit and has [.NET Core SDK 2.0](https://www.microsoft.com/net/learn/dotnet/hello-world-tutorial) or higher version installed.</br>
The simulator of Q# uses the instruction set of AUX, so if your CPU does not support AUX, the calculation speed will be not good enough. By using the sofware [CPU-Z](https://www.cpuid.com/softwares/cpu-z-android.html), you are able to figure out if your CPU sipport AUX.
After installing and opening CPU-Z, you can check by whether there is 'AUX' under 'Instructions', which is shown in Pic 1 below.</br>
</br>
![Pic 1](https://github.com/yangjy0826/Microsoft-Q-/blob/master/img/CPU.PNG)

## 2 Installing Visual Studio and Setting the environment
Firstly download Visual Stuio 2017 from [Microsoft's official webpage](https://visualstudio.microsoft.com/downloads/), and make sure that it is the right version (2017).</br>
During the installation, at least the 'Universal Windows Platform development' and 'NET desktop development' shuld be chosen.</br>
After the installation, it is also necessary to install another extension software [Microsoft Quantum Development Kit](https://marketplace.visualstudio.com/items?itemName=quantum.DevKit). It can be finished by downloading the Q# VSIX file in the link, followed by double clicking.

## 3 First code using C# -- Creating a Bell state
### 3.1 Create a new project
Open the Visual Studio 2017, and then click 'File'->'New'->'Project'. Then choose 'Q# Application' as is shown in the Pic 3.1 below.</br>
</br>
![Pic 3.1](https://github.com/yangjy0826/Microsoft-Q-/blob/master/img/new_project.PNG)
