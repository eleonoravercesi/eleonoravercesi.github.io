# Install Concorde with CPLEX
This tutorial will guide you through the process of building together CPLEX and Concorde.
It merges together information from the [here](https://mertbakir.gitlab.io/operations-research/how-to-install-cplex-ibm-academic-initiative/) and [here](https://www.leandro-coelho.com/install-and-run-concorde-with-cplex/), applyng minor changes.

Tested on the following system:
- Ubuntu 20.04.2 LTS

If you test this instruction to other machines, write me an email and I will update the tutorial.

## CPLEX
1. Register for the CPLEX Academic Initiative [here](https://www.ibm.com/academic/home). Use your institutional email.
2. Note: if you tried to register with a new institutional email, and you were already registered with an old one, you may need to clear your broswer cache and cookies.
3. Go [here](https://www.ibm.com/academic/topic/data-science) and click on "Software", then choose "IBM ILOG CPLEX Optimization Studio".
4. Click to "Download". It is possible that you have to click on it multiple times, otherwise you'll get an error.
5. Search for "IBM ILOG CPLEX Optimization Studio 12.9 for Linux x86-64 Multilingual" (Image: CNZM2ML) and download it.
6. Select it, scroll down, agree to the terms and conditions, and click "Download".
7. Select a directory where to save the files and complete the download.
8. Once the download is complete, go in the selected folder and run 

```bash
chmod +x cplex_studio129.linux-x86-64.bin
sudo ./cplex_studio129.linux-x86-64.bin
```
The `sudo` command is necessary to install the software in the default directory `/opt/ibm/ILOG/CPLEX_Studio129/` (which I recommend). This tutorial assume that you have used this directory.

9. Follow the instructions and install the software. This part should be pretty straightforward and will be not commented further.

## Concorde
1. Download Concorde from the [Concorde website](https://www.math.uwaterloo.ca/tsp/concorde/downloads/downloads.htm) or by directly clicking [here](https://www.math.uwaterloo.ca/tsp/concorde/downloads/codes/src/co031219.tgz).
2. Extrct the files
```bash
gunzip co031219.tgz
tar xvf co031219.tar
```
4. In the file `concorde/Makefile.in` change the line
```bash
LIBFLAGS = @LIBS@
```
into
```bash
LIBFLAGS = @LIBS@ -lpthread
```
5. In the file `concorde/TSP/Makefile.in` change the line
```bash
LIBFLAGS = @LIBS@
```
into
```bash
LIBFLAGS = @LIBS@ -lpthread -ldl
```
6. Create a folder called `./concorde/cplex` and copy in it the following files 
```bash
cp /opt/ibm/ILOG/CPLEX_Studio129/cplex/include/ilcplex/*h .
cp /opt/ibm/ILOG/CPLEX_Studio129/cplex/lib/x86-64_linux/static_pic/libcplex.a .
```
(This command assume that you have used the default installation directory for CPLEX)
7. Create a folder called `build` in the folder `concorde`.
8. In the folder `build` run
```bash
../configure --prefix=/full/path/concorde/build/ --with-cplex=/full/path/concorde/cplex/
```
It is important to use the full path for all the repositories.
9. Run
```bash
make
```

10. It will fail, it's okay :) Now we have the file `concorde/build/concorde.h` to work on. In `concorde.h`  use "find and replace" of any text editor to change all `*new)` to `*NEW)` and all `*class)` to `*CLASS)`

11. In `concorde/LP/lpcplex8.c` replace
```c
#undef  CC_CPLEX_DISPLAY
```
With
```c
#undef  CC_CPLEX_DISPLAY
#ifndef CPX_PARAM_FASTMIP
#define CPX_PARAM_FASTMIP 1017
#endif
```

12. In `concorde/build/`, rename `concorde.a` to `libconcorde.a`

13. In the folder `build` run again
```bash
make
```
14. In the folder `build` run
```bash
./TSP/concorde
```
This should work, printing the help message of Concorde.