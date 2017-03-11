# Fire escape planner

The program is written in FAL - httpwww.dc.fi.udc.es~cabalarfal -(similar to Prolog) and provides a step by step plan that starts from an initial given state (e.g. smoke, fire intensity, location) and works its way to the desired goal state - in this case safety.


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

 
 # Results
 
 - Small fire example (the code from running-simple-example)
 div
 img src=httpsscontent.fomr1-1.fna.fbcdn.netvt1.0-916864378_718331338344950_375224592939287104_n.jpgoh=fa5c1f481620199bbfec553459cbef0f&oe=593C96C6
 div
 
 - Apartment fire
div
img src=httpsscontent.fomr1-1.fna.fbcdn.netvt1.0-916832171_718331341678283_4230535414651733512_n.jpgoh=13298cd284350c485cc9e639991e62a6&oe=59259D70
 div
