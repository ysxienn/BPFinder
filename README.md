# BPFinder
**BPFinder**(**B**ranched **P**athway **F**inder) is a method for finding metabolic branched pathways between a source compound and a target compound.
**BPFinder** consists of three main steps: **First**, BPFinder finds linear pathways from source to target by tracking the movement of atom groups through metabolic networks. **Second**, BPFinder determines the branched compounds in the linear pathways based on the structure of the conserved atom groups from the source compound, and merges these linear pathways into branched metabolic pathways by the branched compounds. **Finally**, BPFinder sorts the resulting branched pathways by the combined information of reaction thermodynamics, compound similarity and the conserved atom groups to pick out more biochemically feasible branched metabolic pathways for the user.

# Requirements and installation
1. BPFinder was written and tested on Java with version "1.8.0_201". **Java with version "1.8.0_201"(or higher)** need to be installed to work with BPFinder.
2. The data required for BPFinder program to find branched pathways are preserved in MySQL Database with version "8.0.14". To work with BPFinder, **MySQL Database with version "8.0.14"(or higher)** need to be installed. 
3. To output resulting branched pathways by directed graph, the results can be visualized using the graph visualization software graphViz with version "2.38.0". Users can install **graphViz with version "2.38.0"(or higher)** to obtain the resulting branched pathways by directed graph.

# Download data and program
BPFinder program is packaged as a JAR bundle called BPFinder.jar. To provide ease of use, users can download **BPFinder.jar** to run BPFinder with command line(see detail in <a  href="#1">Usage</a>). 

# Dataset Preparation
To import the data of metabolic network, the user should type the command lines as follows: 
1. download **fga.sql** from git
2. use shell to create user of MySQL with username "root" and password "123456".
3. enter mysql with command line ``` mysql -u -root -p ``` and input the password "123456"
4. create database fga with command line ```create database fga```
5. enter database fga with command line ```use fga```
6. import the data fga.sql with command line ```source D://fga.sql```(assume fga.sql is under D://)

<a name="1"># Usage</a>
BPFinder can run in command line as follows:

```java -jar (the path of BPFinder.jar) (the path of setting file) ```

**the path of BPFinder.jar** is the path of BPFinder.jar.

**the path of setting file** is the path of the setting file which is used to adjust the running parameters of BPFinder.

for example: ```java -jar D://BPFinder.jar D://C00022_C00183.txt ```

# Running parameters
User can use setting file to adjust the running patameters of BPFinder, and the descreption of each paramaters are listed as follows:
| Option | Description | Default value |
| -----  | ------| ----|
| sourceCompound | Source compound in KEGG format | Required |
| targetCompound | Target compound in KEGG format | Required |
| k | Number of the candidate linear pathways | 2000 |
| numberOfTheMinimalAtomGroups | Number of the minimal atom groups transferred from source to target compound | 2 |
| mergingStrategy | Merging rule for branched compound(overlapping,non-overlapping,default rule. The default rule merging strategy means that BPFinder will first search the branched pathways by non-overlapping rule, and then BPFinder will search the branched pathways by overlapping rule in the case of no branched pathways are returned by non-overlapping rule) | default |
| aSf | aSf is a specific weight parameter for BPFinder running on PC(The PC version can be downloaded here), which is used to adjust the relative weights of Gibbs free energy of reaction when ranking the resulting pathways. | 0.1 |
| aT | aT is a specific weight parameter for BPFinder running on PC(The PC version can be downloaded here), which is used to adjust the relative weights of conserved atom groups when ranking the resulting pathways. | 0.2 |
| aS | aS is a specific weight parameter for BPFinder running on PC(The PC version can be downloaded here), which is used to adjust the relative weights of compound similarity when ranking the resulting pathways. | 0.1 |
| aP | aP is a specific weight parameter for BPFinder running on PC(The PC version can be downloaded here), which is used to adjust the relative weights of the branched compounds when ranking the resulting pathways.| 0.8 |



