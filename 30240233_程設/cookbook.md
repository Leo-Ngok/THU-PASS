# Tutorial for setting up development environments

## 0. Prerequisites

Before proceed, review the following concepts.

1. Compiler: 					A tool that converts your code to assembly language.
2. Assembler:                  A tool that converts assembly code to object file.
3. Linker:                          A tool that merges multiple object files (and sometimes a binary executable, see incremental linking) to a single binary executable.
4. Binary Executable:    A file that can be run by the operating system.
5. Editor:                         A software that allows modifying the contents of a source code.
6. Toolchain:                  A software collection that contains compilers, assemblers and linkers.
7. IDE:                             Integrated development environments, that consists of a development toolchain and an editor.



## 1. Set up

Recommended environment setup:

C/C++: WSL(GCC)/MAC(Clang) + VSCODE

Java: Eclipse

Python: Anaconda + Jupyter notebook

.NET (C#/VB .NET): Visual studio 2022

Unity: Unity IDE + VSCODE

Android: android studio

### 1.1. C/C++ 

The following depicts the installation and the initialization of the C/C++ software development environment, by using VSCODE as the editor, and GCC as the toolchain. For the sake of convenience, it is recommended to install it in the WSL.

#### 1.1.1. VSCODE

Download link: https://code.visualstudio.com/

#### 1.1.2. WSL(Windows only)

> Meanwhile there are other toolchains such as MSVC, MINGW and Clang, GCC is recommended for C/C++ development in Windows platform. Despite the fact that MINGW resembles GCC, MINGW implements socket connection different from native GCC, and it is often troublesome.  What's worse,  it is not convenient to debug using VSCODE when MINGW is used.

1. Go to Control Panel > Programs > Turn Windows features on or off: 

2. Check the box for "Windows Subsystem for Linux" and press OK to exit.

3. Go to Microsoft Store and search for Ubuntu 20.04 LTS, and download it.

4. Press Windows+R and type wsl to start the console terminal.

5. Follow the instructions to set up the ubuntu environment.



In the WSL ubuntu console, type the following to see if GCC is installed properly.

```bash
g++ --version
```

If not, install GCC by typing the following in the console:

```bash
sudo apt-get install build-essential gdb
```



#### 1.1.3. Initializations in VSCODE

##### 1.1.3.1. Set up environment variables  (For mac users only, otherwise skip until 'create new project' )

After VSCODE is downloaded, drag it into the 'Applications' folder via finder.

Then, open VSCODE and press ```⌘``` + ```shift``` + ```P``` , to open the **command palette**.

Type the following sequentially.

```
Shell Command: Install 'code' command in PATH
```

##### 1.1.3.2. Initialize a project

To create a new project, make a new directory in WSL:

 ```bash
 mkdir proj 
 ```

Then, start visual studio code there.

```bash
code .
```

For WSL users, when you are prompted to install VSCODE, let it finish first.

On the left is a panel showing the file structure of the current working directory in the form of a tree diagram. 

On top of it, just below the ***<username> [WSL: UBUNTU]*** section,  the first button enables you to create a new file. 

Press the first button (new file) to create a new source file, namely ``` main.cpp ``` (or other names you wish).

Paste the following content right in the code editor.

```c
#include <stdio.h>
int global_var;
int main(void) {
    int local_var;
    printf("Input A = local_var, B = global_var.\n");
    scanf("%d %d", &local_var, &global_var);
    printf("local_var = %d, global_var = %d\n", local_var, global_var);
    return 0;
}
```

##### 1.1.3.3. Debug your code

Press F5 and choose C++ (GDB/LLDB) to start running(debugging) the code.

If necessary, breakpoints could be set to see the behaviors of the commands. Just click the whitespace on the left of the line numbers to toggle a red dot. That is an indicator of breakpoints. 

When the code is being debugged, it executes everything right before the line prior to the breakpoint. 

You may see the current value of local variables in **Locals** under **VARIABLES**. You may also modify it directly where necessary.

Alternatively, you can inspect other variables available to the current scope of execution by typing in the name of variable under **WATCH** section. However, this is read-only. 

You may also inspect the recursion level of the current function, i.e. all the functions required to be called before entering the current function, in **CALL STACK**.