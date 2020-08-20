Pillars: A Consistent CGRA Design Framework
=====================
Pillars is an open-source CGRA design framework with
consistency to assist in design space exploration and hardware
optimization of CGRAs. Pillars provides a Scala-based architecture
description language (ADL) for an architect to specify
a CGRA architecture, which produces a unified, high-quality
and synthesizable architectural abstraction. Auxiliary hardware
modules and Verilog RTL are automatically generated
according to the architectural abstraction, allowing physical
implementation on an FPGA as an overlay. An integer linear
programming (ILP) CAD tool can map data-flow graph (DFG)
onto the specified CGRA, generating contexts for CGRA RTL level
simulation.



## Installing Necessary Dependencies

|  Package  |  Version  |
|  :----: | :----: |
| Java  | ≥ 8.0 |
| [Scala](https://www.scala-lang.org/download/)  | ≥ 2.12.10 |
| [Chisel](https://github.com/freechipsproject/chisel3)  | ≥ 3.2.2 |
| [Gurobi](https://www.gurobi.com/)  | ≥ 8.1.1 |
| [Verilator](https://www.veripool.org/wiki/verilator)  | ≥ 3.916 |

### Installing Scala
Install Scala either by installing an IDE such as IntelliJ, or sbt, Scala's build tool.
You can install sbt in Ubuntu using following command:
 ``` shell
 echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
 curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
 sudo apt-get update
 sudo apt-get install sbt
 ```

It may take a few minutes.

### Installing Chisel
Chisel will be installed automatically according to build.sbt the first time you run sbt.

### Installing Gurobi

Go to [Gurobi website](https://www.gurobi.com/) to register and request an academic license, and download the Gurobi library.
In bin subdirectory of Gurobi directory, please run 
``` shell
./grbgetkey <key-you-obtained>
``` 
to activate your Gurobi, detailed in [Gurobi installation guide](https://www.gurobi.com/documentation/9.0/quickstart_linux/software_installation_guid.html#section:Installation).

After Gurobi is activated, please run
``` shell
mkdir lib
ln $GUROBI_HOME$/linux64/lib/gurobi.jar lib/
``` 
in this directory to use the Gurobi library in this project.

### Installing Verilator

To install Verilator as a package:
``` shell
sudo apt-get install verilator
``` 

## Project Tree

```
.
├── app_mapping_results             //some pre-generated mapping results
├── build.sbt                       //the library dependencies in sbt
├── doc                             //documents of APIs in Pillars
├── DOT                             //some DFGs in DOT format
├── Makefile                        
├── MRRG                            //some MRRGs
├── README.md 
├── scalastyle-config.xml           //the scalastyle file
├── scalastyle-test-config.xml      //the scalastyle file
└── src
    └── main
        └── scala
            └── tetriski
                └── pillars
                    ├── archlib     //the library of elements and blocks
                    ├── core        //the core of Pillars
                    ├── examples    //some examples showing how to use Pillars
                    ├── hardware    //hardware implemented in Chisel
                    ├── mapping     //mapping tools
                    ├── Pillars.scala
                    ├── testers     //testers in Pillars
                    └── util        //utiliy for realizing hardware
```


## Quick Start

### Running Tests

To test some existing applications and different CGRA architectures, run:
``` shell
make build
make run
``` 


If everything is setup correctly, all tests will be passed.

### Running Mapping

To test mapping tools, run
``` shell
make mapping
``` 
If everything is setup correctly, the same mapping results as origin will be obtained in the app_mapping_results subdirectory.
You can also do mapping with other DFGs and MRRGs generated by your CGRA designs.

### Running End2end tutorial

You can study the end2end tutorial in the examples subdirectory.
To test it, run
``` shell
make end2end
``` 

### Designing CGRA Architectures

You can design your own CGRA architectures by create blocks like what in the archlib subdirectory.

If you want to add or modify a basic module, you can design your own elements and basic chisel modules.
Do not forget to keep the modeling consistency and runtime consistency as mentioned in annotation.