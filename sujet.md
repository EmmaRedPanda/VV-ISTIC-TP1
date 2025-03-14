# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?


## Answers

### 1. The case Mars Climate Orbiter :
 https://www.leparisien.fr/sciences/quand-la-science-semmele-une-erreur-de-conversion-et-la-sonde-secrase-sur-mars-21-08-2021-GAWI22Z4GVAX3E7VYN42CPWMCA.php
The Mars Climate Orbiter was a spatiale probe launched by NASA the 11 december 1998 to study matien climat. The navigation Team used the metric systeme for it's calculation, the conception and construction team on the other hand gave crucial navigation data in the imperial metric system. the error here is inbetween component making it a global bug.
As a consequence, NASA lost a major amount of money (around 327,6 millions dollars) and delayed discovery, causing a big impact on their credibility. 
A complete documentation could've avoid this multi-million dollar loss for NASA.


### 2. 
COLLECTIONS-837 : Remove HasherCollection from bloomfilter code base here, the issue is that the collection isn't compatible with the Hasher's interface. Incompatibiliti between this two element makes it a global bug.
It was decided ti resolve this problem by deleting the HasherCollection and every attached test, no test was added back.


### 3. 
#### Netflix did a lot of experimentations for their tests:
  - résilier des instances de machines virtuelles
  - injecter de la latence dans les requêtes entre les services
  - faire échouer les requêtes entre les services
  - faire échouer un service interne
  - rendre une région Amazon entière indisponible

#### They automatized the experiences following thoose setps:
  - defining the "stable state" as a mesurable output of a normal system.
  - Assuming this state follows in both experimental and witness group.
  - Introducing variables simulating real life event like serveur shut down or hardware malfunctioning.
  - trying too refute the hypothesis by searching differences between the witness group and the experimental group.
#### At the end of an experiment, either everything work or a weakness was discover, showing the path to improvment.
Internetscale organisation use similar approches.


### 4. 
### Advantages:
#### Secure, fast and portable semantics: 
  - execution safe, quick, deterministic
  - independant from the language, the material and the plateform
  - interoperability
  - easy on the web platform
#### Safe and efficient representation:
  - compact
  - easy to decode
  - easy to validate
  - easy to compile
  - easy to generate for produceur
  - streamable and parallelizable
This does not mean WebAssembly shouldn't be tested.

### 5.
#### What are the main advantages of the mechanized specification?   
- the mechanized specification isn't handwritten, contains support for interaction with the host environment, and offers proof of the two soundness properties

#### Did it help improving the original formal specification of the language?
- Yes it helped improved AND correct the original formal specification of the language.

#### What other artifacts were derived from this mechanized specification?
- A separate verified executable interpreter and type checker where derived from this mechanized specifiaction.

#### How did the author verify the specification?
- Several deficiencies in the official WebAssembly specification where uncovered by their proof and modelling work.

#### Does this new specification removes the need for testing?
- No, the specification still need to be updated along WebAssembly's life throughout testing.
