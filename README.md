# Fire escape planner

The goal of the sistem is to present a program that is able to develop a detailed plan of
actions, to follow in case of a fire disaster. This will comprise a step-by-step approach,
giving all possible solutions for getting from an initial state (e.g. smoke, fire intensity, location)
 to the final desired state (or goal- here: safety).

The program is written in FAL -http://www.dc.fi.udc.es/~cabalar/fal/ -(similar to Prolog).


# Installation steps

 - Download and install gcc (only if not available in our unixlinux distribution).
  
 - Download and install lparse.

 - Download lparse-1.1.2 source package.
 
 - Type cd in the terminal, to change to the directory containing lparse source code and type .configure to configure lparse for the system.
``` shell
 .configure
 ``` 
 
- Type make to compile the binaries.
``` shell
make
```

- Type make install to install lparse.
``` shell
make install
```

- If we want to remove the object files from the source code directory we may type make clean to do it.
``` shell
make clean
```

  By default, lparse is installed to the directory usrlocalbin. We may change the directory by giving the configure option the option - -prefix=path.

 - Download and install smodels.

 - Download smodels-2.34 source package.
 
 - In the terminal, change to the directory containing the source code.
 
 - Type make, to compile the binaries. It will output the smodels executable file.
 
 - Move the smodels file to usrbin.

  -Download and install the SWI-Prolog interpreter from httpwww.swi-prolog.orgDownload.html.
  
  -Download and uncompress the file fal-1.0.tar.gz in a separate directory, from httpwww.dc.fi.udc.es~cabalarfalfalf-1.0.tar.gz

  Then run 'make' in the created directory.
  
  In order to do this, type the following commands in the terminal
  
``` shell
$ gunzip fal-1.0.tar-gz
$ tar -xvf fal-1.0.tar
$ cd falf-1.0
$ make
```

  Now, the 'falf' and 'getterms' executables should be present in the falf-1.0 directory.

  In order to make them accessible, make a copy of each of them in some directory in your PATH (for instance, usrlocalbin).

# Small fire example #

The following lines of code present a possible scenario, where one is in the middle of the
room and a fire breaks out. While there is no smoke, a possibility would be to simply walk to
the door, and get outside- alternatively, the person would have to crawl. However, there is no
need to get outside, if, in order to arrive at a state of safetiness, one could simply extinguish
the fire manually. This, of course, if the fire is small and can easily be handled.

We will create a file with the name & extension 'fire.fal' in which we will write our code.

### _Relevant Code_ ###

```shell
instances

location window, door, middle, outside.


fluents

fire: boolean.
smoke: boolean.
at: location.
is_small: boolean.
is_safe: boolean.


actions

crawl_to: location.
walk_to: location.
extinguish: boolean.


rules

is_safe:- at = outside.
is_safe:- at != outside, not fire.

not fire’ :- extinguish, fire.
:- extinguish, not is_small.

at’ = walk_to.
:- not unknown(walk_to), smoke.
:- not unknown(walk_to), is_safe.
:- not unknown(walk_to), extinguish.
:- not unknown(walk_to), is_small, fire.
:- walk_to = at.

at’ = crawl_to.
:- not unknown(crawl_to), not smoke.
:- not unknown(crawl_to), is_safe.
:- not unknown(crawl_to), extinguish.
:- not unknown(crawl_to), is_small, fire.
:- crawl_to = at.


initially

fire.
not smoke.
at = middle.
not is_safe.
is_small.
goals
is_safe.
```


# Running the program #

In order to run the program, first, open a command window, making sure to be located in the
project directory, where you have saved the written text file with the extension ”.fal”.
Now, create a temporary file for the program to use at runtime. Make sure to name the file
”your filename.fal.tmp” (in this case the original file is fire.fal).
``` shell
>fire.fal.tmp
```
After this, in order to receive the shortest plan - in the number of steps - required to reach
the desired goal, run the program, with the following command :
``` shell
falf -l 50 fire.fal
```
The _-l 50_  option assumes that there would be less than, or a maximum of 50 steps required
to solve the problem. The solution builds itself incrementally, starting with the smallest number
of steps and stopping when the first possible solution based on that number of steps is reached.
If we want to obtain all the possible results of the minimal path found, we should type _-n
0_ before the _-l 50_ option.
``` shell 
falf -n 0 -l 50 fire.fal 
```
Bellow is a screen capture with the computed result of the program. The numbers on the
left side of the screen represent the current state. As a state is represented by the instances
of all the fluents, a list of the fluents follows with their instances. Arbitrarily placed, between
the fluents there is an action that triggers the change of state. In the case of the state 0, the
action is ”extinguish”. This leads us to state 1 , where we do not have a fire anymore, arriving
at safetiness.

![alt tag](https://scontent.fomr1-1.fna.fbcdn.net/v/t1.0-9/16864378_718331338344950_375224592939287104_n.jpg?oh=337b4d934a3400574578412f44c074ee&oe=596423C6)

## Another example ##

_Escaping through a window from an apartment_

![alt tag](https://scontent.fomr1-1.fna.fbcdn.net/v/t1.0-9/16832171_718331341678283_4230535414651733512_n.jpg?oh=13298cd284350c485cc9e639991e62a6&oe=59259D70)

* _For the complete documentation see the FireEscapePlanner_docum.pdf_
