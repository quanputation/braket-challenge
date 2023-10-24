Amazon Braket
Developer Guide
Amazon Braket Developer Guide
Amazon Braket: Developer Guide
Copyright © 2023 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.
Amazon's trademarks and trade dress may not be used in connection with any product or service that is not
Amazon's, in any manner that is likely to cause confusion among customers, or in any manner that disparages or
discredits Amazon. All other trademarks not owned by Amazon are the property of their respective owners, who may
or may not be affiliated with, connected to, or sponsored by Amazon.
Amazon's trademarks and trade dress may not be used in connection with any product or service that is not
Amazon's, in any manner that is likely to cause confusion among customers, or in any manner that disparages or
discredits Amazon. All other trademarks not owned by Amazon are the property of their respective owners, who may
or may not be affiliated with, connected to, or sponsored by Amazon.
Amazon Braket Developer Guide
Table of Contents
What is Amazon Braket? ..................................................................................................................... 1
Amazon Braket terms and concepts ............................................................................................. 2
AWS terminology and tips for Amazon Braket ....................................................................... 4
How it works ..................................................................................................................................... 6
Amazon Braket quantum task flow .............................................................................................. 6
Third-party data processing ......................................................................................................... 7
Core repositories and plugins for Braket ....................................................................................... 7
Core repositories ................................................................................................................ 7
Plugins .............................................................................................................................. 7
Supported devices .............................................................................................................................. 8
IonQ ....................................................................................................................................... 10
Rigetti ..................................................................................................................................... 10
Oxford Quantum Circuits (OQC) ................................................................................................. 11
QuEra ..................................................................................................................................... 11
Local state vector simulator (braket_sv) ................................................................................... 12
Local density matrix simulator (braket_dm) ................................................................................ 12
Local AHS simulator (braket_ahs) ............................................................................................ 12
State vector simulator (SV1) ...................................................................................................... 13
Density matrix simulator (DM1) .................................................................................................. 13
Tensor network simulator (TN1) ................................................................................................. 14
Embedded simulators ............................................................................................................... 15
PennyLane’s lightning simulators ....................................................................................... 15
Compare simulators .................................................................................................................. 15
Regions and endpoints ...................................................................................................................... 19
Pricing ............................................................................................................................................ 20
Near real-time cost tracking ...................................................................................................... 20
Best practices for cost savings ................................................................................................... 21
Quotas ............................................................................................................................................ 23
Additional quotas and limits ...................................................................................................... 31
When will my quantum task run? ....................................................................................................... 33
Status change notifications in email or SMS ................................................................................ 33
QPU availability windows and status .......................................................................................... 33
Queue visibility ........................................................................................................................ 33
Enable Amazon Braket ...................................................................................................................... 36
Prerequisites ............................................................................................................................ 36
Steps to enable Amazon Braket ................................................................................................. 36
Get started ...................................................................................................................................... 37
Create an Amazon Braket notebook instance ............................................................................... 37
Run your first circuit using the Amazon Braket Python SDK ........................................................... 39
Explore the algorithm library ..................................................................................................... 42
Hello AHS: Run your first Analog Hamiltonian Simulation .............................................................. 42
AHS ................................................................................................................................ 42
Interacting spin chain ....................................................................................................... 43
Arrangement ................................................................................................................... 44
Interaction ....................................................................................................................... 46
Driving field ..................................................................................................................... 47
AHS program ................................................................................................................... 48
Running on local simulator ................................................................................................ 48
Analyzing simulator results ................................................................................................ 49
Running on QuEra’s Aquila QPU ......................................................................................... 51
Analyzing QPU results ...................................................................................................... 52
Next ............................................................................................................................... 53
Work with Amazon Braket ................................................................................................................. 54
Construct circuits in the SDK ..................................................................................................... 55
iii
Amazon Braket Developer Guide
Gates and circuits ............................................................................................................. 55
Manual qubit allocation .................................................................................................... 59
Verbatim compilation ........................................................................................................ 60
Noise simulation .............................................................................................................. 60
Inspecting the circuit ........................................................................................................ 61
Result types ..................................................................................................................... 63
Run your circuits with OpenQASM 3.0 ......................................................................................... 66
What is OpenQASM 3.0? ................................................................................................... 66
When to use OpenQASM 3.0 ............................................................................................. 67
How OpenQASM 3.0 works ................................................................................................ 67
Prerequisites .................................................................................................................... 67
What OpenQASM features does Braket support? .................................................................. 67
Create and submit an example OpenQASM 3.0 quantum task ................................................ 71
Support for OpenQASM on different Braket Devices ............................................................. 73
Simulate noise with OpenQASM 3.0 ................................................................................... 81
Qubit rewiring with OpenQASM 3.0 .................................................................................... 82
Verbatim Compilation with OpenQASM 3.0 ......................................................................... 83
The Braket console ........................................................................................................... 83
More resources ................................................................................................................. 83
Computing gradients with OpenQASM 3.0 ........................................................................... 83
Submitting quantum tasks to QPUs and simulators ...................................................................... 84
Example quantum tasks on Amazon Braket ......................................................................... 85
Submitting quantum tasks to a QPU .................................................................................. 88
Running a quantum task with the local simulator ................................................................. 90
Quantum task batching ..................................................................................................... 90
Set up SNS notifications (optional) ..................................................................................... 91
Inspecting compiled circuits ............................................................................................... 92
Submit an analog program using QuEra’s Aquila .......................................................................... 92
Hamiltonian ..................................................................................................................... 92
Braket AHS program schema ............................................................................................. 93
Braket AHS task result schema ........................................................................................... 95
QuEra device properties schema ........................................................................................ 99
Monitoring and tracking quantum tasks .................................................................................... 105
Tracking quantum tasks from the Amazon Braket SDK ........................................................ 106
Advanced logging ........................................................................................................... 107
Monitoring quantum tasks through the Amazon Braket console ............................................ 109
Working with Boto3 ................................................................................................................ 111
Turn on the Amazon Braket Boto3 client ........................................................................... 111
Configure AWS CLI profiles for Boto3 and the Amazon Braket SDK ........................................ 114
Pulse control on Amazon Braket ....................................................................................................... 116
Braket Pulse ........................................................................................................................... 116
Frames .......................................................................................................................... 116
Ports ............................................................................................................................. 116
Waveforms .................................................................................................................... 116
Roles of frames and ports ....................................................................................................... 117
Rigetti ........................................................................................................................... 118
OQC ............................................................................................................................. 119
Hello Pulse ............................................................................................................................ 119
Accessing native gates using pulses .......................................................................................... 122
Hello Pulse using OpenPulse .................................................................................................... 123
Amazon Braket Hybrid Jobs ............................................................................................................. 129
What is a Hybrid Job .............................................................................................................. 129
When to use Amazon Braket Hybrid Jobs .................................................................................. 130
Run your local code as a hybrid job .......................................................................................... 130
Create a hybrid job from local Python code ....................................................................... 130
Install additional Python packages and source code ............................................................ 132
Save and load data into a hybrid job instance .................................................................... 133
iv
Amazon Braket Developer Guide
Best practices for hybrid job decorators .............................................................................. 21
Run a hybrid job with Amazon Braket Hybrid Jobs ...................................................................... 135
Create your first Hybrid Job ..................................................................................................... 136
Inputs, outputs, environmental variables, and helper functions ..................................................... 142
Inputs ........................................................................................................................... 142
Outputs ......................................................................................................................... 143
Environmental variables .................................................................................................. 143
Helper functions ............................................................................................................. 144
Save job results ...................................................................................................................... 144
Save and restart hybrid jobs using checkpoints .......................................................................... 145
Define the environment for your algorithm script ....................................................................... 146
Use hyperparameters .............................................................................................................. 148
Configure the hybrid job instance to run your algorithm script ..................................................... 149
Cancel a Hybrid Job ................................................................................................................ 151
Using parametric compilation to speed up Hybrid Jobs ............................................................... 152
Use Amazon Braket Hybrid Jobs and PennyLane to run a QAOA algorithm ..................................... 153
Accelerate your hybrid workloads with embedded simulators from PennyLane ................................ 155
Using lightning.gpu for Quantum Approximate Optimization Algorithm workloads ............. 156
Quantum machine learning and data parallelism ................................................................ 157
Build and debug a hybrid job with local mode ........................................................................... 160
Bring your own container (BYOC) ............................................................................................. 161
When is bringing my own container the right decision? ....................................................... 161
Recipe for bringing your own container ............................................................................. 161
Running Braket hybrid jobs in your own container .............................................................. 165
Configure the default bucket in AwsSession ............................................................................ 166
Interact with hybrid jobs directly using the API .......................................................................... 166
Use PennyLane with Amazon Braket ................................................................................................. 169
Amazon Braket with PennyLane .............................................................................................. 169
Hybrid algorithms in Amazon Braket example notebooks ............................................................. 170
Hybrid algorithms with embedded PennyLane simulators ............................................................ 171
Adjoint gradient on PennyLane with Amazon Braket simulators .................................................... 171
Error mitigation .............................................................................................................................. 173
Error mitigation on IonQ Aria ................................................................................................... 173
Sharpening .................................................................................................................... 173
Security ......................................................................................................................................... 175
Shared responsibility for security .............................................................................................. 175
Data protection ...................................................................................................................... 175
Data retention ........................................................................................................................ 176
Managing access to Amazon Braket .......................................................................................... 176
Amazon Braket resources ............................................................................................... 176
Notebooks and roles ....................................................................................................... 177
About the AmazonBraketFullAccess policy ......................................................................... 177
About the AmazonBraketJobsExecutionPolicy policy ........................................................... 181
Restrict user access to certain devices ............................................................................... 183
Amazon Braket updates to AWS managed policies ............................................................. 184
Restrict user access to certain notebook instances .............................................................. 184
Restrict user access to certain S3 buckets .......................................................................... 185
Service-linked role .................................................................................................................. 185
Service-linked role permissions for Amazon Braket ............................................................. 186
Resilience .............................................................................................................................. 187
Compliance validation ............................................................................................................. 187
Infrastructure Security ............................................................................................................. 187
Third Party Security ................................................................................................................ 188
Troubleshoot .................................................................................................................................. 189
Access denied exception .......................................................................................................... 189
A quantum task is failing creation ............................................................................................ 189
An SDK feature does not work ................................................................................................. 189
v
Amazon Braket Developer Guide
A hybrid job fails due to an exceeded quota .............................................................................. 190
Something stopped working in your notebook instance ............................................................... 190
Troubleshoot OpenQASM ........................................................................................................ 191
Include statement error ................................................................................................... 191
Non-contiguous qubits error ............................................................................................ 191
Mixing physical qubits with virtual qubits error .................................................................. 192
Requesting result types and measuring qubits in the same program error .............................. 192
Classical and qubit register limits exceeded error ................................................................ 192
Box not preceded by a verbatim pragma error .................................................................... 192
Verbatim boxes missing native gates error ......................................................................... 193
Verbatim boxes missing physical qubits error ..................................................................... 193
The verbatim pragma is missing "braket" error ................................................................... 193
Single qubits cannot be indexed error ............................................................................... 193
The physical qubits in a two qubit gate are not connected error ........................................... 194
GetDevice does not return OpenQASM results error ............................................................ 194
Local simulator support warning ...................................................................................... 195
VPC endpoints (PrivateLink) ............................................................................................................. 196
Considerations for Amazon Braket VPC endpoints ....................................................................... 196
Set up Braket and PrivateLink .................................................................................................. 196
Step 1: Launch an Amazon VPC if needed ......................................................................... 196
Step 2: Create an interface VPC endpoint for Braket ........................................................... 197
Step 3: Connect and run Braket quantum tasks through your endpoint .................................. 197
More about creating an endpoint ............................................................................................. 197
Control access with Amazon VPC endpoint policies ..................................................................... 198
Tagging resources ........................................................................................................................... 199
Using tags ............................................................................................................................. 199
More about AWS and tags ....................................................................................................... 199
Supported resources in Amazon Braket ..................................................................................... 199
Tag restrictions ...................................................................................................................... 200
Managing tags in Amazon Braket ............................................................................................. 200
Add tags ....................................................................................................................... 200
View tags ...................................................................................................................... 200
Edit tags ........................................................................................................................ 201
Remove tags .................................................................................................................. 201
Example of CLI tagging in Amazon Braket ................................................................................. 201
Tagging with the Amazon Braket API ........................................................................................ 201
Monitor with CloudWatch ................................................................................................................ 203
Amazon Braket Metrics and Dimensions ................................................................................... 203
Supported Devices .................................................................................................................. 203
Amazon Braket Events with EventBridge ........................................................................................... 204
Monitor quantum task status with EventBridge .......................................................................... 204
Example Amazon Braket EventBridge event ............................................................................... 205
Logging with CloudTrail .................................................................................................................. 207
Amazon Braket Information in CloudTrail ................................................................................. 207
Understanding Amazon Braket Log File Entries .......................................................................... 208
Create a Braket notebook using CloudFormation ................................................................................ 210
Step 1: Create an Amazon SageMaker lifecycle configuration script ............................................... 210
Step 2: Create the IAM role assumed by Amazon SageMaker ........................................................ 211
Step 3: Create an Amazon SageMaker notebook instance with the prefix amazon-braket- .............. 212
API and SDK Reference ................................................................................................................... 213
Document history ........................................................................................................................... 214
vi
Amazon Braket Developer Guide
What is Amazon Braket?
Amazon Braket is a fully managed AWS service that helps researchers, scientists, and developers get
started with quantum computing. Quantum computing has the potential to solve computational
problems that are beyond the reach of classical computers because it harnesses the laws of quantum
mechanics to process information in new ways.
Gaining access to quantum computing hardware can be expensive and inconvenient. Limited access
makes it difficult to run algorithms, optimize designs, evaluate the current state of the technology,
and plan for when to invest your resources for maximum benefit. Braket helps you overcome these
challenges.
Braket offers a single point of access to a variety of quantum computing technologies. With Braket, you
can:
• Explore and design quantum and hybrid algorithms.
• Test algorithms on different quantum circuit simulators.
• Run algorithms on different types of quantum computers.
• Create proof of concept applications.
Defining quantum problems and programming quantum computers to solve them requires a new set
of skills. To help you gain these skills, Braket offers different environments to simulate and run your
quantum algorithms. You can find the approach that best suits your requirements and get started quickly
with a set of example environments called notebooks.
Braket development has three stages — build, test, and run:
Build - Braket provides fully managed Jupyter notebook environments that make it easy to get started.
Braket notebooks are pre-installed with sample algorithms, resources, and developer tools, including the
Amazon Braket SDK. With the Amazon Braket SDK, you can build quantum algorithms and then test and
run them on different quantum computers and simulators by changing a single line of code.
Test - Braket provides access to fully managed, high-performance quantum circuit simulators. You can
test and validate your circuits. Braket handles all the underlying software components and Amazon
Elastic Compute Cloud (Amazon EC2) clusters to take away the burden of simulating quantum circuits on
classical high performance computing (HPC) infrastructure.
Run - Braket provides secure, on-demand access to different types of quantum computers. You have
access to gate-based quantum computers from IonQ, OQC, and Rigetti, as well as an Analog Hamiltonian
Simulator from QuEra. You also have no upfront commitment, and no need to procure access through
individual providers.
About quantum computing and Braket
Quantum computing is in its early developmental stage. It’s important to understand that no universal,
fault-tolerant quantum computer exists at present. Therefore, certain types of quantum hardware are
better suited for each use case and it’s crucial to have access to a variety of computing hardware. Braket
offers a variety of hardware through third-party providers.
Existing quantum hardware is limited due to noise, which introduces errors. The industry is in the Noisy
Intermediate Scale Quantum (NISQ) era. In the NISQ era, quantum computing devices are too noisy to
sustain pure quantum algorithms, such as Shor’s algorithm or Grover’s algorithm. Until better quantum
error correction is available, the most practical quantum computing requires the combination of classical
1
Amazon Braket Developer Guide
Amazon Braket terms and concepts
(traditional) computing resources with quantum computers to create hybrid algorithms. Braket helps you
work with hybrid quantum algorithms.
In hybrid quantum algorithms, quantum processing units (QPUs) are used as co-processors for CPUs, thus
speeding up specific calculations in a classical algorithm. These algorithms utilize iterative processing, in
which computation moves between classical and quantum computers. For example, current applications
of quantum computing in chemistry, optimization, and machine learning are based on variational
quantum algorithms, which are a type of hybrid quantum algorithm. In variational quantum algorithms,
classical optimization routines adjust the parameters of a parameterized quantum circuit iteratively,
much in the same way the weights of a neural network are adjusted iteratively based on the error in a
machine learning training set. Braket offers access to the PennyLane open source software library, which
assists you with variational quantum algorithms.
Quantum computing is gaining traction for computations in four main areas:
• Number theory — including factoring and cryptography (for example, Shor’s algorithm is a primary
quantum method for number theory computations)
• Optimization — including constraint satisfaction, solving linear systems, and machine learning
• Oracular computing — including search, hidden subgroups, and order finding (for example, Grover’s
algorithm is a primary quantum method for oracular computations)
• Simulation — including direct simulation, knot invariants, and quantum approximate optimization
algorithm (QAOA) applications
Applications for these categories of computations can be found in financial services, biotechnology,
manufacturing, and pharmaceuticals, to name a few. Braket offers capabilities and example notebooks
that can already be applied to many proof of concept problems in addition to certain practical problems.
Amazon Braket terms and concepts
The following terms and concepts are used in Braket:
Analog Hamiltonian Simulation
Analog Hamiltonian Simulation (AHS) is a distinct quantum computing paradigm for direct
simulation of time-dependent quantum dynamics of many-body systems. In AHS, users directly
specify a time-dependent Hamiltonian and the quantum computer is tuned in such a way that it
directly emulates the continuous time evolution under this Hamiltonian. AHS devices are typically
special-purpose devices and not universal quantum computers like gate-based devices. They
are limited to a class of Hamiltonians they can simulate. However, since these Hamiltonians are
naturally implemented on the device, AHS does not suffer from the overhead required to formulate
algorithms as circuits and implement gate operations.
Braket
We named the Braket service after the bra-ket notation, a standard notation in quantum mechanics.
It was introduced by Paul Dirac in 1939 to describe the state of quantum systems, and it is also
known as the Dirac notation.
Braket hybrid job
Amazon Braket has a feature called Amazon Braket Hybrid Jobs that provides fully managed
executions of hybrid algorithms. A Braket hybrid job consists of three components:
1. The definition of your algorithm, which can be provided as a script, Python module, or Docker
container.
2. The hybrid job instance, based on Amazon EC2, on which to run your algorithm. The default is an
ml.m5.xlarge instance.
2
Amazon Braket Developer Guide
Amazon Braket terms and concepts
3. The quantum device on which to run the quantum tasks that are part of your algorithm. A single
hybrid job typically contains a collection of many quantum tasks.
Device
In Amazon Braket, a device is a backend that can run quantum tasks. A device can be a QPU or a
quantum circuit simulator. To learn more, see Amazon Braket supported devices (p. 8).
Gate-based quantum computing
In gate-based quantum computing (QC), also called circuit-based QC, computations are broken
down into elementary operations (gates). Certain sets of gates are universal, meaning that every
computation can be expressed as a finite sequence of those gates. Gates are the building blocks of
quantum circuits and are analogous to the logic gates of classical digital circuits.
Hamiltonian
The quantum dynamics of a physical system are determined by its Hamiltonian, which encodes all
information about the interactions between constituents of the system and the effects of exogenous
driving forces. The Hamiltonian of an N-qubit system is commonly represented as a 2
N
by 2
N
 matrix
of complex numbers on classical machines. By running an Analog Hamiltonian Simulation on a
quantum device, you can avoid these exponential resource requirements.
Pulse
A pulse is a transient physical signal transmitted to the qubits. It is described by a waveform played
in a frame that serves as a support for the carrier signal and is bound to the hardware channel or
port. Customers can design their own pulses by providing the analog envelope that modulates
the high-frequency sinusoidal carrier signal. The frame is uniquely described by a frequency and
a phase that are often chosen to be on resonance with the energy separation between the energy
levels for |0⟩ and |1⟩ of the qubit. Gates are thus enacted as pulses with a predetermined shape and
calibrated parameters such as its amplitude, frequency and duration. Use cases that are not covered
by template waveforms will be enabled via custom waveforms which will be specified at the single
sample resolution by providing a list of values separated by a fixed, physical cycle-time.
Quantum circuit
A quantum circuit is the instruction set that defines a computation on a gate-based quantum
computer. A quantum circuit is a sequence of quantum gates, which are reversible transformations
on a qubit register, together with measurement instructions.
Quantum circuit simulator
A quantum circuit simulator is a computer program that runs on classical computers and calculates
the measurement outcomes of a quantum circuit. For general circuits, the resource requirements of
a quantum simulation grow exponentially with the number of qubits to simulate. Braket provides
access to both managed (accessed through the Braket API) and local (part of the Amazon Braket
SDK) quantum circuit simulators.
Quantum computer
A quantum computer is a physical device that uses quantum-mechanical phenomena, such as
superposition and entanglement, to perform computations. There are different paradigms to
quantum computing (QC), such as gate-based QC.
Quantum processing unit (QPU)
A QPU is a physical quantum computing device that can run on a quantum task. QPUs can be based
on different QC paradigms, such as gate-based QC. To learn more, see Amazon Braket supported
devices (p. 8).
QPU native gates
QPU native gates can be directly mapped to control pulses by the QPU control system. Native gates
can be run on the QPU device without further compilation. Subset of QPU supported gates. You can
3
Amazon Braket Developer Guide
AWS terminology and tips for Amazon Braket
find the native gates of a device on the Devices page in the Amazon Braket console and through the
Braket SDK.
QPU supported gates
QPU supported gates are the gates accepted by the QPU device. These gates might not be able to
directly run on the QPU, meaning that they might need to be decomposed into native gates. You can
find the supported gates of a device on the Devices page in the Amazon Braket console and through
the Amazon Braket SDK.
Quantum task
In Braket, a quantum task is the atomic request to a device. For gate-based QC devices, this includes
the quantum circuit (including the measurement instructions and number of shots) and other
request metadata. You can create quantum tasks through the Amazon Braket SDK or by using the
CreateQuantumTask API operation directly. After you create a quantum task, it will be queued until
the requested device becomes available. You can view your quantum tasks on the Quantum Tasks
page of the Amazon Braket console or by using the GetQuantumTask or SearchQuantumTasks API
operations.
Qubit
The basic unit of information in a quantum computer is called a qubit (quantum bit), much like a
bit in classical computing. A qubit is a two-level quantum system that can be realized by different
physical implementations, such as superconducting circuits or individual ions and atoms. Other qubit
types are based on photons, electronic or nuclear spins, or more exotic quantum systems.
Queue depth
Queue depth refers to the number of quantum tasks and hybrid jobs queued for a particular device.
A device’s quantum task and hybrid job queue count are accessible through the Braket Software
Development Kit (SDK) or Amazon Braket Management Console.
1. Task queue depth refers to the total number of quantum tasks currently waiting to run in normal
priority.
2. Priority task queue depth refers to the total number of submitted quantum tasks waiting to run
through Amazon Braket Hybrid Jobs. These tasks get priority over standalone tasks once a hybrid
job starts.
3. Hybrid jobs queue depth refers to the total number of hybrid jobs currently queued on a device.
Quantum tasks submitted as part of a hybrid job have priority, and are aggregated in the Priority
Task Queue.
Queue position
Queue position refers to the current position of your quantum task or hybrid job within a respective
device queue. It can be obtained for quantum tasks or hybrid jobs through the Braket Software
Development Kit (SDK) or Amazon Braket Management Console.
Shots
Since quantum computing is inherently probabilistic, any circuit needs to be evaluated multiple
times to get an accurate result. A single circuit execution and measurement is called a shot. The
number of shots (repeated executions) for a circuit is chosen based on the desired accuracy for the
result.
AWS terminology and tips for Amazon Braket
IAM policies
An IAM policy is a document that allows or denies permissions to AWS services and resources. IAM
policies enable you to customize users' levels of access to resources. For example, you can allow
users access to all of the Amazon S3 buckets within your AWS account, or only a specific bucket.
4
Amazon Braket Developer Guide
AWS terminology and tips for Amazon Braket
• Best practice: Follow the security principle of least privilege when granting permissions. By
following this principle, you help to prevent users or roles from having more permissions than
needed to perform their quantum tasks. For example, if an employee needs access to only a
specific bucket, specify the bucket in the IAM policy instead of granting the employee access to all
of the buckets in your AWS account.
IAM roles
An IAM role is an identity that you can assume to gain temporary access to permissions. Before a
user, application, or service can assume an IAM role, they must be granted permissions to switch to
the role. When someone assumes an IAM role, they abandon all previous permissions that they had
under a previous role and assume the permissions of the new role.
• Best practice: IAM roles are ideal for situations in which access to services or resources needs to be
granted temporarily, instead of long-term.
Amazon S3 bucket
Amazon Simple Storage Service (Amazon S3) is an AWS service that lets you store data as objects
in buckets. Amazon S3 buckets offer unlimited storage space. The maximum size for an object in
an Amazon S3 bucket is 5 TB. You can upload any type of file data to an Amazon S3 bucket, such
as images, videos, text files, backup files, media files for a website, archived documents, and your
Braket quantum task results.
• Best practice: You can set permissions to control access to your S3 bucket. For more information,
see Bucket policies and user policies in the Amazon S3 documentation.
5
Amazon Braket Developer Guide
Amazon Braket quantum task flow
How Amazon Braket works
Amazon Braket provides on-demand access to quantum computing devices, including on-demand circuit
simulators and different types of QPUs. In Amazon Braket, the atomic request to a device is a quantum
task. For gate-based QC devices, this request includes the quantum circuit (including the measurement
instructions and number of shots) and other request metadata. For Analog Hamiltonian Simulators, the
quantum task contains the physical layout of the quantum register and the time- and space-dependence
of the manipulating fields.
In this section, we are going to learn about the high-level flow of running quantum tasks on Amazon
Braket.
Amazon Braket quantum task flow
With Jupyter notebooks, you can conveniently define, submit, and monitor your quantum tasks from the
Amazon Braket Console or using the Amazon Braket SDK. You can build your quantum circuits directly in
the SDK. However, for Analog Hamiltonian Simulators, you define the register layout and the controlling
fields. After your quantum task is defined, you can choose a device to run it on and submit it to the
Amazon Braket API (2). Depending on the device you chose, the quantum task is queued until the device
becomes available and the task is sent to the QPU or simulator for implementation (3). Amazon Braket
gives you access to different types of QPUs (IonQ, Oxford Quantum Circuits (OQC), QuEra, Rigetti), three
on-demand simulators (SV1, DM1, TN1), two local simulators, and one embedded simulator. To learn
more, see Amazon Braket supported devices (p. 8).
After processing your quantum task, Amazon Braket returns the results to an Amazon S3 bucket,
where the data is stored in your AWS account (4). At the same time, the SDK polls for the results in the
background and loads them into the Jupyter notebook at quantum task completion. You can also view
and manage your quantum tasks on the Quantum Tasks page in the Amazon Braket console or by using
the GetQuantumTask operation of the Amazon Braket API.
6
Amazon Braket Developer Guide
Third-party data processing
Amazon Braket is integrated with AWS Identity and Access Management (IAM), Amazon CloudWatch,
AWS CloudTrail and Amazon EventBridge for user access management, monitoring and logging as well as
for event based processing (5).
Third-party data processing
Quantum tasks that are submitted to a QPU device are processed on quantum computers located in
facilities operated by third party providers. To learn more about security and third-party processing in
Amazon Braket, see Security of Amazon Braket Hardware Providers (p. 188).
Core repositories and plugins for Braket
Core repositories
The following displays a list of core repositories that contain key packages that are used for Braket:
• Braket Python SDK - Use the Braket Python SDK to set up your code on Jupyter notebooks in the
Python programming language. After your Jupyter notebooks are set up, you can run your code on
Braket devices and simulators
• Braket Schemas - The contract between the Braket SDK and the Braket service.
• Braket Default Simulator - All our local quantum simulators for Braket (state vector and density
matrix).
Plugins
Then there are the various plugins that are used along with various devices and programming tools.
These include Braket supported plugins as well as plugins that are supported by third parties as shown
below.
Amazon Braket supported:
• Amazon Braket algorithm library - A catalog of pre-built quantum algorithms written in Python. Run
them as they are or use them as a starting point to build more complex algorithms.
• Braket-PennyLane plugin - Use PennyLane as the QML framework on Braket.
Third-party (Braket team monitors and contributes):
• Qiskit-Braket provider - Use the Qiskit SDK to access Braket resources.
• Braket-Julia SDK - (EXPERIMENTAL) A Julia native version of the Braket SDK
7
Amazon Braket Developer Guide
Amazon Braket supported devices
In Amazon Braket, a device represents a QPU or simulator that you can call to run quantum tasks.
Amazon Braket provides access to QPU devices from IonQ, Oxford Quantum Circuits, QuEra, and Rigetti,
three on-demand simulators, three local simulators, and one embedded simulator. For all devices, you
can find further device properties, such as device topology, calibration data, and native gate sets, on
the Devices tab of the Amazon Braket console or by means of the GetDevice API. When constructing a
circuit with the simulators, Amazon Braket currently requires that you use contiguous qubits or indices.
If you are working with the Amazon Braket SDK, you have access to device properties as shown in the
following code example.
from braket.aws import AwsDevice
from braket.devices import LocalSimulator
device = AwsDevice('arn:aws:braket:::device/quantum-simulator/amazon/sv1')
 #SV1
# device = LocalSimulator()
 #Local State Vector Simulator
# device = LocalSimulator("default")
 #Local State Vector Simulator
# device = LocalSimulator(backend="default")
 #Local State Vector Simulator
# device = LocalSimulator(backend="braket_sv")
 #Local State Vector Simulator
# device = LocalSimulator(backend="braket_dm")
 #Local Density Matrix Simulator
# device = LocalSimulator(backend="braket_ahs")
 #Local Analog Hamiltonian Simulation
# device = AwsDevice('arn:aws:braket:::device/quantum-simulator/amazon/tn1')
 #TN1
# device = AwsDevice('arn:aws:braket:::device/quantum-simulator/amazon/dm1')
 #DM1
# device = AwsDevice('arn:aws:braket:us-east-1::device/qpu/ionq/Harmony')
 #IonQ
# device = AwsDevice('arn:aws:braket:us-east-1::device/qpu/ionq/Aria-1')
 #IonQ
# device = AwsDevice('arn:aws:braket:us-east-1::device/qpu/ionq/Aria-2')
 #IonQ
# device = AwsDevice('arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3')
 #Rigetti Aspen-M-3
# device = AwsDevice('arn:aws:braket:eu-west-2::device/qpu/oqc/Lucy')
 #OQC Lucy
# device = AwsDevice('arn:aws:braket:us-east-1::device/qpu/quera/Aquila')
 #QuEra Aquila
# get device properties
device.properties
Supported quantum hardware providers
• IonQ (p. 10)
• Oxford Quantum Circuits (OQC) (p. 11)
• QuEra Computing (p. 11)
• Rigetti (p. 10)
Supported simulators
8
Amazon Braket Developer Guide
• Local state vector simulator (braket_sv) ('Default Simulator') (p. 12)
• Local density matrix simulator (braket_dm) (p. 12)
• Local AHS simulator (p. 12)
• State vector simulator (SV1) (p. 13)
• Density matrix simulator (DM1) (p. 13)
• Tensor network simulator (TN1) (p. 14)
• PennyLane’s Lightning Simulators (p. 15)
Choose the best simulator for your quantum task
• Compare simulators (p. 15)
Note
To view the available AWS Regions for each device, scroll right across the following table.
Amazon Braket devices
Provider Device Name Paradigm Type Device ARN Region
IonQ Aria 1 gatebased
QPU arn:aws:braket:useast-1::device/qpu/
ionq/Aria-1
us-east-1
IonQ Aria 2 gatebased
QPU arn:aws:braket:useast-1::device/qpu/
ionq/Aria-2
us-east-1
IonQ Harmony gatebased
QPU arn:aws:braket:useast-1::device/qpu/
ionq/Harmony
us-east-1
Oxford
Quantum
Circuits
Lucy gatebased
QPU arn:aws:braket:euwest-2::device/qpu/
oqc/Lucy
eu-west-2
QuEra Aquila Analog
Hamiltonian
Simulation
QPU arn:aws:braket:useast-1::device/qpu/
quera/Aquila
us-east-1
Rigetti Aspen M-3 gatebased
QPU arn:aws:braket:uswest-1::device/qpu/
rigetti/Aspen-M-3
us-west-1
AWS braket_sv gatebased
Local
simulator
N/A (local simulator in
Braket SDK)
N/A
AWS braket_dm gatebased
Local
simulator
N/A (local simulator in
Braket SDK)
N/A
AWS SV1 gatebased
Ondemand
simulator
arn:aws:braket:::device/
quantum-simulator/
amazon/sv1
All
Regions
where
Amazon
Braket is
available.
9
Amazon Braket Developer Guide
IonQ
Provider Device Name Paradigm Type Device ARN Region
AWS DM1 gatebased
Ondemand
simulator
arn:aws:braket:::device/
quantum-simulator/
amazon/dm1
All
Regions
where
Amazon
Braket is
available.
AWS TN1 gatebased
Ondemand
simulator
arn:aws:braket:::device/
quantum-simulator/
amazon/tn1
us-west-2,
us-east-1,
and euwest-2
To view additional details about the QPUs you can use with Amazon Braket, see Amazon Braket
Hardware Providers.
IonQ
IonQ offers gate-based QPUs based on ion trap technology. IonQ’s trapped ion QPUs are built on a chain
of trapped 171Yb+ ions that are spatially confined by means of a microfabricated surface electrode trap
within a vacuum chamber.
IonQ devices support the following quantum gates.
'x', 'y', 'z', 'rx', 'ry', 'rz', 'h', 'cnot', 's', 'si', 't', 'ti', 'v', 'vi', 'xx', 'yy',
 'zz', 'swap'
With verbatim compilation, the IonQ QPUs support the following native gates.
'gpi', 'gpi2', 'ms'
If you only specify two phase parameters when using the native MS gate, a fully- entangling MS gate
runs. A fully-entangling MS gate always performs a π/2 rotation. To specify a different angle and run
a partially-entangling MS gate, you specify the desired angle by adding a third parameter. For more
information, see the braket.circuits.gate module.
These native gates can only be used with verbatim compilation. To learn more about verbatim
compilation, see Verbatim Compilation.
Rigetti
Rigetti quantum processors are universal, gate-model machines based on all-tunable superconducting
qubits. The 79-qubit Aspen-M-3 device leverages their proprietary multi-chip technology and is
assembled from 2 40-qubit processors.
The Rigetti device supports the following quantum gates.
'cz', 'xy', 'ccnot', 'cnot', 'cphaseshift', 'cphaseshift00', 'cphaseshift01',
 'cphaseshift10', 'cswap', 'h', 'i', 'iswap', 'phaseshift', 'pswap', 'rx', 'ry', 'rz', 's',
 'si', 'swap', 't', 'ti', 'x', 'y', 'z'
10
Amazon Braket Developer Guide
Oxford Quantum Circuits (OQC)
With verbatim compilation, the Rigetti devices support the following native gates.
'rx', 'rz', 'cz', 'cphaseshift', 'xy'
Rigetti superconducting quantum processors can run the 'rx' gate with only the angles of ±π/2 or ±π.
Pulse-level control is available on the Rigetti devices, which support a set of predefined frames of the
following types:
'rf', 'rf_f12', 'ro_rx', 'ro_rx', 'cz', 'cphase', 'xy'
For more information about these frames, see Roles of frames and ports (p. 117).
Oxford Quantum Circuits (OQC)
OQC quantum processors are universal, gate-model machines, built using scalable Coaxmon technology.
The OQC Lucy system is an 8-qubit device with the topology of a ring in which each qubit is connected to
its two nearest neighbors.
The Lucy device supports the following quantum gates.
'ccnot', 'cnot', 'cphaseshift', 'cswap', 'cy', 'cz', 'h', 'i', 'phaseshift', 'rx', 'ry',
 'rz', 's', 'si', 'swap', 't', 'ti', 'v', 'vi', 'x', 'y', 'z', 'ecr'
With verbatim compilation, the OQC device supports the following native gates.
'i', 'rz', 'v', 'x', 'ecr'
Pulse-level control is available on the OQC devices. The OQC devices support a set of predefined frames
of the following types:
'drive', 'second_state', 'measure', 'acquire', 'cross_resonance',
 'cross_resonance_cancellation'
OQC devices support dynamic declaration of frames provided that you supply a valid port identifier. For
more information about these frames and ports, see Roles of frames and ports (p. 117).
Note
When using pulse control with OQC, the length of your programs cannot exceed a maximum
of 90 microseconds. The maximum duration is approximately 50 nanoseconds for single-qubit
gates and 1 microsecond for two-qubit gates. These numbers may vary depending on the qubits
used, the device’s current calibration, and the circuit compilation.
QuEra
QuEra offers neutral-atom based devices that can run Analog Hamiltonian Simulation (AHS) quantum
tasks. These special-purpose devices faithfully reproduce the time-dependent quantum dynamics of
hundreds of simultaneously interacting qubits.
One can program these devices in the paradigm of Analog Hamiltonian Simulation by prescribing
the layout of the qubit register and the temporal and spatial dependence of the manipulating fields.
Amazon Braket provides utilities to construct such programs via the AHS module of the python SDK,
braket.ahs.
11
Amazon Braket Developer Guide
Local state vector simulator (braket_sv)
For more information, see the Analog Hamiltonian Simulation example notebooks or the Submit an
analog program using QuEra’s Aquila (p. 92) page.
Local state vector simulator (braket_sv)
The local state vector simulator (braket_sv) is part of the Amazon Braket SDK that runs locally in your
environment. It is well-suited for rapid prototyping on small circuits (up to 25 qubits) depending on the
hardware specifications of your Braket notebook instance or your local environment.
The local simulator supports all gates in the Amazon Braket SDK, but QPU devices support a smaller
subset. You can find the supported gates of a device in the device properties.
Note
The local simulator supports advanced OpenQASM features which may not be supported on
QPU devices or other simulators. For more information on supported features, see the examples
provided in the OpenQASM Local Simulator notebook.
For more information about how to work with simulators, see the Amazon Braket examples.
Local density matrix simulator (braket_dm)
The local density matrix simulator (braket_dm) is part of the Amazon Braket SDK that runs locally in
your environment. It is well-suited for rapid prototyping on small circuits with noise (up to 12 qubits)
depending on the hardware specifications of your Braket notebook instance or your local environment.
You can build common noisy circuits from the ground up using gate noise operations such as bit-flip and
depolarizing error. You can also apply noise operations to specific qubits and gates of existing circuits
that are intended to run both with and without noise.
The braket_dm local simulator can provide the following results, given the specified number of shots:
• Reduced density matrix: Shots = 0
Note
The local simulator supports advanced OpenQASM features, which may not be supported
on QPU devices or other simulators. For more information about supported features, see the
examples provided in the OpenQASM Local Simulator notebook.
To learn more about the local density matrix simulator, see the Braket introductory noise simulator
example.
Local AHS simulator (braket_ahs)
The local AHS (Analog Hamiltonian Simulation) simulator (braket_ahs) is part of the Amazon Braket
SDK that runs locally in your environment. It can be used to simulate results from an AHS program.
It is well-suited for prototyping on small registers (up to 10-12 atoms) depending on the hardware
specifications of your Braket notebook instance or your local environment.
The local simulator supports AHS programs with one uniform driving field, one (non-uniform) shifting
field, and arbitrary atom arrangements. For details, please refer to the Braket AHS class and the Braket
AHS program schema.
12
Amazon Braket Developer Guide
State vector simulator (SV1)
To learn more about the local AHS simulator, see the Hello AHS: Run your first Analog Hamiltonian
Simulation (p. 42) page and the Analog Hamiltonian Simulation example notebooks.
State vector simulator (SV1)
SV1 is an on-demand, high-performance, universal state vector simulator. It can simulate circuits of up to
34 qubits. You can expect a 34-qubit, dense, and square circuit (circuit depth = 34) to take approximately
1–2 hours to complete, depending on the type of gates used and other factors. Circuits with all-toall gates are well suited for SV1. It returns results in forms such as a full state vector or an array of
amplitudes.
SV1 has a maximum runtime of 6 hours. It has a default of 35 concurrent quantum tasks, and a
maximum of 100 (50 in us-west-1 and eu-west-2) concurrent quantum tasks.
SV1 results
SV1 can provide the following results, given the specified number of shots:
• Sample: Shots > 0
• Expectation: Shots >= 0
• Variance: Shots >= 0
• Probability: Shots > 0
• Amplitude: Shots = 0
• Adjoint Gradient: Shots = 0
For more about results, see Result types.
SV1 is always available, it runs your circuits on demand, and it can run multiple circuits in parallel. The
runtime scales linearly with the number of operations and exponentially with the number of qubits. The
number of shots has a small impact on the runtime. To learn more, visit Compare simulators.
Simulators support all gates in the Braket SDK, but QPU devices support a smaller subset. You can find
the supported gates of a device in the device properties.
Density matrix simulator (DM1)
DM1 is an on-demand, high-performance, density matrix simulator. It can simulate circuits of up to 17
qubits.
DM1 has a maximum runtime of 6 hours, a default of 35 concurrent quantum tasks, and a maximum of
50 concurrent quantum tasks.
DM1 results
DM1 can provide the following results, given the specified number of shots:
• Sample: Shots > 0
• Expectation: Shots >= 0
• Variance: Shots >= 0
• Probability: Shots > 0
• Reduced density matrix: Shots = 0, up to max 8 qubits
13
Amazon Braket Developer Guide
Tensor network simulator (TN1)
For more information about results, see Result types.
DM1 is always available, it runs your circuits on demand, and it can run multiple circuits in parallel. The
runtime scales linearly with the number of operations and exponentially with the number of qubits. The
number of shots has a small impact on the runtime. To learn more, see Compare simulators.
Noise gates and limitations
AmplitudeDamping
 Probability has to be within [0,1]
BitFlip
 Probability has to be within [0,0.5]
Depolarizing
 Probability has to be within [0,0.75]
GeneralizedAmplitudeDamping
 Probability has to be within [0,1]
PauliChannel
 The sum of the probabilities has to be within [0,1]
Kraus
 At most 2 qubits
 At most 4 (16) Kraus matrices for 1 (2) qubit
PhaseDamping
 Probability has to be within [0,1]
PhaseFlip
 Probability has to be within [0,0.5]
TwoQubitDephasing
 Probability has to be within [0,0.75]
TwoQubitDepolarizing
 Probability has to be within [0,0.9375]
Tensor network simulator (TN1)
TN1 is an on-demand, high-performance, tensor network simulator. TN1 can simulate certain circuit
types with up to 50 qubits and a circuit depth of 1,000 or smaller. TN1 is particularly powerful for sparse
circuits, circuits with local gates, and other circuits with special structure, such as quantum Fourier
transform (QFT) circuits. TN1 operates in two phases. First, the rehearsal phase attempts to identify an
efficient computational path for your circuit, so TN1 can estimate the runtime of the next stage, which is
called the contraction phase. If the estimated contraction time exceeds the TN1 simulation runtime limit,
TN1 does not attempt contraction.
TN1 has a runtime limit of 6 hours. It is limited to a maximum of 10 (5 in eu-west-2) concurrent quantum
tasks.
TN1 results
The contraction phase consists of a series of matrix multiplications. The series of multiplications
continues until a result is reached or until it is determined that a result cannot be reached.
Note: Shots must be > 0.
Result types include:
• Sample
• Expectation
• Variance
For more about results, see Result types.
14
Amazon Braket Developer Guide
Embedded simulators
TN1 is always available, it runs your circuits on demand, and it can run multiple circuits in parallel. To
learn more, see Compare simulators.
Simulators support all gates in the Braket SDK, but QPU devices support a smaller subset. You can find
the supported gates of a device in the device properties.
Visit the Amazon Braket GitHub repository for a TN1 example notebook to help you get started with
TN1.
Best practices for working with TN1
• Avoid all-to-all circuits.
• Test a new circuit or class of circuits with a small number of shots, to learn the circuit’s "hardness" for
TN1.
• Split large shot simulations over multiple quantum tasks.
Embedded simulators
Embedded simulators work by having the simulation embedded with the algorithm code in the same
container and executing the simulation on the hybrid job instance directly. This can be useful for
removing bottlenecks associated with having the simulation communicate with a remote device. This
can result in significantly lower memory usage, reduced number of circuit executions to achieve a desired
result, and an improved performance of ten times or more. For more information about embedded
simulators, see the Run a hybrid job with Amazon Braket Hybrid Jobs page.
PennyLane’s lightning simulators
You can use PennyLane’s lightning simulators as embedded simulators on Braket. With PennyLane’s
lightning simulators, you can leverage advanced gradient computation methods, such as adjoint
differentiation, to evaluate gradients faster. The lightning.qubit simulator is available as a device via
Braket NBIs and as an embedded simulator, whereas the lightning.gpu simulator needs to be run as an
embedded simulator with a GPU instance. See the Embedded simulators in Braket Hybrid Jobs notebook
for an example of using lightning.gpu.
Compare simulators
This section helps you select the Amazon Braket simulator that’s best suited for your quantum task, by
describing some concepts, limitations, and use cases.
Choosing between local simulators and on-demand simulators (SV1, TN1, DM1)
The performance of local simulators depends on the hardware that hosts the local environment, such
as a Braket notebook instance, used to run your simulator. On-demand simulators run in the AWS cloud
and are designed to scale beyond typical local environments. On-demand simulators are optimized for
larger circuits, but add some latency overhead per quantum task or batch of quantum tasks. This can
imply a trade-off if many quantum tasks are involved. Given these general performance characteristics,
the following guidance can help you choose how to run simulations, including ones with noise.
For simulations:
• When employing fewer than 18 qubits, use a local simulator.
• When employing 18–24 qubits, choose a simulator based on the workload.
• When employing more than 24 qubits, use an on-demand simulator.
15
Amazon Braket Developer Guide
Compare simulators
For noise simulations:
• When employing fewer than 9 qubits, use a local simulator.
• When employing 9–12 qubits, choose a simulator based on the workload.
• When employing more than 12 qubits, use DM1.
What is a state vector simulator?
SV1 is a universal state vector simulator. It stores the full wave function of the quantum state and
sequentially applies gate operations to the state. It stores all possibilities, even the extremely unlikely
ones. The SV1 simulator’s run time for a quantum task increases linearly with the number of gates in the
circuit.
What is a density matrix simulator?
DM1 simulates quantum circuits with noise. It stores the full density matrix of the system and
sequentially applies the gates and noise operations of the circuit. The final density matrix contains
complete information about the quantum state after the circuit runs. The runtime generally scales
linearly with the number of operations and exponentially with the number of qubits.
What is a tensor network simulator?
TN1 encodes quantum circuits into a structured graph.
• The nodes of the graph consist of quantum gates, or qubits.
• The edges of the graph represent connections between gates.
As a result of this structure, TN1 can find simulated solutions for relatively large and complex quantum
circuits.
TN1 requires two phases
Typically, TN1 operates in a two-phase approach to simulating quantum computation.
• The rehearsal phase: In this phase, TN1 comes up with a way to traverse the graph in an efficient
manner, which involves visiting every node so that you can obtain the measurement you desire. As a
customer, you do not see this phase because TN1 performs both phases together for you. It completes
the first phase and determines whether to perform the second phase on its own based on practical
constraints. You have no input into that decision after the simulation has begun.
• The contraction phase: This phase is analogous to the execution phase of a computation in a classical
computer. The phase consists of a series of matrix multiplications. The order of these multiplications
has a great effect on the difficulty of the computation. Therefore, the rehearsal phase is accomplished
first in order to find the most effective computation paths across the graph. After it finds the
contraction path during the rehearsal phase, TN1 contracts together the gates of your circuit to
produce the results of the simulation.
TN1 graphs are analogous to a map
Metaphorically, you can compare the underlying TN1 graph to the streets of a city. In a city with a
planned grid, it is easy to find a route to your destination using a map. In a city with unplanned streets,
duplicate street names, and so forth, it can be difficult to find a route to your destination by looking at a
map.
If TN1 did not perform the rehearsal phase, it would be like walking around the streets of the city to find
your destination, instead of looking at a map first. It can really pay off in terms of walking time to spend
more time looking at the map. Similarly, the rehearsal phase provides valuable information.
16
Amazon Braket Developer Guide
Compare simulators
You might say that the TN1 has a certain “awareness” of the structure of the underlying circuit that it
traverses. It gains this awareness during the rehearsal phase.
Types of problems best suited for each of these types of simulators
SV1 is well-suited for any class of problems that rely primarily on having a certain number of qubits and
gates. Generally, the time required grows linearly with the number of gates, while it does not depend on
the number of shots. SV1 is generally faster than TN1 for circuits under 28 qubits.
SV1 can be slower for higher qubit numbers because it actually simulates all possibilities, even the
extremely unlikely ones. It has no way to determine which outcomes are likely. Thus, for a 30-qubit
evaluation, SV1 must calculate 2^30 configurations. The limit of 34 qubits for the Amazon Braket SV1
simulator is a practical constraint due to memory and storage limitations. You can think of it like this:
Each time you add a qubit to SV1, the problem becomes twice as hard.
For many classes of problems, TN1 can evaluate much larger circuits in realistic time than SV1 because
TN1 takes advantage of the structure of the graph. It essentially tracks the evolution of solutions from its
starting place and it retains only the configurations that contribute to an efficient traversal. Put another
way, it saves the configurations to create an ordering of matrix multiplication that results in a simpler
evaluation process.
For TN1, the number of qubits and gates matters, but the structure of the graph matters a lot more.
For example, TN1 is very good at evaluating circuits (graphs) in which the gates are short-range (that is,
each qubit is connected by gates only to its nearest neighbour qubits), and circuits (graphs) in which the
connections (or gates) have similar range. A typical range for TN1 is having each qubit talk only to other
qubits that are 5 qubits away. If most of the structure can be decomposed into simpler relationships
such as these, which can be represented in more, smaller, or more uniform matrices, TN1 performs the
evaluation easily.
Limitations of TN1
TN1 can be slower than SV1 depending on the graph’s structural complexity. For certain graphs, TN1
terminates the simulation after the rehearsal stage, and shows a status of FAILED, for either of these
two reasons:
• Cannot find a path — If the graph is too complex, it is too difficult to find a good traversal path and
the simulator gives up on the computation. TN1 cannot perform the contraction. You may see an error
message similar to this one: No viable contraction path found.
• Contraction stage is too difficult — In some graphs, TN1 can find a traversal path, but it is very long
and extremely time-consuming to evaluate. In this case, the contraction is so expensive that the cost
would be prohibitive and instead, TN1 exits after the rehearsal phase. You may see an error message
similar to this one: Predicted runtime based on best contraction path found exceeds
TN1 limit.
Note
You are billed for the rehearsal stage of TN1 even if contraction is not performed and you see a
FAILED status.
The predicted runtime also depends on the shot count. In worst-case scenarios, TN1 contraction time
depends linearly on the shot count. The circuit may be contractable with fewer shots. For example, you
might submit a quantum task with 100 shots, which TN1 decides is uncontractable, but if you resubmit
with only 10, the contraction proceeds. In this situation, to attain 100 samples, you could submit 10
quantum tasks of 10 shots for the same circuit and combine the results in the end.
As a best practice, we recommend that you always test your circuit or circuit class with a few shots (for
example, 10) to find out how hard your circuit is for TN1, before you proceed with a higher number of
shots.
17
Amazon Braket Developer Guide
Compare simulators
Note
The series of multiplications that forms the contraction phase begins with small, NxN matrices.
For example, a 2-qubit gate requires a 4x4 matrix. The intermediate matrices required during a
contraction that is adjudged to be too difficult are gigantic. Such a computation would require
days to complete. That’s why Amazon Braket does not attempt extremely complex contractions.
Concurrency
All Braket simulators give you the ability to run multiple circuits concurrently. Concurrency limits vary by
simulator and region. For more information on concurrency limits, see the Quotas page.
18
Amazon Braket Developer Guide
Amazon Braket Regions and
endpoints
Amazon Braket is available in the following AWS Regions:
Region availability of Amazon Braket
Region Name Region Braket Endpoint QPU
US East (N. Virginia) us-east-1 braket.useast-1.amazonaws.com
IonQ
US East (N. Virginia) us-east-1 braket.useast-1.amazonaws.com
QuEra
US West (N. California) us-west-1 braket.uswest-1.amazonaws.com
Rigetti
EU West 2 (London) eu-west-2 braket.euwest-2.amazonaws.com
OQC
You can run Amazon Braket from any Region in which it is available, but each QPU is available only in a
single Region. Quantum tasks that run on a QPU device can be viewed in the Amazon Braket console in
the Region of that device. If you are using the Amazon Braket SDK, you can submit quantum tasks to any
QPU device, regardless of the Region in which you are working. The SDK automatically creates a session
to the Region for the QPU specified.
For general information about how AWS works with Regions and endpoints, see AWS service endpoints
in the AWS General Reference.
19
Amazon Braket Developer Guide
Near real-time cost tracking
Amazon Braket pricing
With Amazon Braket, you have access to quantum computing resources on demand without upfront
commitment. You pay only for what you use. To learn more about pricing, please visit our pricing page.
Near real-time cost tracking
The Braket SDK offers you the option to add a near real-time cost tracking to your quantum workloads.
Each of our example notebooks includes cost tracking code to provide you with a maximum cost
estimate on Braket’s quantum processing units (QPUs) and on-demand simulators. Maximum cost
estimates will be shown in USD and are not inclusive of any credits or discounts.
Note
Charges shown are estimates based on your Amazon Braket simulator and quantum processing
unit (QPU) task usage. Estimated charges shown may differ from your actual charges. Estimated
charges do not factor in any discounts or credits and you may experience additional charges
based on your use of other services such as Amazon Elastic Compute Cloud (Amazon EC2).
Cost tracking for SV1
In order to demonstrate how the cost tracking function can be used, we will be constructing a Bell State
circuit and running it on our SV1 simulator. Begin by importing the Braket SDK modules, defining a Bell
State and adding the Tracker() function to our circuit:
#import any required modules
from braket.aws import AwsDevice
from braket.circuits import Circuit
from braket.tracking import Tracker
#create our bell circuit
circ = Circuit().h(0).cnot(0,1)
device = AwsDevice("arn:aws:braket:::device/quantum-simulator/amazon/sv1")
with Tracker() as tracker:
task = device.run(circ, shots=1000).result()
#Your results
print(task.measurement_counts)
When you run your Notebook, you can expect the following output for your Bell State simulation. The
tracker function will show you the number of shots sent, quantum tasks completed, the execution
duration, the billed execution duration, and your maximum cost in USD. Your execution time may vary
for each simulation.
tracker.quantum_tasks_statistics()
 {'arn:aws:braket:::device/quantum-simulator/amazon/sv1':
 {'shots': 1000,
 'tasks': {'COMPLETED': 1},
 'execution_duration': datetime.timedelta(microseconds=4000),
 'billed_execution_duration': datetime.timedelta(seconds=3)}}
tracker.simulator_tasks_cost()
$0.00375
20
Amazon Braket Developer Guide
Best practices for cost savings
Using the cost tracker to set maximum costs
You can use the cost tracker to set maximum costs on a program. You may have a maximum threshold
for how much you want to spend on a given program. In this way, you can use the cost tracker to build
out cost control logic in your execution code. The following example takes the same circuit on a Rigetti
QPU and limits the cost to 1 USD. The cost to run one iteration of the circuit in our code is 0.37 USD. We
have set the logic to repeat the iterations until the total cost exceeds 1 USD; hence, the code snippet will
run three times until the next iteration exceeds 1 USD. Generally, a program would continue to iterate
until it reaches your desired maximum cost, in this case - three iterations.
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
with Tracker() as tracker:
while tracker.qpu_tasks_cost() < 1:
result = device.run(circ, shots=200).result()
print(tracker.quantum_tasks_statistics())
print(tracker.qpu_tasks_cost(), "USD")
{'arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3': {'shots': 600, 'tasks':
 {'COMPLETED': 3}}}
1.11 USD
Note
The cost tracker will not track duration for failed TN1 quantum tasks. During a TN1 simulation,
if your rehearsal completes, but the contraction step fails, your rehearsal charge will not be
shown in the cost tracker.
Best practices for cost savings
Consider the following best practices for using Amazon Braket. Save time, minimize costs, and avoid
common errors.
Verify with simulators
• Verify your circuits using a simulator before you run it on a QPU, so you can fine-tune your circuit
without incurring charges for QPU usage.
• Although the results from running the circuit on a simulator may not be identical to the results from
running the circuit on a QPU, you can identify coding errors or configuration issues using a simulator.
Restrict user access to certain devices
• You can set up restrictions that keep unauthorized users from submitting quantum tasks on certain
devices. The recommended method for restricting access is with AWS IAM. For more information about
how to do that, see Restrict access.
• We recommend that you do not use your admin account as a way to give or restrict user access to
Amazon Braket devices.
Set billing alarms
• You can set a billing alarm to notify you when your bill reaches a preset limit. The recommended way
to set up an alarm is through AWS Budgets. You can set custom budgets and receive alerts when your
costs or usage may exceed your budgeted amount. Information is available at AWS Budgets.
Test TN1 quantum tasks with low shot counts
21
Amazon Braket Developer Guide
Best practices for cost savings
• Simulators cost less than QHPs, but certain simulators can be expensive if quantum tasks are run with
high shot counts. We recommend that you test your TN1 tasks with a low shot count. Shot count does
not affect the cost for SV1 and local simulator tasks.
Check all Regions for quantum tasks
• The console displays quantum tasks only for your current AWS Region. When looking for billable
quantum tasks that have been submitted, be sure to check all Regions.
• You can view a list of devices and their associated Regions on the Supported Devices (p. 8)
documentation page.
22
Amazon Braket Developer Guide
Amazon Braket Quotas
The following table lists the service quotas for Amazon Braket. Service quotas, also referred to as limits,
are the maximum number of service resources or operations for your AWS account.
Some quotas can be increased. For more information, see AWS service quotas.
• Burst rate quotas cannot be increased.
• The maximum rate increase for adjustable quotas (except burst rate, which cannot be adjusted) is 2X
the specified default rate limit. For example, a default quota of 60 can be adjusted to a maximum of
120.
• The adjustable quota for concurrent SV1 (DM1) quantum tasks allows a maximum of 60 per AWS
Region.
Resource Description Limit Adjustable
Rate of API requests The maximum number
of requests per second
that you can send in
this account in the
current Region.
140 Yes
Burst rate of API
requests
The maximum number
of additional requests
per second (RPS) that
you can send in one
burst in this account in
the current Region.
600 No
Rate of
CreateQuantumTask
requests
The maximum
number of
CreateQuantumTask
requests you can send
per second in this
account per Region.
20 Yes
Burst rate of
CreateQuantumTask
requests
The maximum
number of additional
CreateQuantumTask
requests per second
(RPS) that you can send
in one burst in this
account in the current
Region.
40 No
Rate of
SearchQuantumTasks
requests
The maximum
number of
SearchQuantumTasks
requests you can send
per second in this
account per Region.
5 Yes
23
Amazon Braket Developer Guide
Resource Description Limit Adjustable
Burst rate of
SearchQuantumTasks
requests
The maximum
number of additional
SearchQuantumTasks
requests per second
(RPS) that you can send
in one burst in this
account in the current
Region.
50 No
Rate of
GetQuantumTask
requests
The maximum number
of GetQuantumTask
requests you can send
per second in this
account per Region.
100 Yes
Burst rate of
GetQuantumTask
requests
The maximum
number of additional
GetQuantumTask
requests per second
(RPS) that you can send
in one burst in this
account in the current
Region.
500 No
Rate of
CancelQuantumTask
requests
The maximum
number of
CancelQuantumTask
requests you can send
per second in this
account per Region.
2 Yes
Burst rate of
CancelQuantumTask
requests
The maximum
number of additional
CancelQuantumTask
requests per second
(RPS) that you can send
in one burst in this
account in the current
Region.
20 No
Rate of GetDevice
requests
The maximum number
of GetDevice requests
you can send per
second in this account
per Region.
5 Yes
Burst rate of
GetDevice requests
The maximum
number of additional
GetDevice requests
per second (RPS) that
you can send in one
burst in this account in
the current Region.
50 No
24
Amazon Braket Developer Guide
Resource Description Limit Adjustable
Rate of
SearchDevices
requests
The maximum number
of SearchDevices
requests you can send
per second in this
account per Region.
5 Yes
Burst rate of
SearchDevices
requests
The maximum
number of additional
SearchDevices
requests per second
(RPS) that you can send
in one burst in this
account in the current
Region.
50 No
Rate of CreateJob
requests
The maximum number
of CreateJob requests
you can send per
second in this account
per Region.
1 Yes
Burst rate of
CreateJob requests
The maximum
number of additional
CreateJob requests
per second (RPS) that
you can send in one
burst in this account in
the current Region.
5 No
Rate of SearchJob
requests
The maximum number
of SearchJob requests
you can send per
second in this account
per Region.
5 Yes
Burst rate of
SearchJob requests
The maximum
number of additional
SearchJob requests
per second (RPS) that
you can send in one
burst in this account in
the current Region.
50 No
Rate of GetJob
requests
The maximum number
of GetJob requests you
can send per second in
this account per Region.
5 Yes
Burst rate of GetJob
requests
The maximum number
of additional GetJob
requests per second
(RPS) that you can send
in one burst in this
account in the current
Region.
25 No
25
Amazon Braket Developer Guide
Resource Description Limit Adjustable
Rate of CancelJob
requests
The maximum number
of CancelJob requests
you can send per
second in this account
per Region.
2 Yes
Burst rate of
CancelJob requests
The maximum
number of additional
CancelJob requests
per second (RPS) that
you can send in one
burst in this account in
the current Region.
5 No
Number of concurrent
SV1 quantum tasks
The maximum number
of concurrent quantum
tasks running on the
state vector simulator
(SV1) in the current
Region.
100 (50 in us-west-1
and eu-west-2)
No
Number of concurrent
DM1 quantum tasks
The maximum number
of concurrent quantum
tasks running on
the density matrix
simulator (DM1) in the
current Region.
100 (50 in us-west-1
and eu-west-2)
No
Number of concurrent
TN1 quantum tasks
The maximum number
of concurrent quantum
tasks running on
the tensor network
simulator (TN1) in the
current Region.
10 (5 in eu-west-2) Yes
Number of concurrent
hybrid jobs
The maximum number
of concurrent hybrid
jobs in the current
Region.
5 Yes
Hybrid jobs runtime
limit
The maximum amount
of time in days that a
hybrid job can run.
5 No
The following are the default classical compute instance quotas for Hybrid Jobs. If you wish to raise
these quotas, please contact AWS Support.
Resource Description Limits Adjustable
Maximum number
of instances of
ml.c4.xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c4.xlarge allowed
for all Amazon Braket
5 Yes
26
Amazon Braket Developer Guide
Resource Description Limits Adjustable
Hybrid Jobs in this
account and region.
Maximum number
of instances of
ml.c4.2xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c4.2xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.c4.4xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c4.4xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.c4.8xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c4.8xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.c5.xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c5.xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.c5.2xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c5.2xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.c5.4xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c5.4xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
1 Yes
Maximum number
of instances of
ml.c5.9xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c5.9xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
1 Yes
27
Amazon Braket Developer Guide
Resource Description Limits Adjustable
Maximum number
of instances of
ml.c5.18xlarge for
hybrid jobs
The maximum number
of instances of type
ml.c5.18xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.c5n.xlarge for hybrid
jobs
The maximum number
of instances of type
ml.c5n.xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.c5n.2xlarge for
hybrid jobs
The maximum number
of instances of type
ml.c5n.2xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.c5n.4xlarge for
hybrid jobs
The maximum number
of instances of type
ml.c5n.4xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.c5n.9xlarge for
hybrid jobs
The maximum number
of instances of type
ml.c5n.9xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.c5n.18xlarge for
hybrid jobs
The maximum number
of instances of type
ml.c5n.18xlarge
allowed for all Amazon
Braket Hybrid Jobs in
this account and region.
0 Yes
Maximum number
of instances of
ml.g4dn.xlarge for
hybrid jobs
The maximum number
of instances of type
ml.g4dn.xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.g4dn.2xlarge for
hybrid jobs
The maximum number
of instances of type
ml.g4dn.2xlarge
allowed for all Amazon
Braket Hybrid Jobs in
this account and region.
0 Yes
28
Amazon Braket Developer Guide
Resource Description Limits Adjustable
Maximum number
of instances of
ml.g4dn.4xlarge for
hybrid jobs
The maximum number
of instances of type
ml.g4dn.4xlarge
allowed for all Amazon
Braket Hybrid Jobs in
this account and region.
0 Yes
Maximum number
of instances of
ml.g4dn.8xlarge for
hybrid jobs
The maximum number
of instances of type
ml.g4dn.8xlarge
allowed for all Amazon
Braket Hybrid Jobs in
this account and region.
0 Yes
Maximum number
of instances of
ml.g4dn.12xlarge for
hybrid jobs
The maximum number
of instances of type
ml.g4dn.12xlarge
allowed for all Amazon
Braket Hybrid Jobs in
this account and region.
0 Yes
Maximum number
of instances of
ml.g4dn.16xlarge for
hybrid jobs
The maximum number
of instances of type
ml.g4dn.16xlarge
allowed for all Amazon
Braket Hybrid Jobs in
this account and region.
0 Yes
Maximum number
of instances of
ml.m4.xlarge for hybrid
jobs
The maximum number
of instances of type
ml.m4.xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.m4.2xlarge for
hybrid jobs
The maximum number
of instances of type
ml.m4.2xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.m4.4xlarge for
hybrid jobs
The maximum number
of instances of type
ml.m4.4xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
2 Yes
Maximum number
of instances of
ml.m4.10xlarge for
hybrid jobs
The maximum number
of instances of type
ml.m4.10xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
29
Amazon Braket Developer Guide
Resource Description Limits Adjustable
Maximum number
of instances of
ml.m4.16xlarge for
hybrid jobs
The maximum number
of instances of type
ml.m4.16xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.m5.large for hybrid
jobs
The maximum number
of instances of type
ml.m5.large allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.m5.xlarge for hybrid
jobs
The maximum number
of instances of type
ml.m5.xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.m5.2xlarge for
hybrid jobs
The maximum number
of instances of type
ml.m5.2xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.m5.4xlarge for
hybrid jobs
The maximum number
of instances of type
ml.m5.4xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
5 Yes
Maximum number
of instances of
ml.m5.12xlarge for
hybrid jobs
The maximum number
of instances of type
ml.m5.12xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.m5.24xlarge for
hybrid jobs
The maximum number
of instances of type
ml.m5.24xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.p2.xlarge for hybrid
jobs
The maximum number
of instances of type
ml.p2.xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
30
Amazon Braket Developer Guide
Additional quotas and limits
Resource Description Limits Adjustable
Maximum number
of instances of
ml.p2.8xlarge for hybrid
jobs
The maximum number
of instances of type
ml.p2.8xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.p2.16xlarge for
hybrid jobs
The maximum number
of instances of type
ml.p2.16xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.p3.2xlarge for hybrid
jobs
The maximum number
of instances of type
ml.p3.2xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.p3.8xlarge for hybrid
jobs
The maximum number
of instances of type
ml.p3.8xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum number
of instances of
ml.p3.16xlarge for
hybrid jobs
The maximum number
of instances of type
ml.p3.16xlarge allowed
for all Amazon Braket
Hybrid Jobs in this
account and region.
0 Yes
Maximum allowed
compute instances for a
hybrid job
The maximum allowed
number of compute
instances for a hybrid
job.
5 Yes
Requesting limit updates
If you receive a ServiceQuotaExceeded exception for an instance type and do not have sufficient
instances available for it, you may request a limit increase from the Service Quotas page in the AWS
console and search for Amazon Braket under AWS Services.
Note
p3 instances are not available in us-west-1. If your hybrid job is unable to provision requested
ML compute capacity, use another region. In addition, if you do not see an instance in the table,
it is not available for Hybrid Jobs.
Additional quotas and limits
• The Amazon Braket quantum task action is limited to 3MB in size.
31
Amazon Braket Developer Guide
Additional quotas and limits
• The maximum number of shots per task allowed for SV1, DM1, and Rigetti devices is 100,000.
• The maximum number of shots per task allowed for TN1 is 1000.
• For IonQ and OQC devices, the maximum is 10,000 shots per task.
• For QuEra, the maximum allowed shots per task is 1000.
• For TN1 and the QPU devices, shots per task must be > 0.
32
Amazon Braket Developer Guide
Status change notifications in email or SMS
When will my quantum task run?
When you submit a circuit, Amazon Braket sends it to the device you specify. Quantum Processing Unit
(QPU) and on-demand simulator quantum tasks are queued and processed in the order they are received.
The time required to process your quantum task after you submit it varies depending on the number
and complexity of tasks submitted by other Amazon Braket customers and the availability of the QPU
selected.
Status change notifications in email or SMS
Amazon Braket sends events to Amazon EventBridge when the availability of a QPU changes or when
your quantum task’s state changes. Follow these steps to receive device and quantum task status change
notifications by email or SMS message:
1. Create an Amazon SNS topic and a subscription to email or SMS. Availability of email or SMS depends
on your Region. For more information, see Getting started with Amazon SNS and Sending SMS
messages.
2. Create a rule in EventBridge that triggers the notifications to your SNS topic. For more information,
see Monitoring Amazon Braket with Amazon EventBridge (p. 204).
Quantum task completion alerts
You can set up notifications through the Amazon Simple Notification Service (SNS) so that you receive an
alert when your Amazon Braket quantum task is complete. Active notifications are useful if you expect
a long wait time — for example, when you submit a large task or when you submit a task outside of a
device’s availability window. If you do not want to wait for the task to complete, you can set up an SNS
notification.
An Amazon Braket notebook walks you through the setup steps. For more information, see the Amazon
Braket example notebook for setting up notifications.
QPU availability windows and status
QPU availability varies from device to device.
In the Devices page of the Amazon Braket console, you can see the current and upcoming availability
windows and device status. Additionally, each device page shows individual queue depths for quantum
tasks and hybrid jobs.
A device is considered offline if is not available to customers, regardless of availability window. For
example, it could be offline due to scheduled maintenance, upgrades, or operational issues.
Queue visibility
Before submitting a quantum task or hybrid job, you can view how many quantum tasks or hybrid jobs
are in front of you by checking device queue depth.
Queue depth
33
Amazon Braket Developer Guide
Queue visibility
Queue depth refers to the number of quantum tasks and hybrid jobs queued for a particular device.
A device’s quantum task and hybrid job queue count are accessible through the Braket Software
Development Kit (SDK) or Amazon Braket Management Console.
1. Task queue depth refers to the total number of quantum tasks currently waiting to run in normal
priority.
2. Priority task queue depth refers to the total number of submitted quantum tasks waiting to run
through Amazon Braket Hybrid Jobs. These tasks run before standalone tasks.
3. Hybrid jobs queue depth refers to the total number of hybrid jobs currently queued on a device.
Quantum tasks submitted as part of a hybrid job have priority, and are aggregated in the Priority Task
Queue.
Customers wishing to view queue depth via the Braket SDK can modify the following code snippet to get
the queue position of their quantum task or hybrid job:
device = AwsDevice("arn:aws:braket:us-east-1::device/qpu/ionq/Harmony")
# returns the number of quantum tasks queued on the device
print(device.queue_depth().quantum_tasks)
{<QueueType.NORMAL: 'Normal'>: '0', <QueueType.PRIORITY: 'Priority'>: '0'}
# returns the number of hybrid jobs queued on the device
print(device.queue_depth().jobs)
'3'

Submitting a quantum task or hybrid job to a QPU may result in your workload being in a QUEUED state.
Amazon Braket provides customers visibility into their quantum task and hybrid job queue position.
Queue position
Queue position refers to the current position of your quantum task or hybrid job within a respective
device queue. It can be obtained for quantum tasks or hybrid jobs through the Braket Software
Development Kit (SDK) or Amazon Braket Management Console.
Customers wishing to view queue position via the Braket SDK can modify the following code snippet to
get the queue position of their quantum task or hybrid job:
# choose the device to run your circuit
device = AwsDevice("arn:aws:braket:us-east-1::device/qpu/ionq/Harmony")

#execute the circuit
task = device.run(bell, s3_folder, shots=100)
# retrieve the queue position information
print(task.queue_position().queue_position)

# Returns the number of Quantum Tasks queued ahead of you
'2'

from braket.aws import AwsQuantumJob
job = AwsQuantumJob.create(
 "arn:aws:braket:us-east-1::device/qpu/ionq/Harmony",
 source_module="algorithm_script.py",
 entry_point="algorithm_script:start_here",
 wait_until_complete=False
)
34
Amazon Braket Developer Guide
Queue visibility
# retrieve the queue position information
print(job.queue_position().queue_position)
'3' # returns the number of hybrid jobs queued ahead of you
35
Amazon Braket Developer Guide
Prerequisites
Enable Amazon Braket
You can enable Amazon Braket in your account through the AWS console.
Prerequisites
To enable and run Amazon Braket, you must have a user or role with permission to initiate Amazon
Braket actions. These permissions are included in the AmazonBraketFullAccess IAM policy
(ARN:arn:aws:iam::aws:policy/AmazonBraketFullAccess).
Note
If you are an administrator:
To give other users access to Amazon Braket, grant users permissions by attaching the
AmazonBraketFullAccess policy or by attaching a custom policy that you create. To learn more
about the permissions necessary to use Amazon Braket, see Managing access to Amazon Braket
 (p. 176).
Steps to enable Amazon Braket
1. Sign in to the Amazon Braket console with your AWS account.
2. Open the Amazon Braket console.
3. From the Braket landing page, click Get Started to be taken to the Service Dashboard page. The alert
at the top of your service dashboard will walk you through the following three steps:
a. Creating service-linked roles (SLR) (p. 185)
b. Enabling access to third-party quantum computers
c. Creating a new Jupyter notebook instance
In order to use third-party quantum devices, you need to agree to certain conditions regarding data
transfer between yourself, AWS, and those devices. The terms and conditions of this agreement are
provided on the General tab of the Permissions and settings page in the Amazon Braket console.
Note
Quantum devices that don’t involve any third-parties, such as the Braket local simulators
or on-demand simulators, can be used without agreeing to the Enable third-party devices
agreement.
Accepting these terms to enable use of third-party devices only needs to be done once per
account if you are accessing third-party hardware.
36
Amazon Braket Developer Guide
Create an Amazon Braket notebook instance
Get started with Amazon Braket
After you have followed the instructions in Enable Amazon Braket (p. 36), you can get started with
Amazon Braket.
The steps to get started include:
• Create an Amazon Braket notebook instance (p. 37)
• Run your first circuit using the Amazon Braket Python SDK (p. 39)
• Explore the algorithm library (p. 42)
• Hello AHS: Run your first Analog Hamiltonian Simulation (p. 42)
Create an Amazon Braket notebook instance
Amazon Braket provides fully-managed Jupyter notebooks to get you started. The Amazon Braket
notebook instances are based on Amazon SageMaker notebook instances. You can learn more about
notebook instances. To get started with Braket, follow these steps to create an Amazon Braket notebook
instance.
1. Open the Amazon Braket console.
2. Choose Notebooks in the left pane, then choose Create notebook.
3. In Notebook instance settings, enter a Notebook instance name using only alphanumeric and
hyphen characters.
4. Select the Notebook instance type. Choose the smallest type you need. To get started, choose a costeffective instance type, such as ml.t3.medium. The instance types are Amazon SageMaker notebook
instances. To learn more, see Amazon SageMaker pricing.
5. In Permissions and encryption, select Create a new role (a new role with a name that begins
with`AmazonBraketServiceSageMakerNotebook` is created).
6. If you want to associate a public Github repository with your notebook instance, click on the Git
repository dropdown and select Clone a public git repository from url from the Repository
dropdown menu. Enter the URL of the repo in the Git repository URL text bar.
37
Amazon Braket Developer Guide
Create an Amazon Braket notebook instance
38
Amazon Braket Developer Guide
Run your first circuit using the Amazon Braket Python SDK
7. Choose Create notebook instance.
It takes several minutes to create the notebook. The notebook is displayed on the Notebooks
page with a status of Pending. When the notebook instance is ready to use, the status changes to
InService. You may need to refresh the page to display the updated status for the notebook.
Note
You can view and manage your Amazon Braket notebook instances in the Amazon Braket
and Amazon SageMaker consoles. Additional Amazon Braket notebook settings are available
through the SageMaker console.
If you’re working in the Amazon Braket console within AWS, as given previously, the Amazon Braket SDK
and plugins are preloaded in the notebooks you just created. If you want to run on your own machine,
you can install the SDK and plugins when you run the command pip install amazon-braket-sdk
or when you run the command pip install amazon-braket-pennylane-plugin (the latter for
use with PennyLane plugins).
Run your first circuit using the Amazon Braket
Python SDK
After your notebook instance has launched, open the instance with a standard Jupyter interface by
choosing the notebook you just created.
Amazon Braket notebook instances are pre-installed with the Amazon Braket SDK and all its
dependencies. Start by creating a new notebook with conda_braket kernel.
You can start with a simple “Hello, world!” example. First, construct a circuit that prepares a Bell state,
and then run that circuit on different devices to obtain the results.
39
Amazon Braket Developer Guide
Run your first circuit using the Amazon Braket Python SDK
Begin by importing the Amazon Braket SDK modules and defining a simple Bell State circuit.
import boto3
from braket.aws import AwsDevice
from braket.devices import LocalSimulator
from braket.circuits import Circuit
# create the circuit
bell = Circuit().h(0).cnot(0, 1)
You can visualize the circuit with this command:
print(bell)
Run your circuit on the local simulator
Next, choose the quantum device on which to execute the circuit. The Amazon Braket SDK comes with a
local simulator for rapid prototyping and testing. We recommend using the local simulator for smaller
circuits, which can be up to 25 qubits (depending on your local hardware).
Here’s how to instantiate the local simulator:
# instantiate the local simulator
local_sim = LocalSimulator()
and run the circuit:
# run the circuit
result = local_sim.run(bell, shots=1000).result()
counts = result.measurement_counts
print(counts)
You should see a result something like this:
Counter({'11': 503, '00': 497})
The specific Bell state you have prepared is an equal superposition of |00> and |11>, and you’ll find a
roughly equal (up to shot noise) distribution of 00 and 11 as measurement outcomes, as expected.
Run your circuit on an on-demand simulator
Amazon Braket also provides access to an on-demand, high-performance simulator, SV1, for running
larger circuits. SV1 is an on-demand state-vector simulator that allows for simulation of quantum circuits
of up to 34 qubits. You can find more information on SV1 in the Supported Devices (p. 8) section and
in the AWS console. When running quantum tasks on SV1 (and on TN1 or any QPU), the results of your
quantum task are stored in an S3 bucket in your account. If you do not specify a bucket, the Braket
SDK creates a default bucket amazon-braket-{region}-{accountID} for you. To learn more, see
Managing access to Amazon Braket (p. 176).
Note
Fill in your actual, existing bucket name where the following example shows example-bucket
as your bucket name. Bucket names for Amazon Braket always begin with amazon-braketfollowed by other identifying characters you add. If you need information on how to set up an
S3 bucket, see Getting started with Amazon S3.
# get the account ID
aws_account_id = boto3.client("sts").get_caller_identity()["Account"]
# the name of the bucket
40
Amazon Braket Developer Guide
Run your first circuit using the Amazon Braket Python SDK
my_bucket = "example-bucket"
# the name of the folder in the bucket
my_prefix = "simulation-output"
s3_folder = (my_bucket, my_prefix)
To run a circuit on SV1, you must provide the location of the S3 bucket you previously selected as a
positional argument in the .run() call.
# choose the cloud-based on-demand simulator to run your circuit
device = AwsDevice("arn:aws:braket:::device/quantum-simulator/amazon/sv1")
# execute the circuit
task = device.run(bell, s3_folder, shots=100)
# display the results
print(task.result().measurement_counts)
The Amazon Braket console provides further information about your quantum task. Navigate to the
Quantum Tasks tab in the console and your quantum task should be on the top of the list. Alternatively,
you can search for your quantum task using the unique quantum task ID or other criteria.
Note
After 90 days, Amazon Braket automatically removes all quantum task IDs and other metadata
associated with your quantum tasks. For more information, see Data retention.
Running on a QPU
With Amazon Braket, you can run the previous quantum circuit example on a physical quantum computer
by just changing a single line of code. Amazon Braket provides access to QPU devices from IonQ,
Oxford Quantum Circuits, QuEra, and Rigetti. You can find information about the different devices and
availability windows in the Supported Devices (p. 8) section, and in the AWS console under the Devices
tab. The following example shows how to instantiate a Rigetti device.
# choose the Rigetti hardware to run your circuit
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
Choose an IonQ device with this code:
# choose the Ionq device to run your circuit
device = AwsDevice("arn:aws:braket:us-east-1::device/qpu/ionq/Harmony")
After selecting a device and before running your workload, you can query device queue depth with the
following code to determine the number of quantum tasks or hybrid jobs. Additionally, customers can
view device specific queue depths on the Devices page of the Amazon Braket Management Console.
# Print your queue depth
print(device.queue_depth().quantum_tasks)
# returns the number of quantum tasks queued on the device
{<QueueType.NORMAL: 'Normal'>: '0', <QueueType.PRIORITY: 'Priority'>: '0'}
print(device.queue_depth().jobs)
'2' # returns the number of hybrid jobs queued on the device
When you run your task, the Amazon Braket SDK polls for a result (with a default timeout of 5 days).
You can change this default by modifying the poll_timeout_seconds parameter in the the .run()
command as shown in the example that follows. Keep in mind that if your polling timeout is too short,
results may not be returned within the polling time, such as when a QPU is unavailable and a local
timeout error is returned. You can restart the polling by calling the task.result() function.
# define quantum task with 1 day polling timeout
41
Amazon Braket Developer Guide
Explore the algorithm library
task = device.run(bell, s3_folder, poll_timeout_seconds=24*60*60)
print(task.result().measurement_counts)
Additionally, after submitting your quantum task or hybrid job, you can call the queue_position()
function to check your queue position.
print(task.queue_position().queue_position)
# Return the number of quantum tasks queued ahead of you
'2'

print(job.queue_position().queue_position)
# Return the number of hybrid jobs queued ahead of you
'3'
Explore the algorithm library
The Amazon Braket algorithm library is a catalog of pre-built quantum algorithms written in Python. You
can run these algorithms as they are or use them as a starting point to build more complex algorithms.
You can access the algorithm library from the Braket console. You can also access the Braket algorithm
library on Github: https://github.com/aws-samples/amazon-braket-algorithm-library.
The Braket console provides a description of each available algorithm in the algorithm library. Choose a
GitHub link to see the details of each algorithm, or choose Open notebook to open or create a notebook
that contains all of the available algorithms. If you choose the notebook option, you can then find the
Braket algorithm library in the root folder of your notebook.
Hello AHS: Run your first Analog Hamiltonian
Simulation
AHS
Analog Hamiltonian Simulation (AHS) is a paradigm of quantum computing different from quantum
circuits: instead of a sequence of gates, each acting only on a couple of qubits at a time, an AHS
42
Amazon Braket Developer Guide
Interacting spin chain
program is defined by the time- and space-dependent parameters of the Hamiltonian in question. The
Hamiltonian of a system encodes its energy levels and the effects of external forces, which together
govern the time evolution of its states. For an N-qubit systems, the Hamiltonian can be represented by a
2
N
X2N
square matrix of complex numbers.
Quantum devices capable of performing AHS will tune their parameters (for example amplitude
and detuning of a coherent driving field) to closely approximate the time evolution of the quantum
system under the custom Hamiltonian. The AHS paradigm is suitable for simulating static and dynamic
properties of quantum systems of many interacting particles. Purpose-built QPUs, such as the Aquila
device from QuEra can simulate the time evolution of systems with sizes that are otherwise infeasible on
classical hardware.
Interacting spin chain
For a canonical example of a system of many interacting particles, let us consider a ring of eight spins
(each of which can be in “up” ∣↑# and “down” ∣↓# states). Albeit small, this model system already exhibits
a handful of interesting phenomena of naturally occurring magnetic materials. In this example, we will
show how to prepare a so-called anti-ferromagnetic order, where consecutive spins point in opposite
directions.
43
Amazon Braket Developer Guide
Arrangement
Arrangement
We will use one neutral atom to stand for each spin, and the “up” and “down” spin states will be
encoded in excited Rydberg state and ground state of the atoms, respectively. First, we create the 2-d
arrangement. We can program the above ring of spins with the following code.
Prerequisites: You need to pip install the Braket SDK. (If you are using a Braket hosted notebook
instance, this SDK comes pre-installed with the notebooks.) To reproduce the plots, you also need to
separately install matplotlib with the shell command pip install matplotlib.
import numpy as np
import matplotlib.pyplot as plt # required for plotting
from braket.ahs.atom_arrangement import AtomArrangement
a = 5.7e-6 # nearest-neighbor separation (in meters)
44
Amazon Braket Developer Guide
Arrangement
register = AtomArrangement()
register.add(np.array([0.5, 0.5 + 1/np.sqrt(2)]) * a)
register.add(np.array([0.5 + 1/np.sqrt(2), 0.5]) * a)
register.add(np.array([0.5 + 1/np.sqrt(2), - 0.5]) * a)
register.add(np.array([0.5, - 0.5 - 1/np.sqrt(2)]) * a)
register.add(np.array([-0.5, - 0.5 - 1/np.sqrt(2)]) * a)
register.add(np.array([-0.5 - 1/np.sqrt(2), - 0.5]) * a)
register.add(np.array([-0.5 - 1/np.sqrt(2), 0.5]) * a)
register.add(np.array([-0.5, 0.5 + 1/np.sqrt(2)]) * a)
which we can also plot with
fig, ax = plt.subplots(1, 1, figsize=(7,7))
xs, ys = [register.coordinate_list(dim) for dim in (0, 1)]
ax.plot(xs, ys, 'r.', ms=15)
for idx, (x, y) in enumerate(zip(xs, ys)):
 ax.text(x, y, f" {idx}", fontsize=12)
plt.show() # this will show the plot below in an ipython or jupyter session
45
Amazon Braket Developer Guide
Interaction
Interaction
To prepare the anti-ferromagnetic phase, we need to induce interactions between neighboring spins.
We use the van der Waals interaction for this, which is natively implemented by neutral atom devices
(such as the Aquila device from QuEra). Using the spin-representation, the Hamiltonian term for this
interaction can be expressed as a sum over all spin pairs (j,k).
Here, nj=∣↑j
⟩⟨#j
∣ is an operator that takes the value of 1 only if spin j is in the “up” state, and 0 otherwise.
The strength is Vj,k=C6/(dj,k)
6
, where C6 is the fixed coefficient, and dj,k is the Euclidean distance between
spins j and k. The immediate effect of this interaction term is that any state where both spin j and spin k
are “up” have elevated energy (by the amount Vj,k). By carefully designing the rest of the AHS program,
this interaction will prevent neighboring spins from both being in the “up” state, an effect commonly
known as "Rydberg blockade."
46
Amazon Braket Developer Guide
Driving field
Driving field
At the beginning of the AHS program, all spins (by default) start in their “down” state, they are in a socalled ferromagnetic phase. Keeping an eye on our goal to prepare the anti-ferromagnetic phase, we
specify a time-dependent coherent driving field that smoothly transitions the spins from this state to a
many-body state where the “up” states are preferred. The corresponding Hamiltonian can be written as
where Ω(t),ϕ(t),Δ(t) are the time-dependent, global amplitude (aka Rabi frequency), phase, and detuning
of the driving field affecting all spins uniformly. Here S−,k=∣↓k⟩⟨#k∣and S+,k=(S−,k)
†
=∣↑k⟩⟨#k∣ are the
lowering and raising operators of spin k, respectively, and nk=∣↑k⟩⟨#k∣ is the same operator as before. The
Ω part of the driving field coherently couples the “down” and the “up” states of all spins simultaneously,
while the Δ part controls the energy reward for “up” states.
To program a smooth transition from the ferromagnetic phase to the anti-ferromagnetic phase, we
specify the driving field with the following code.
from braket.timings.time_series import TimeSeries
from braket.ahs.driving_field import DrivingField
# smooth transition from "down" to "up" state
time_max = 4e-6 # seconds
time_ramp = 1e-7 # seconds
omega_max = 6300000.0 # rad / sec
delta_start = -5 * omega_max
delta_end = 5 * omega_max
omega = TimeSeries()
omega.put(0.0, 0.0)
omega.put(time_ramp, omega_max)
omega.put(time_max - time_ramp, omega_max)
omega.put(time_max, 0.0)
delta = TimeSeries()
delta.put(0.0, delta_start)
delta.put(time_ramp, delta_start)
delta.put(time_max - time_ramp, delta_end)
delta.put(time_max, delta_end)
phi = TimeSeries().put(0.0, 0.0).put(time_max, 0.0)
drive = DrivingField(
 amplitude=omega,
 phase=phi,
 detuning=delta
)
We can visualize the time series of the driving field with the following script.
fig, axes = plt.subplots(3, 1, figsize=(12, 7), sharex=True)
ax = axes[0]
time_series = drive.amplitude.time_series
ax.plot(time_series.times(), time_series.values(), '.-');
ax.grid()
ax.set_ylabel('Omega [rad/s]')
ax = axes[1]
time_series = drive.detuning.time_series
ax.plot(time_series.times(), time_series.values(), '.-');
47
Amazon Braket Developer Guide
AHS program
ax.grid()
ax.set_ylabel('Delta [rad/s]')
ax = axes[2]
time_series = drive.phase.time_series
# Note: time series of phase is understood as a piecewise constant function
ax.step(time_series.times(), time_series.values(), '.-', where='post');
ax.set_ylabel('phi [rad]')
ax.grid()
ax.set_xlabel('time [s]')
plt.show() # this will show the plot below in an ipython or jupyter session
AHS program
The register, the driving field, (and the implicit van der Waals interactions) make up the Analog
Hamiltonian Simulation program ahs_program.
from braket.ahs.analog_hamiltonian_simulation import AnalogHamiltonianSimulation
ahs_program = AnalogHamiltonianSimulation(
 register=register,
 hamiltonian=drive
)
Running on local simulator
Since this example is small (less than 15 spins), before running it on an AHS-compatible QPU, we can run
it on the local AHS simulator which comes with the Braket SDK. Since the local simulator is available for
free with the Braket SDK, this is best practice to ensure that our code can correctly execute.
Here, we can set the number of shots to a high value (say, 1 million) because the local simulator tracks
the time evolution of the quantum state and draws samples from the final state; hence, increasing the
number of shots, while increasing the total runtime only marginally.
48
Amazon Braket Developer Guide
Analyzing simulator results
from braket.devices import LocalSimulator
device = LocalSimulator("braket_ahs")
result_simulator = device.run(
 ahs_program,
 shots=1_000_000
).result() # takes about 5 seconds
Analyzing simulator results
We can aggregate the shot results with the following function that infers the state of each spin
(which may be “d” for “down”, “u” for “up”, or “e” for empty site), and counts how many times each
configuration occurred across the shots.
from collections import Counter
def get_counts(result):
 """Aggregate state counts from AHS shot results
 A count of strings (of length = # of spins) are returned, where
 each character denotes the state of a spin (site):
 e: empty site
 u: up state spin
 d: down state spin
 Args:
 result
 (braket.tasks.analog_hamiltonian_simulation_quantum_task_result.AnalogHamiltonianSimulationQuantumTask Returns
 dict: number of times each state configuration is measured
 """
 state_counts = Counter()
 states = ['e', 'u', 'd']
 for shot in result.measurements:
 pre = shot.pre_sequence
 post = shot.post_sequence
 state_idx = np.array(pre) * (1 + np.array(post))
 state = "".join(map(lambda s_idx: states[s_idx], state_idx))
 state_counts.update((state,))
 return dict(state_counts)
counts_simulator = get_counts(result_simulator) # takes about 5 seconds
print(counts_simulator)
{'udududud': 330944, 'dudududu': 329576, 'dududdud': 38033, ...}
Here counts is a dictionary that counts the number of times each state configuration is observed across
the shots. We can also visualize them with the following code.
from collections import Counter
def has_neighboring_up_states(state):
 if 'uu' in state:
 return True
 if state[0] == 'u' and state[-1] == 'u':
 return True
 return False
49
Amazon Braket Developer Guide
Analyzing simulator results
def number_of_up_states(state):
 return Counter(state)['u']
def plot_counts(counts):
 non_blockaded = []
 blockaded = []
 for state, count in counts.items():
 if not has_neighboring_up_states(state):
 collection = non_blockaded
 else:
 collection = blockaded
 collection.append((state, count, number_of_up_states(state)))
 blockaded.sort(key=lambda _: _[1], reverse=True)
 non_blockaded.sort(key=lambda _: _[1], reverse=True)
 for configurations, name in zip((non_blockaded,
 blockaded),
 ('no neighboring "up" states',
 'some neighboring "up" states')):
 plt.figure(figsize=(14, 3))
 plt.bar(range(len(configurations)), [item[1] for item in configurations])
 plt.xticks(range(len(configurations)))
 plt.gca().set_xticklabels([item[0] for item in configurations], rotation=90)
 plt.ylabel('shots')
 plt.grid(axis='y')
 plt.title(f'{name} configurations')
 plt.show()
plot_counts(counts_simulator)
From the plots, we can read the following observations the verify that we successfully prepared the antiferromagnetic phase.
50
Amazon Braket Developer Guide
Running on QuEra’s Aquila QPU
1. Generally, non-blockaded states (where no two neighboring spins are in the “up” state) are more
common than states where at least one pair of neighboring spins are both in “up” states.
2. Generally, states with more "up" excitations are favored, unless the configuration is blockaded.
3. The most common states are indeed the perfect anti-ferromagnetic states "dudududu" and
"udududud".
4. The second most common states are the ones where there is only 3 “up” excitations with consecutive
separations of 1, 2, 2. This shows that the van der Waals interaction has an affect (albeit much
smaller) on next-nearest neighbors too.
Running on QuEra’s Aquila QPU
Prerequisites: Apart from pip installing the Braket SDK, if you are new to Amazon Braket, please make
sure that you have completed the necessary Get Started steps.
Note
If you are using a Braket hosted notebook instance, the Braket SDK comes pre-installed with the
instance.
With all dependencies installed, we can connect to the Aquila QPU.
from braket.aws import AwsDevice
aquila_qpu = AwsDevice("arn:aws:braket:us-east-1::device/qpu/quera/Aquila")
To make our AHS program suitable for the QuEra machine, we need to round all values to
comply with the levels of precision allowed by the Aquila QPU. (These requirements are governed
by the device parameters with “Resolution” in their name. We can see them by executing
aquila_qpu.properties.dict() in a notebook. For more details of capabilities and requirements of
Aquila, see the Introduction to Aquila notebook.) We can do this by calling the discretize method.
discretized_ahs_program = ahs_program.discretize(aquila_qpu)
Now we can run the program (running only 100 shots for now) on the Aquila QPU.
Note
Running this program on the Aquila processor will incur a cost. The Amazon Braket SDK includes
a Cost Tracker that enables customers to set cost limits as well as track their costs in near realtime.
task = aquila_qpu.run(discretized_ahs_program, shots=100)
metadata = task.metadata()
task_arn = metadata['quantumTaskArn']
task_status = metadata['status']
print(f"ARN: {task_arn}")
print(f"status: {task_status}")
task ARN: arn:aws:braket:us-east-1:123456789012:quantum-task/12345678-90abcdef-1234-567890abcdef
task status: CREATED
Due to the large variance of how long a quantum task may take to run (depending on availability
windows and QPU utilization), it is a good idea to note down the quantum task ARN, so we can check its
status at a later time with the following code snippet.
51
Amazon Braket Developer Guide
Analyzing QPU results
# Optionally, in a new python session
from braket.aws import AwsQuantumTask
SAVED_TASK_ARN = "arn:aws:braket:us-east-1:123456789012:quantum-task/12345678-90abcdef-1234-567890abcdef"
task = AwsQuantumTask(arn=SAVED_TASK_ARN)
metadata = task.metadata()
task_arn = metadata['quantumTaskArn']
task_status = metadata['status']
print(f"ARN: {task_arn}")
print(f"status: {task_status}")
*[Output]*
task ARN: arn:aws:braket:us-east-1:123456789012:quantum-task/12345678-90abcdef-1234-567890abcdef
task status: COMPLETED
Once the status is COMPLETED (which can also be checked from the quantum tasks page of the Amazon
Braket console), we can query the results with:
result_aquila = task.result()
Analyzing QPU results
Using the same get_counts functions as before, we can compute the counts:
counts_aquila = get_counts(result_aquila)
print(counts_aquila)
*[Output]*
{'udududud': 24, 'dudududu': 17, 'dududdud': 3, ...}
and plot them with plot_counts:
plot_counts(counts_aquila)
52
Amazon Braket Developer Guide
Next
Note that a small fraction of shots have empty sites (marked with “e”). This is due to a 1—2% per atom
preparation imperfections of the Aquila QPU. Apart from this, the results match with the simulation
within the expected statistical fluctuation due to small number of shots.
Next
Congratulations, you have now run your first AHS workload on Amazon Braket using the local AHS
simulator and the Aquila QPU.
To learn more about Rydberg physics, Analog Hamiltonian Simulation and the Aquila device, refer to our
example notebooks.
53
Amazon Braket Developer Guide
Work with Amazon Braket
This section shows you how to design quantum circuits, submit these problems as quantum tasks to
devices, and monitor the quantum tasks with the Amazon Braket SDK.
The following are the main means of interacting with resources on Amazon Braket.
• The Amazon Braket Console provides device information and status to help you create, manage, and
monitor your resources and quantum tasks.
• Submit and run quantum tasks through the Amazon Braket Python SDK, as well as through the
console. The SDK is accessible through preconfigured Amazon Braket notebooks.
• The Amazon Braket API is accessible through the Amazon Braket Python SDK and notebooks. You
can make calls directly to the API if you’re building applications that work with quantum computing
programmatically.
The examples throughout this section demonstrate how you can work with the Amazon Braket API
directly using the Amazon Braket Python SDK along with the AWS Python SDK for Braket (Boto3).
More about the Amazon Braket Python SDK
To work with the Amazon Braket Python SDK, first install the AWS Python SDK for Braket (Boto3) so
that you can communicate with the AWS API. You can think of the Amazon Braket Python SDK as a
convenient wrapper around Boto3 for quantum customers.
• Boto3 contains interfaces you need to tap into the AWS API. (Note that Boto3 is a large Python SDK
that talks to the AWS API. Most AWS services support a Boto3 interface.)
• The Amazon Braket Python SDK contains software modules for circuits, gates, devices, result types,
and other parts of a quantum task. Each time you create a program, you import the modules you need
for that quantum task.
• The Amazon Braket Python SDK is accessible through notebooks, which are pre-loaded with all of the
modules and dependencies you need for running quantum tasks.
• You can import modules from the Amazon Braket Python SDK into any Python script if you do not
wish to work with notebooks.
After you’ve installed Boto3, an overview of steps for creating a quantum task through the Amazon
Braket Python SDK resembles the following:
1. (Optionally) Open your notebook.
2. Import the SDK modules you need for your circuits.
3. Specify a QPU or simulator.
4. Instantiate the circuit.
5. Run the circuit.
6. Collect the results.
The examples in this section show details of each step.
For more examples, see the Amazon Braket Examples repository on GitHub.
In this section:
• Construct circuits in the SDK (p. 55)
• Run your circuits with OpenQASM 3.0 (p. 66)
54
Amazon Braket Developer Guide
Construct circuits in the SDK
• Submitting quantum tasks to QPUs and simulators (p. 84)
• Submit an analog program using QuEra’s Aquila (p. 92)
• Monitoring and tracking quantum tasks (p. 105)
• Working with Boto3 (p. 111)
Construct circuits in the SDK
This section provides examples of defining a circuit, viewing available gates, extending a circuit, and
viewing gates that each device supports. It also contains instructions on how to manually allocate
qubits, instruct the compiler to run your circuits exactly as defined, and build noisy circuits with a noise
simulator.
You can also work at the pulse level in Braket for various gates with certain QPUs. For more information,
see Pulse Control on Amazon Braket (p. 116).
In this section:
• Gates and circuits (p. 55)
• Manual qubit allocation (p. 59)
• Verbatim compilation (p. 60)
• Noise simulation (p. 60)
• Inspecting the circuit (p. 61)
• Result types (p. 63)
Gates and circuits
Quantum gates and circuits are defined in the braket.circuits class of the Amazon Braket Python
SDK. From the SDK, you can instantiate a new circuit object by calling Circuit().
Example: Define a circuit
The example starts by defining a sample circuit of four qubits (labelled q0, q1, q2, and q3) consisting
of standard, single-qubit Hadamard gates and two-qubit CNOT gates. You can visualize this circuit by
calling the print function as the following example shows.
# import the circuit module
from braket.circuits import Circuit
# define circuit with 4 qubits
my_circuit = Circuit().h(range(4)).cnot(control=0, target=2).cnot(control=1, target=3)
print(my_circuit)
T : |0| 1 |
q0 : -H-C---
 |
q1 : -H-|-C-
 | |
q2 : -H-X-|-
 |
q3 : -H---XT : |0| 1 |
Example: Define a parameterized circuit
55
Amazon Braket Developer Guide
Gates and circuits
In this example, we define a circuit with gates that depend on free parameters. We can specify the values
of these parameters to create a new circuit, or, when submitting the circuit, to run as a quantum task on
certain devices.
from braket.circuits import Circuit, FreeParameter
#define a FreeParameter to represent the angle of a gate
alpha = FreeParameter("alpha")
#define a circuit with three qubits
my_circuit = Circuit().h(range(3)).cnot(control=0, target=2).rx(0, alpha).rx(1, alpha)
print(my_circuit)
You can create a new, non-parametrized circuit from a parametrized one by supplying either a single
float (which is the value all free parameters will take) or keyword arguments specifying each
parameter’s value to the circuit as follows.
my_fixed_circuit = my_circuit(1.2)
my_fixed_circuit = my_circuit(alpha=1.2)
Note that my_circuit is unmodified, so you can use it to instantiate many new circuits with fixed
parameter values.
Example: Modify gates in a circuit
The following example defines a circuit with gates that use control and power modifiers. You can use
these modifications to create new gates, such as the controlled Ry gate.
from braket.circuits import Circuit
# Create a bell circuit with a controlled x gate
my_circuit = Circuit().h(0).x(control=0, target=1)

# Add a multi-controlled Ry gate of angle .13
my_circuit.ry(angle=.13, target=2, control=(0, 1))

# Add a 1/5 root of X gate
my_circuit.x(0, power=1/5)

print(my_circuit)
Gate modifiers are supported only on the local simulator.
Example: See all available gates
The following example shows how to look at all the available gates in Amazon Braket.
from braket.circuits import Gate
# print all available gates in Amazon Braket
gate_set = [attr for attr in dir(Gate) if attr[0].isupper()]
print(gate_set)
The output from this code lists all of the gates.
['CCNot', 'CNot', 'CPhaseShift', 'CPhaseShift00', 'CPhaseShift01', 'CPhaseShift10',
 'CSwap', 'CV', 'CY', 'CZ', 'ECR', 'GPi', 'GPi2', 'H', 'I', 'ISwap', 'MS', 'PSwap',
 'PhaseShift', 'PulseGate', 'Rx', 'Ry', 'Rz', 'S', 'Si', 'Swap', 'T', 'Ti', 'Unitary', 'V',
 'Vi', 'X', 'XX', 'XY', 'Y', 'YY', 'Z', 'ZZ']
56
Amazon Braket Developer Guide
Gates and circuits
Any of these gates can be appended to a circuit by calling the method for that type of circuit. For
example, you’d call circ.h(0), to add a Hadamard gate to the first qubit.
Note
Gates are appended in place, and the example that follows adds all of the gates listed in the
previous example to the same circuit.
circ = Circuit()
# toffoli gate with q0, q1 the control qubits and q2 the target.
circ.ccnot(0, 1, 2)
# cnot gate
circ.cnot(0, 1)
# controlled-phase gate that phases the |11> state, cphaseshift(phi) =
 diag((1,1,1,exp(1j*phi))), where phi=0.15 in the examples below
circ.cphaseshift(0, 1, 0.15)
# controlled-phase gate that phases the |00> state, cphaseshift00(phi) =
 diag([exp(1j*phi),1,1,1])
circ.cphaseshift00(0, 1, 0.15)
# controlled-phase gate that phases the |01> state, cphaseshift01(phi) =
 diag([1,exp(1j*phi),1,1])
circ.cphaseshift01(0, 1, 0.15)
# controlled-phase gate that phases the |10> state, cphaseshift10(phi) =
 diag([1,1,exp(1j*phi),1])
circ.cphaseshift10(0, 1, 0.15)
# controlled swap gate
circ.cswap(0, 1, 2)
# swap gate
circ.swap(0,1)
# phaseshift(phi)= diag([1,exp(1j*phi)])
circ.phaseshift(0,0.15)
# controlled Y gate
circ.cy(0, 1)
# controlled phase gate
circ.cz(0, 1)
# Echoed cross-resonance gate applied to q0, q1
circ = Circuit().ecr(0,1)
# X rotation with angle 0.15
circ.rx(0, 0.15)
# Y rotation with angle 0.15
circ.ry(0, 0.15)
# Z rotation with angle 0.15
circ.rz(0, 0.15)
# Hadamard gates applied to q0, q1, q2
circ.h(range(3))
# identity gates applied to q0, q1, q2
circ.i([0, 1, 2])
# iswap gate, iswap = [[1,0,0,0],[0,0,1j,0],[0,1j,0,0],[0,0,0,1]]
circ.iswap(0, 1)
# pswap gate, PSWAP(phi) = [[1,0,0,0],[0,0,exp(1j*phi),0],[0,exp(1j*phi),0,0],[0,0,0,1]]
circ.pswap(0, 1, 0.15)
# X gate applied to q1, q2
circ.x([1, 2])
# Y gate applied to q1, q2
circ.y([1, 2])
# Z gate applied to q1, q2
circ.z([1, 2])
# S gate applied to q0, q1, q2
circ.s([0, 1, 2])
# conjugate transpose of S gate applied to q0, q1
circ.si([0, 1])
# T gate applied to q0, q1
circ.t([0, 1])
# conjugate transpose of T gate applied to q0, q1
circ.ti([0, 1])
# square root of not gate applied to q0, q1, q2
57
Amazon Braket Developer Guide
Gates and circuits
circ.v([0, 1, 2])
# conjugate transpose of square root of not gate applied to q0, q1, q2
circ.vi([0, 1, 2])
# exp(-iXX theta/2)
circ.xx(0, 1, 0.15)
# exp(i(XX+YY) theta/4), where theta=0.15 in the examples below
circ.xy(0, 1, 0.15)
# exp(-iYY theta/2)
circ.yy(0, 1, 0.15)
# exp(-iZZ theta/2)
circ.zz(0, 1, 0.15)
# IonQ native gate GPi with angle 0.15 applied to q0
circ.gpi(0, 0.15)
# IonQ native gate GPi2 with angle 0.15 applied to q0
circ.gpi2(0, 0.15)
# IonQ native gate MS with angles 0.15, 0.15, 0.15 applied to q0, q1
circ.ms(0, 1, 0.15, 0.15, 0.15)
Apart from the pre-defined gate set, you also can apply self-defined unitary gates to the circuit. These
can be single-qubit gates (as shown in the following source code) or multi-qubit gates applied to the
qubits defined by the targets parameter.
import numpy as np
# apply a general unitary
my_unitary = np.array([[0, 1],[1, 0]])
circ.unitary(matrix=my_unitary, targets=[0])
Example: Extend existing circuits
You can extend existing circuits by adding instructions. An Instruction is a quantum directive that
describes the quantum task to perform on a quantum device. Instruction operators include objects of
type Gate only.
# import the Gate and Instruction modules
from braket.circuits import Gate, Instruction
# add instructions directly.
circ = Circuit([Instruction(Gate.H(), 4), Instruction(Gate.CNot(), [4, 5])])
# or with add_instruction/add functions
instr = Instruction(Gate.CNot(), [0, 1])
circ.add_instruction(instr)
circ.add(instr)
# specify where the circuit is appended
circ.add_instruction(instr, target=[3, 4])
circ.add_instruction(instr, target_mapping={0: 3, 1: 4})
# print the instructions
print(circ.instructions)
# if there are multiple instructions, you can print them in a for loop
for instr in circ.instructions:
 print(instr)
# instructions can be copied
new_instr = instr.copy()
# appoint the instruction to target
new_instr = instr.copy(target=[5])
new_instr = instr.copy(target_mapping={0: 5})
Example: View the gates that each device supports
58
Amazon Braket Developer Guide
Manual qubit allocation
Simulators support all gates in the Braket SDK, but QPU devices support a smaller subset. You can find
the supported gates of a device in the device properties. The following shows an example with an IonQ
device:
# import the device module
from braket.aws import AwsDevice
device = AwsDevice("arn:aws:braket:us-east-1::device/qpu/ionq/Harmony")
# get device name
device_name = device.name
# show supportedQuantumOperations (supported gates for a device)
device_operations = device.properties.dict()['action']['braket.ir.openqasm.program']
['supportedOperations']
print('Quantum Gates supported by {}:\n {}'.format(device_name, device_operations))
Quantum Gates supported by the Harmony device:
 ['x', 'y', 'z', 'rx', 'ry', 'rz', 'h', 'cnot', 's', 'si', 't', 'ti', 'v', 'vi', 'xx',
 'yy', 'zz', 'swap', 'i']
Supported gates may need to be compiled into native gates before they can run on quantum hardware.
When you submit a circuit, Amazon Braket performs this compilation automatically.
Example: Programmatically retrieve the fidelity of native gates supported by a device
You can view the fidelity information on the Devices page of the Braket console. Sometimes it is helpful
to access the same information programmatically. The following code shows how to extract the two
qubit gate fidelity between two gates of a QPU.
# import the device module
from braket.aws import AwsDevice
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
#specify the qubits
a=10
b=113
print(f"Fidelity of the XY gate between qubits {a} and {b}: ",
 device.properties.provider.specs["2Q"][f"{a}-{b}"]["fXY"])
Manual qubit allocation
When you run a quantum circuit on quantum computers from Rigetti, you can optionally use manual
qubit allocation to control which qubits are used for your algorithm. The Amazon Braket Console and
the Amazon Braket SDK help you to inspect the most recent calibration data of your selected quantum
processing unit (QPU) device, so you can select the best qubits for your experiment.
Manual qubit allocation enables you to run circuits with greater accuracy and to investigate individual
qubit properties. Researchers and advanced users optimize their circuit design based on the latest device
calibration data and can obtain more accurate results.
The following example demonstrates how to allocate qubits explicitly.
circ = Circuit().h(0).cnot(0, 7) # Indices of actual qubits in the QPU
my_task = device.run(circ, s3_location, shots=100, disable_qubit_rewiring=True)
For more information, see the Amazon Braket examples on GitHub, or more specifically, this notebook:
Allocating Qubits on QPU Devices.
59
Amazon Braket Developer Guide
Verbatim compilation
Note
The OQC compiler does not support setting disable_qubit_rewiring=True. Setting this
flag to True yields the following error: An error occurred (ValidationException)
when calling the CreateQuantumTask operation: Device arn:aws:braket:euwest-2::device/qpu/oqc/Lucy does not support disabled qubit rewiring.
Verbatim compilation
When you run a quantum circuit on quantum computers from Rigetti, IonQ, or Oxford Quantum Circuits
(OQC), you can direct the compiler to run your circuits exactly as defined without any modifications.
Using verbatim compilation, you can specify either that an entire circuit be preserved precisely
(supported by Rigetti, IonQ, and OQC) as specified or that only specific parts of it be preserved
(supported by Rigetti only). When developing algorithms for hardware benchmarking or error mitigation
protocols, you need have the option to exactly specify the gates and circuit layouts that you’re running
on the hardware. Verbatim compilation gives you direct control over the compilation process by turning
off certain optimization steps, thereby ensuring that your circuits run exactly as designed.
Verbatim compilation is currently supported on Rigetti, IonQ, and Oxford Quantum Circuits (OQC)
devices and requires the use of native gates. When using verbatim compilation, it is advisable to check
the topology of the device to ensure that gates are called on connected qubits and that the circuit uses
the native gates supported on the hardware. The following example shows how to programmatically
access the list of native gates supported by a device.
device.properties.paradigm.nativeGateSet
For Rigetti, qubit rewiring must be turned off by setting disableQubitRewiring=True for use
with verbatim compilation. If disableQubitRewiring=False is set when using verbatim boxes in a
compilation, the quantum circuit fails validation and does not run.
If verbatim compilation is enabled for a circuit and run on a QPU that does not support it, an error
is generated indicating that an unsupported operation has caused the task to fail. As more quantum
hardware natively support compiler functions, this feature will be expanded to include these devices.
Devices that support verbatim compilation include it as a supported operation when queried with the
following code.
from braket.aws import AwsDevice
from braket.device_schema.device_action_properties import DeviceActionType
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
device.properties.action[DeviceActionType.OPENQASM].supportedPragmas
There is no additional cost associated with using verbatim compilation. You continue to be charged for
quantum tasks executed on Braket QPU devices, notebook instances, and on-demand simulators based
on current rates as specified on the Amazon Braket Pricing page. For more information, see the Verbatim
compilation example notebook.
Note
If you are using OpenQASM to write your circuits for the OQC and IonQ devices, and you wish
to map your circuit directly to the physical qubits, you need to use the #pragma braket
verbatim as the disableQubitRewiring flag is completely ignored by OpenQASM.
Noise simulation
To instantiate the local noise simulator you can change the backend as follows.
device = LocalSimulator(backend="braket_dm")
60
Amazon Braket Developer Guide
Inspecting the circuit
You can build noisy circuits in two ways:
1. Build the noisy circuit from the bottom up.
2. Take an existing, noise-free circuit and inject noise throughout.
The following example shows the approaches using a simple circuit with depolarizing noise and a custom
Kraus channel.
# Bottom up approach
# apply depolarizing noise to qubit 0 with probability of 0.1
circ = Circuit().x(0).x(1).depolarizing(0, probability=0.1)
# create an arbitrary 2-qubit Kraus channel
E0 = scipy.stats.unitary_group.rvs(4) * np.sqrt(0.8)
E1 = scipy.stats.unitary_group.rvs(4) * np.sqrt(0.2)
K = [E0, E1]
# apply a two-qubit Kraus channel to qubits 0 and 2
circ = circ.kraus([0,2], K)
# Inject noise approach
# define phase damping noise
noise = Noise.PhaseDamping(gamma=0.1)
# the noise channel is applied to all the X gates in the circuit
circ = Circuit().x(0).y(1).cnot(0,2).x(1).z(2)
circ_noise = circ.copy()
circ_noise.apply_gate_noise(noise, target_gates = Gate.X)
Running a circuit is the same user experience as before, as shown in the following two examples.
Example 1
task = device.run(circ, s3_location)
Or
Example 2
task = device.run(circ_noise, s3_location)
For more examples, see the Braket introductory noise simulator example
Inspecting the circuit
Quantum circuits in Amazon Braket have a pseudo-time concept called Moments. Each qubit can
experience a single gate per Moment. The purpose of Moments is to make circuits and their gates easier
to address and to provide a temporal structure.
Note
Moments generally do not correspond to the real time at which gates are executed on a QPU.
The depth of a circuit is given by the total number of Moments in that circuit. You can view the circuit
depth calling the method circuit.depth as shown in the following example.
# define a circuit with parametrized gates
circ = Circuit().rx(0, 0.15).ry(1, 0.2).cnot(0,2).zz(1, 3, 0.15).x(0)
print(circ)
61
Amazon Braket Developer Guide
Inspecting the circuit
print('Total circuit depth:', circ.depth)
T : | 0 | 1 |2|
q0 : -Rx(0.15)-C----------X-
 |
q1 : -Ry(0.2)--|-ZZ(0.15)---
 | |
q2 : ----------X-|----------
 |
q3 : ------------ZZ(0.15)---
T : | 0 | 1 |2|
Total circuit depth: 3
The total circuit depth of the circuit above is 3 (shown as moments 0, 1, and 2). You can check the gate
operation for each moment.
Moments functions as a dictionary of key-value pairs.
• The key is MomentsKey(), which contains pseudo-time and qubit information.
• The value is assigned in the type of Instructions().
moments = circ.moments
for key, value in moments.items():
 print(key)
 print(value, "\n")
MomentsKey(time=0, qubits=QubitSet([Qubit(0)]))
Instruction('operator': Rx('angle': 0.15, 'qubit_count': 1), 'target':
 QubitSet([Qubit(0)]))
MomentsKey(time=0, qubits=QubitSet([Qubit(1)]))
Instruction('operator': Ry('angle': 0.2, 'qubit_count': 1), 'target': QubitSet([Qubit(1)]))
MomentsKey(time=1, qubits=QubitSet([Qubit(0), Qubit(2)]))
Instruction('operator': CNot('qubit_count': 2), 'target': QubitSet([Qubit(0), Qubit(2)]))
MomentsKey(time=1, qubits=QubitSet([Qubit(1), Qubit(3)]))
Instruction('operator': ZZ('angle': 0.15, 'qubit_count': 2), 'target': QubitSet([Qubit(1),
 Qubit(3)]))
MomentsKey(time=2, qubits=QubitSet([Qubit(0)]))
Instruction('operator': X('qubit_count': 1), 'target': QubitSet([Qubit(0)]))
You can also add gates to a circuit through Moments.
new_circ = Circuit()
instructions = [Instruction(Gate.S(), 0),
 Instruction(Gate.CZ(), [1,0]),
 Instruction(Gate.H(), 1)
]
new_circ.moments.add(instructions)
print(new_circ)
T : |0|1|2|
q0 : -S-Z---
62
Amazon Braket Developer Guide
Result types
 |
q1 : ---C-HT : |0|1|2|
Result types
Amazon Braket can return different types of results when a circuit is measured using ResultType. A
circuit can return the following types of results.
• AdjointGradient returns the gradient (vector derivative) of the expectation value of a provided
observable. This observable is acting on a provided target with respect to specified parameters using
the adjoint differentiation method. You can only use this method when shots=0.
• Amplitude returns the amplitude of specified quantum states in the output wave function. It is
available on the SV1 and local simulators only.
• Expectation returns the expectation value of a given observable, which can be specified with the
Observable class introduced later in this chapter. The target qubits used to measure the observable
must be specified, and the number of specified targets must equal the number of qubits on which
the observable acts. If no targets are specified, the observable must operate only on 1 qubit and it is
applied to all qubits in parallel.
• Probability returns the probabilities of measuring computational basis states. If no targets are
specified, Probability returns the probability of measuring all basis states. If targets are specified,
only the marginal probabilities of the basis vectors on the specified qubits are returned.
• Reduced density matrix returns a density matrix for a subsystem of specified target qubits from
a system of qubits. To limit the size of this result type, Braket limits the number of target qubits to a
maximum of 8.
• StateVector returns the full state vector. It is available on the local simulator.
• Sample returns the measurement counts of a specified target qubit set and observable. If no targets
are specified, the observable must operate only on 1 qubit and it is applied to all qubits in parallel. If
targets are specified, the number of specified targets must equal the number of qubits on which the
observable acts.
• Variance returns the variance (mean([x-mean(x)]2
)) of the specified target qubit set and
observable as the requested result type. If no targets are specified, the observable must operate only
on 1 qubit and it is applied to all qubits in parallel. Otherwise, the number of targets specified must
equal the number of qubits to which the observable can be applied.
The supported result types for different devices:
Local sim SV1 DM1 TN1 Rigetti IonQ OQC
Adjoint
Gradient
N Y N N N N N
Amplitude Y Y N N N N N
Expectation Y Y Y Y Y Y Y
Probability Y Y Y N Y* Y Y
Reduced
density
matrix
Y N Y N N N N
State
vector
Y N N N N N N
63
Amazon Braket Developer Guide
Result types
Sample Y Y Y Y Y Y Y
Variance Y Y Y Y Y Y Y
Note
* Rigetti only supports probability result types of up to 40 qubits.
You can check the supported result types by examining the device properties, as shown in the following
example.
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
# print the result types supported by this device
for iter in device.properties.action['braket.ir.jaqcd.program'].supportedResultTypes:
 print(iter)
name='Sample' observables=['x', 'y', 'z', 'h', 'i'] minShots=10 maxShots=100000
name='Expectation' observables=['x', 'y', 'z', 'h', 'i'] minShots=10 maxShots=100000
name='Variance' observables=['x', 'y', 'z', 'h', 'i'] minShots=10 maxShots=100000
name='Probability' observables=None minShots=10 maxShots=100000
To call a ResultType, append it to a circuit, as shown in the following example.
from braket.circuits import Observable
circ = Circuit().h(0).cnot(0, 1).amplitude(state=["01", "10"])
circ.probability(target=[0, 1])
circ.probability(target=0)
circ.expectation(observable=Observable.Z(), target=0)
circ.sample(observable=Observable.X(), target=0)
circ.state_vector()
circ.variance(observable=Observable.Z(), target=0)
# print one of the result types assigned to the circuit
print(circ.result_types[0])
Note
Some devices provide measurements (for instance Rigetti) as results and others provide
probabilities as results (for instance IonQ and OQC). The SDK provides a measurements property
on results, but for the devices that return probabilities, it is post-computed. Thus, devices like
those provided by IonQ and OQC have measurement results determined by probability since per
shot measurements are not returned. You can check if a result is post-computed by viewing the
measurements_copied_from_device on the result object as shown in this file.
Observables
Amazon Braket includes an Observable class, which can be used to specify an observable to be
measured.
You can apply at most one unique non-identity observable to each qubit. If you specify two or more
different non-identity observables to the same qubit, you see an error. For this purpose, each factor of a
tensor product counts as an individual observable, so it is permissible to have multiple tensor products
acting on the same qubit, provided that the factor acting on that qubit is the same.
You can also scale an observable and add observables (scaled or not). This creates a Sum which can be
used in the AdjointGradient result type.
The Observable class includes the following observables.
64
Amazon Braket Developer Guide
Result types
Observable.I()
Observable.H()
Observable.X()
Observable.Y()
Observable.Z()
# get the eigenvalues of the observable
print("Eigenvalue:", Observable.H().eigenvalues)
# or whether to rotate the basis to be computational basis
print("Basis rotation gates:",Observable.H().basis_rotation_gates)
# get the tensor product of observable for the multi-qubit case
tensor_product = Observable.Y() @ Observable.Z()
# view the matrix form of an observable by using
print("The matrix form of the observable:\n",Observable.Z().to_matrix())
print("The matrix form of the tensor product:\n",tensor_product.to_matrix())
# also factorize an observable in the tensor form
print("Factorize an observable:",tensor_product.factors)
# self-define observables given it is a Hermitian
print("Self-defined Hermitian:",Observable.Hermitian(matrix=np.array([[0, 1],[1, 0]])))
print("Sum of other (scaled) observables:", 2.0 * Observable.X() @ Observable.X() + 4.0 *
 Observable.Z() @ Observable.Z())
Eigenvalue: [ 1 -1]
Basis rotation gates: (Ry('angle': -0.7853981633974483, 'qubit_count': 1),)
The matrix form of the observable:
 [[ 1.+0.j 0.+0.j]
 [ 0.+0.j -1.+0.j]]
The matrix form of the tensor product:
 [[ 0.+0.j 0.+0.j 0.-1.j 0.-0.j]
 [ 0.+0.j -0.+0.j 0.-0.j 0.+1.j]
 [ 0.+1.j 0.+0.j 0.+0.j 0.+0.j]
 [ 0.+0.j -0.-1.j 0.+0.j -0.+0.j]]
Factorize an observable: (Y('qubit_count': 1), Z('qubit_count': 1))
Self-defined Hermitian: Hermitian('qubit_count': 1, 'matrix': [[0.+0.j 1.+0.j], [1.+0.j 0.
+0.j]])
Sum of other (scaled) observables: Sum(TensorProduct(X('qubit_count': 1), X('qubit_count':
 1)), TensorProduct(Z('qubit_count': 1), Z('qubit_count': 1)))
Parameters
Circuits may include free parameters, which you can be use in a “construct once - run many times”
manner and to compute gradients. Free parameters have a string-encoded name that you can use to
specify their values or to determine whether to differentiate with respect to them.
from braket.circuits import Circuit, FreeParameter, Observable
theta = FreeParameter("theta")
phi = FreeParameter("phi")
circ = Circuit().h(0).rx(0, phi).ry(0, phi).cnot(0, 1).xx(0, 1, theta)
circ.adjoint_gradient(observable=Observable.Z() @ Observable.Z(), target=[0, 1], parameters
 = ["phi", theta]
For the parameters you want to differentiate, specify them either by using their name (as a string) or by
direct reference. Note that computing the gradient using the AdjointGradient result type is done with
respect to the expectation value of the observable.
Note: If you have fixed the values of free parameters by passing them as arguments to the
parameterized circuit, running a circuit with AdjointGradient as a result type and parameters
65
Amazon Braket Developer Guide
Run your circuits with OpenQASM 3.0
specified will produce an error. This is because the parameters we are using to differentiate with are no
longer present. See the following example.
device.run(circ(0.2), shots=0) # will error, as no free parameters will be present
device.run(circ, shots=0, inputs={'phi'=0.2, 'theta'=0.2) # will succeed
Run your circuits with OpenQASM 3.0
Amazon Braket now supports OpenQASM 3.0 for gate-based quantum devices and simulators. This user
guide provides information about the subset of OpenQASM 3.0 supported by Braket. Braket customers
now have the choice of submitting Braket circuits with the SDK (p. 55) or by directly providing
OpenQASM 3.0 strings to all gate-based devices with the Amazon Braket API and the Amazon Braket
Python SDK.
The topics in this guide walk you through various examples of how to complete the following quantum
tasks.
• Create and submit OpenQASM quantum tasks on different Braket devices (p. 71)
• Access the supported operations and result types (p. 79)
• Simulate noise with OpenQASM (p. 81)
• Use verbatim compilation with OpenQASM (p. 83)
• Troubleshoot OpenQASM issues
This guide also provides an introduction to certain hardware-specific features that can be implemented
with OpenQASM 3.0 on Braket and links to further resources.
In this section:
• What is OpenQASM 3.0? (p. 66)
• When to use OpenQASM 3.0 (p. 67)
• How OpenQASM 3.0 works (p. 67)
• Prerequisites (p. 67)
• What OpenQASM features does Braket support? (p. 67)
• Create and submit an example OpenQASM 3.0 quantum task (p. 71)
• Support for OpenQASM on different Braket Devices (p. 73)
• Simulate noise with OpenQASM 3.0 (p. 81)
• Qubit rewiring with OpenQASM 3.0 (p. 82)
• Verbatim Compilation with OpenQASM 3.0 (p. 83)
• The Braket console (p. 83)
• More resources (p. 83)
• Computing gradients with OpenQASM 3.0 (p. 83)
What is OpenQASM 3.0?
The Open Quantum Assembly Language (OpenQASM) is an intermediate representation for quantum
instructions. OpenQASM is an open-source framework and is widely used for the specification of
quantum programs for gate-based devices. With OpenQASM, users can program the quantum gates and
measurement operations that form the building blocks of quantum computation. The previous version of
OpenQASM (2.0) was used by a number of quantum programming libraries to describe simple programs.
66
Amazon Braket Developer Guide
When to use OpenQASM 3.0
The new version of OpenQASM (3.0) extends the previous version to include more features, such as
pulse-level control, gate timing, and classical control flow to bridge the gap between end-user interface
and hardware description language. Details and specification on the current version 3.0 are available
on the GitHub OpenQASM 3.x Live Specification. OpenQASM’s future development is governed by the
OpenQASM 3.0 Technical Steering Committee, of which AWS is a member alongside IBM, Microsoft, and
the University of Innsbruck.
When to use OpenQASM 3.0
OpenQASM provides an expressive framework to specify quantum programs through low-level controls
that are not architecture specific, making it well suited as a representation across multiple gate-based
devices. The Braket support for OpenQASM furthers its adoption as a consistent approach to developing
gate-based quantum algorithms, reducing the need for users to learn and maintain libraries in multiple
frameworks.
If you have existing libraries of programs in OpenQASM 3.0, you can adapt them for use with Braket
rather than completely rewriting these circuits. Researchers and developers should also benefit from
an increasing number of available third-party libraries with support for algorithm development in
OpenQASM.
How OpenQASM 3.0 works
Support for OpenQASM 3.0 from Braket provides feature parity with the current Intermediate
Representation. This means that anything you can do today on hardware devices and on-demand
simulators with Braket, you can do with OpenQASM using the Braket API. You can run OpenQASM
3.0 programs by directly supplying OpenQASM strings to all gate-based devices in a manner that is
similar to how circuits are currently supplied to devices on Braket. Braket users can also integrate thirdparty libraries that support OpenQASM 3.0. The rest of this guide details how to develop OpenQASM
representations for use with Braket.
Prerequisites
To use OpenQASM 3.0 on Amazon Braket, you must have version v1.8.0 of the Amazon Braket Python
Schemas and v1.17.0 or higher of the Amazon Braket Python SDK.
If you are a first time user of Amazon Braket, you need to enable Amazon Braket. For instructions, see
Enable Amazon Braket.
What OpenQASM features does Braket support?
The following section lists the OpenQASM 3.0 data types, statements, and pragma instructions
supported by Braket.
In this section:
• Supported OpenQASM data types (p. 67)
• Supported OpenQASM statements (p. 68)
• Braket OpenQASM pragmas (p. 69)
• Advanced feature support for OpenQASM on the Local Simulator (p. 69)
• Supported operations and grammar with OpenPulse (p. 70)
Supported OpenQASM data types
The following OpenQASM data types are supported by Amazon Braket.
67
Amazon Braket Developer Guide
What OpenQASM features does Braket support?
• Non-negative integers are used for (virtual and physical) qubit indices:
• cnot q[0], q[1];
• h $0;
• Floating-point numbers or constants may be used for gate rotation angles:
• rx(-0.314) $0;
• rx(pi/4) $0;
Note
pi is a built-in constant in OpenQASM and cannot be used as a parameter name.
• Arrays of complex numbers (with the OpenQASM im notation for imaginary part) are allowed in result
type pragmas for defining general hermitian observables and in unitary pragmas:
• #pragma braket unitary [[0, -1im], [1im, 0]] q[0]
• #pragma braket result expectation hermitian([[0, -1im], [1im, 0]]) q[0]
Supported OpenQASM statements
The following OpenQASM statements are supported by Amazon Braket.
• Header: OPENQASM 3;
• Classic bit declarations:
• bit b1; (equivalently, creg b1;)
• bit[10] b2; (equivalently, creg b2[10];)
• Qubit declarations:
• qubit b1; (equivalently, qreg b1;)
• qubit[10] b2; (equivalently, qreg b2[10];)
• Indexing within arrays: q[0]
• Input: input float alpha;
• specification of physical qubits: $0
• Supported gates and operations on a device:
• h $0;
• iswap q[0], q[1];
Note
A device’s supported gates can be found in the device properties for OpenQASM actions; no
gate definitions are needed to use these gates.
• Verbatim box statements. Currently, we do not support box duration notation. Native gates and
physical qubits are required in verbatim boxes.
#pragma braket verbatim
box{
 rx(0.314) $0;
}
• Measurement and measurement assignment on qubits or a whole qubit register.
• measure $0;
• measure q;
68
Amazon Braket Developer Guide
What OpenQASM features does Braket support?
• measure q[0];
• b = measure q;
• measure q # b;
Note
pi is a built-in constant in OpenQASM and cannot be used as a parameter name.
Braket OpenQASM pragmas
The following OpenQASM pragma instructions are supported by Amazon Braket.
• Noise pragmas
• #pragma braket noise bit_flip(0.2) q[0]
• #pragma braket noise phase_flip(0.1) q[0]
• #pragma braket noise pauli_channel
• Verbatim pragmas
• #pragma braket verbatim
• Result type pragmas
• Basis invariant result types:
• State vector: #pragma braket result state_vector
• Density matrix: #pragma braket result density_matrix
• Gradient computation pragmas:
• Adjoint gradient: #pragma braket result adjoint_gradient expectation(2.2 * x[0]
@ x[1]) all
• Z basis result types:
• Amplitude: #pragma braket result amplitude "01"
• Probability: #pragma braket result probability q[0], q[1]
• Basis rotated result types
• Expectation: #pragma braket result expectation x(q[0]) @ y([q1])
• Variance: #pragma braket result variance hermitian([[0, -1im], [1im, 0]]) $0
• Sample: #pragma braket result sample h($1)
Note
OpenQASM 3.0 is backwards compatible with OpenQASM 2.0, so programs written using 2.0
can run on Braket. However the features of OpenQASM 3.0 supported by Braket do have some
minor syntax differences, such as qreg vs creg and qubit vs bit. There are also differences in
measurement syntax, and these need to be supported with their correct syntax.
Advanced feature support for OpenQASM on the Local
Simulator
The LocalSimulator supports advanced OpenQASM features which are not offered as part of
Braket’s QPU’s or on-demand simulators. The following list of features are only supported in the
LocalSimulator:
• Gate modifiers
• OpenQASM built-in gates
• Classical variables
• Classical operations
69
Amazon Braket Developer Guide
What OpenQASM features does Braket support?
• Custom gates
• Classical control
• QASM files
• Subroutines
For examples of each advanced feature, see this sample notebook. For the full OpenQASM specification,
see the OpenQASM website.
Supported operations and grammar with OpenPulse
Supported OpenPulse Data Types
Cal blocks:
cal {
 ...
}
Defcal blocks:
// 1 qubit
defcal x $0 {
...
}
// 1 qubit w. input parameters as constants
defcal my_rx(pi) $0 {
...
}
// 1 qubit w. input parameters as free parameters
defcal my_rz(angle theta) $0 {
...
}
// 2 qubit (above gate args are also valid)
defcal cz $1, $0 {
...
}
Frames:
frame my_frame = newframe(port_0, 4.5e9, 0.0);
Waveforms:
// prebuilt
waveform my_waveform_1 = constant(1e-6, 1.0);
//arbitrary
waveform my_waveform_2 = {0.1 + 0.1im, 0.1 + 0.1im, 0.1, 0.1};
Custom Gate Calibration Example:
cal {
 waveform wf1 = constant(1e-6, 0.25);
}
70
Amazon Braket Developer Guide
Create and submit an example
OpenQASM 3.0 quantum task
defcal my_x $0 {
 play(wf1, q0_rf_frame);
}
defcal my_cz $1, $0 {
 barrier q0_q1_cz_frame, q0_rf_frame;
 play(q0_q1_cz_frame, wf1);
 delay[300ns] q0_rf_frame
 shift_phase(q0_rf_frame, 4.366186381749424);
 delay[300ns] q0_rf_frame;
 shift_phase(q0_rf_frame.phase, 5.916747563126659);
 barrier q0_q1_cz_frame, q0_rf_frame;
 shift_phase(q0_q1_cz_frame, 2.183093190874712);
}
bit[2] ro;
my_x $0;
my_cz $1,$0;
c[0] = measure $0;
Arbitrary pulse example:
bit[2] ro;
cal {
 waveform wf1 = {0.1 + 0.1im, 0.1 + 0.1im, 0.1, 0.1};
 barrier q0_drive, q0_q1_cross_resonance;
 play(q0_q1_cross_resonance, wf1);
 delay[300ns] q0_drive;
 shift_phase(q0_drive, 4.366186381749424);
 delay[300dt] q0_drive;
 barrier q0_drive, q0_q1_cross_resonance;
 play(q0_q1_cross_resonance, wf1);
 ro[0] = capture_v0(r0_measure);
 ro[1] = capture_v0(r1_measure);
}
Create and submit an example OpenQASM 3.0
quantum task
You can use the Amazon Braket Python SDK, Boto3, or the AWS CLI to submit OpenQASM 3.0 quantum
tasks to an Amazon Braket device.
In this section:
• An example OpenQASM 3.0 program (p. 71)
• Use the Python SDK to create OpenQASM 3.0 quantum tasks (p. 72)
• Use Boto3 to create OpenQASM 3.0 quantum tasks (p. 72)
• Use the AWS CLI to create OpenQASM 3.0 tasks (p. 73)
An example OpenQASM 3.0 program
To create a OpenQASM 3.0 task, you can start with a simple OpenQASM 3.0 program (ghz.qasm) that
prepares a GHZ state as shown in the following example.
// ghz.qasm
// Prepare a GHZ state
OPENQASM 3;
71
Amazon Braket Developer Guide
Create and submit an example
OpenQASM 3.0 quantum task
qubit[3] q;
bit[3] c;
h q[0];
cnot q[0], q[1];
cnot q[1], q[2];
c = measure q;
Use the Python SDK to create OpenQASM 3.0 quantum tasks
You can use the Amazon Braket Python SDK to submit this program to an Amazon Braket device with the
following code.
with open("ghz.qasm", "r") as ghz:
 ghz_qasm_string = ghz.read()
# import the device module
from braket.aws import AwsDevice
# choose the Rigetti device
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
from braket.ir.openqasm import Program
program = Program(source=ghz_qasm_string)
my_task = device.run(program)
# You can also specify an optional s3 bucket location and number of shots,
 # if you so choose, when running the program
s3_location = ("amazon-braket-my-bucket", "openqasm-tasks")
my_task = device.run(
 program,
 s3_location,
 shots=100,
)
Use Boto3 to create OpenQASM 3.0 quantum tasks
You can also use AWS Python SDK for Braket (Boto3) to create the quantum tasks using OpenQASM
3.0 strings, as shown in the following example. The following code snippet references ghz.qasm that
prepares a GHZ state as shown above.
import boto3
import json
my_bucket = "amazon-braket-my-bucket"
s3_prefix = "openqasm-tasks"
with open("ghz.qasm") as f:
 source = f.read()
action = {
 "braketSchemaHeader": {
 "name": "braket.ir.openqasm.program",
 "version": "1"
 },
 "source": source
}
device_parameters = {}
device_arn = "arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3"
shots = 100
72
Amazon Braket Developer Guide
Support for OpenQASM on different Braket Devices
braket_client = boto3.client('braket', region_name='us-west-1')
rsp = braket_client.create_quantum_task(
 action=json.dumps(
 action
 ),
 deviceParameters=json.dumps(
 device_parameters
 ),
 deviceArn=device_arn,
 shots=shots,
 outputS3Bucket=my_bucket,
 outputS3KeyPrefix=s3_prefix,
)
Use the AWS CLI to create OpenQASM 3.0 tasks
The AWS Command Line Interface (CLI) can also be used to submit OpenQASM 3.0 programs, as shown
in the following example.
aws braket create-quantum-task \
 --region "us-west-1" \
 --device-arn "arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3" \
 --shots 100 \
 --output-s3-bucket "amazon-braket-my-bucket" \
 --output-s3-key-prefix "openqasm-tasks" \
 --action '{
 "braketSchemaHeader": {
 "name": "braket.ir.openqasm.program",
 "version": "1"
 },
 "source": $(cat ghz.qasm)
 }'
Support for OpenQASM on different Braket Devices
For devices supporting OpenQASM 3.0, the action field supports a new action through the GetDevice
response, as shown in the following example for the Rigetti and IonQ devices.
//OpenQASM as available with the Rigetti device capabilities
{
 "braketSchemaHeader": {
 "name": "braket.device_schema.rigetti.rigetti_device_capabilities",
 "version": "1"
 },
 "service": {...},
 "action": {
 "braket.ir.jaqcd.program": {...},
 "braket.ir.openqasm.program": {
 "actionType": "braket.ir.openqasm.program",
 "version": [
 "1"
 ],
 ….
 }
 }
}
//OpenQASM as available with the IonQ device capabilities
{
 "braketSchemaHeader": {
73
Amazon Braket Developer Guide
Support for OpenQASM on different Braket Devices
 "name": "braket.device_schema.ionq.ionq_device_capabilities",
 "version": "1"
 },
 "service": {...},
 "action": {
 "braket.ir.jaqcd.program": {...},
 "braket.ir.openqasm.program": {
 "actionType": "braket.ir.openqasm.program",
 "version": [
 "1"
 ],
 ….
 }
 }
}
For devices that support pulse control, the pulse field is displayed in the GetDevice response. The
following examples show this pulse field for the Rigetti and OQC devices.
// Rigetti
{
 "pulse": {
 "braketSchemaHeader": {
 "name": "braket.device_schema.pulse.pulse_device_action_properties",
 "version": "1"
 },
 "supportedQhpTemplateWaveforms": {
 "constant": {
 "functionName": "constant",
 "arguments": [
 {
 "name": "length",
 "type": "float",
 "optional": false
 },
 {
 "name": "iq",
 "type": "complex",
 "optional": false
 }
 ]
 },
 ...
 },
 "ports": {
 "q0_ff": {
 "portId": "q0_ff",
 "direction": "tx",
 "portType": "ff",
 "dt": 1e-9,
 "centerFrequencies": [
 375000000
 ]
 },
 ...
 },
 "supportedFunctions": {
 "shift_phase": {
 "functionName": "shift_phase",
 "arguments": [
 {
 "name": "frame",
 "type": "frame",
 "optional": false
74
Amazon Braket Developer Guide
Support for OpenQASM on different Braket Devices
 },
 {
 "name": "phase",
 "type": "float",
 "optional": false
 }
 ]
 },
 ...
 },
 "frames": {
 "q0_q1_cphase_frame": {
 "frameId": "q0_q1_cphase_frame",
 "portId": "q0_ff",
 "frequency": 462475694.24460185,
 "centerFrequency": 375000000,
 "phase": 0,
 "associatedGate": "cphase",
 "qubitMappings": [
 0,
 1
 ]
 },
 ...
 },
 "supportsLocalPulseElements": false,
 "supportsDynamicFrames": false,
 "supportsNonNativeGatesWithPulses": false,
 "validationParameters": {
 "MAX_SCALE": 4,
 "MAX_AMPLITUDE": 1,
 "PERMITTED_FREQUENCY_DIFFERENCE": 400000000
 }
 }
}
// OQC
{
 "pulse": {
 "braketSchemaHeader": {
 "name": "braket.device_schema.pulse.pulse_device_action_properties",
 "version": "1"
 },
 "supportedQhpTemplateWaveforms": {
 "gaussian": {
 "functionName": "gaussian",
 "arguments": [
 {
 "name": "length",
 "type": "float",
 "optional": false
 },
 {
 "name": "sigma",
 "type": "float",
 "optional": false
 },
 {
 "name": "amplitude",
 "type": "float",
 "optional": true
 },
 {
 "name": "zero_at_edges",
 "type": "bool",
75
Amazon Braket Developer Guide
Support for OpenQASM on different Braket Devices
 "optional": true
 }
 ]
 },
 ...
 },
 "ports": {
 "channel_1": {
 "portId": "channel_1",
 "direction": "tx",
 "portType": "port_type_1",
 "dt": 5e-10,
 "qubitMappings": [
 0
 ]
 },
 ...
 },
 "supportedFunctions": {
 "new_frame": {
 "functionName": "new_frame",
 "arguments": [
 {
 "name": "port",
 "type": "port",
 "optional": false
 },
 {
 "name": "frequency",
 "type": "float",
 "optional": false
 },
 {
 "name": "phase",
 "type": "float",
 "optional": true
 }
 ]
 },
 ...
 },
 "frames": {
 "q0_drive": {
 "frameId": "q0_drive",
 "portId": "channel_1",
 "frequency": 5500000000,
 "centerFrequency": 5500000000,
 "phase": 0,
 "qubitMappings": [
 0
 ]
 },
 ...
 },
 "supportsLocalPulseElements": false,
 "supportsDynamicFrames": true,
 "supportsNonNativeGatesWithPulses": true,
 "validationParameters": {
 "MAX_SCALE": 1,
 "MAX_AMPLITUDE": 1,
 "PERMITTED_FREQUENCY_DIFFERENCE": 1,
 "MIN_PULSE_LENGTH": 8e-9,
 "MAX_PULSE_LENGTH": 0.00012
 }
 }
76
Amazon Braket Developer Guide
Support for OpenQASM on different Braket Devices
}
The preceding fields detail the following:
Ports:
Describes pre-made external (extern) device ports declared on the QPU in addition to the associated
properties of the given port. All ports listed in this structure are pre-declared as valid identifiers within
the OpenQASM 3.0 program submitted by the user. The additional properties for a port include:
• Port id (portId)
• The port name declared as an identifier in OpenQASM 3.0.
• Direction (direction)
• The direction of the port. Drive ports transmit pulses (direction “tx”), while measurement ports
receive pulses (direction “rx”).
• Port type (portType)
• The type of action for which this port is responsible (for example, drive, capture, or ff - fast-flux).
• Dt (dt)
• The time in seconds that represents a single sample time step on the given port.
• Qubit mappings (qubitMappings)
• The qubits associated with the given port.
• Center frequencies (centerFrequencies)
• A list of the associated center frequencies for all pre-declared or user-defined frames on the port.
For more information, refer to Frames.
• QHP Specific Properties (qhpSpecificProperties)
• An optional map detailing existing properties about the port specific to the QHP.
Frames:
Describes pre-made external frames declared on the QPU as well as associated properties about the
frames. All frames listed in this structure are pre-declared as valid identifiers within the OpenQASM 3.0
program submitted by the user. The additional properties for a frame include:
• Frame Id (frameId)
• The frame name declared as an identifier in OpenQASM 3.0.
• Port Id (portId)
• The associated hardware port for the frame.
• Frequency (frequency)
• The default initial frequency of the frame.
• Center Frequency (centerFrequency)
• The center of the frequency bandwidth for the frame. Typically, frames may only be adjusted to
a certain bandwidth around the center frequency. As a result, frequency adjustments should stay
within a given delta of the center frequency. You can find the bandwidth value in the validation
parameters.
• Phase (phase)
• The default initial phase of the frame.
• Associated Gate (associatedGate)
• The gates associated with the given frame.
• Qubit Mappings (qubitMappings)
77
Amazon Braket Developer Guide
Support for OpenQASM on different Braket Devices
• The qubits associated with the given frame.
• QHP Specific Properties (qhpSpecificProperties)
• An optional map detailing existing properties about the frame specific to the QHP.
SupportsDynamicFrames:
Describes whether or not a frame can be declared in cal or defcal blocks through the OpenPulse
newframe function. If this is false, only frames listed in the frame structure may be used within the
program.
SupportedFunctions:
Describes the OpenPulse functions that are supported for the device in addition to the associated
arguments, argument types, and return types for the given functions. To see examples of using the
OpenPulse functions, see the OpenPulse specification. At this time, Braket supports:
• shift_phase
• Shifts the phase of a frame by a specified value
• set_phase
• Sets the phase of frame to the specified value
• shift_frequency
• Shifts the frequency of a frame by a specified value
• set_frequency
• Sets the frequency of frame to the specified value
• play
• Schedules a waveform
• capture_v0
• Returns the value on a capture frame to a bit register
SupportedQhpTemplateWaveforms:
Describes the pre-built waveform functions available on the device and the associated arguments and
types. By default, Braket Pulse offers pre-built waveform routines on all devices, which are:
Constant
τ is the length of the waveform and iq is a complex number.
def constant(length, iq)
Gaussian
τ is the length of the waveform, σ is the width of the Gaussian, and A is the amplitude. If setting ZaE
to True, the Gaussian is offset and rescaled such that it is equal to zero at the start and end of the
waveform, and reaches A at maximum.
78
Amazon Braket Developer Guide
Support for OpenQASM on different Braket Devices
def gaussian(length, sigma, amplitude=1, zero_at_edges=False)
DRAG Gaussian
τ is the length of the waveform, σ is the width of the gaussian, β is a free parameter, and A is the
amplitude. If setting ZaE to True, the Derivative Removal by Adiabatic Gate (DRAG) Gaussian is offset
and rescaled such that it is equal to zero at the start and end of the waveform, and the real part reaches
A at maximum. For more information about the DRAG waveform, see the paper Simple Pulses for
Elimination of Leakage in Weakly Nonlinear Qubits.
def drag_gaussian(length, sigma, beta, amplitude=1, zero_at_edges=False)
SupportsLocalPulseElements:
Describes whether or not pulse elements, such as ports, frames, and waveforms may be defined locally in
defcal blocks. If the value is false, elements must be defined in cal blocks.
SupportsNonNativeGatesWithPulses:
Describes whether we can or cannot use non-native gates in combination with pulse programs. For
example, we can’t use a non-native gate like an H gate in a program without first defining the gate
through defcal for the used qubit. You can find the list of native gates nativeGateSet key under the
device capabilities.
ValidationParameters:
Describes pulse element validation boundaries, including:
• Maximum Scale / Maximum Amplitude values for waveforms (arbitrary and pre-built)
• Maximum frequency bandwidth from supplied center frequency in Hz
• Minimum pulse length/duration in seconds
• Maximum pulse length/duration in seconds
Supported Operations, Results and Result Types with
OpenQASM
To find out which OpenQASM 3.0 features each device supports, you can refer to the
braket.ir.openqasm.program key in the action field on the device capabilities output. For
example, the following are the supported operations and result types available for the Braket State
Vector simulator SV1.
...
 "action": {
 "braket.ir.jaqcd.program": {
 ...
 },
"braket.ir.openqasm.program": {
 "version": [
 "1.0"
79
Amazon Braket Developer Guide
Support for OpenQASM on different Braket Devices
 ],
 "actionType": "braket.ir.openqasm.program",
 "supportedOperations": [
 "ccnot",
 "cnot",
 "cphaseshift",
 "cphaseshift00",
 "cphaseshift01",
 "cphaseshift10",
 "cswap",
 "cy",
 "cz",
 "h",
 "i",
 "iswap",
 "pswap",
 "phaseshift",
 "rx",
 "ry",
 "rz",
 "s",
 "si",
 "swap",
 "t",
 "ti",
 "v",
 "vi",
 "x",
 "xx",
 "xy",
 "y",
 "yy",
 "z",
 "zz"
 ],
 "supportedPragmas": [
 "braket_unitary_matrix"
 ],
 "forbiddenPragmas": [],
 "maximumQubitArrays": 1,
 "maximumClassicalArrays": 1,
 "forbiddenArrayOperations": [
 "concatenation",
 "negativeIndex",
 "range",
 "rangeWithStep",
 "slicing",
 "selection"
 ],
 "requiresAllQubitsMeasurement": true,
 "supportsPhysicalQubits": false,
 "requiresContiguousQubitIndices": true,
 "disabledQubitRewiringSupported": false,
 "supportedResultTypes": [
 {
 "name": "Sample",
 "observables": [
 "x",
 "y",
 "z",
 "h",
 "i",
 "hermitian"
 ],
 "minShots": 1,
 "maxShots": 100000
80
Amazon Braket Developer Guide
Simulate noise with OpenQASM 3.0
 },
 {
 "name": "Expectation",
 "observables": [
 "x",
 "y",
 "z",
 "h",
 "i",
 "hermitian"
 ],
 "minShots": 0,
 "maxShots": 100000
 },
 {
 "name": "Variance",
 "observables": [
 "x",
 "y",
 "z",
 "h",
 "i",
 "hermitian"
 ],
 "minShots": 0,
 "maxShots": 100000
 },
 {
 "name": "Probability",
 "minShots": 1,
 "maxShots": 100000
 },
 {
 "name": "Amplitude",
 "minShots": 0,
 "maxShots": 0
 }
 {
 "name": "AdjointGradient",
 "minShots": 0,
 "maxShots": 0
 }
 ]
 }
 },
...
Simulate noise with OpenQASM 3.0
To simulate noise with OpenQASM3, you use pragma instructions to add noise operators. For example,
to simulate the noisy version of the GHZ program (p. 71) provided previously, you can submit the
following OpenQASM program.
// ghz.qasm
// Prepare a GHZ state
OPENQASM 3;
qubit[3] q;
bit[3] c;
h q[0];
#pragma braket noise depolarizing(0.75) q[0] cnot q[0], q[1];
#pragma braket noise depolarizing(0.75) q[0]
81
Amazon Braket Developer Guide
Qubit rewiring with OpenQASM 3.0
#pragma braket noise depolarizing(0.75) q[1] cnot q[1], q[2];
#pragma braket noise depolarizing(0.75) q[0]
#pragma braket noise depolarizing(0.75) q[1]
c = measure q;
Specifications for all supported pragma noise operators are provided in the following list.
#pragma braket noise bit_flip(<float in [0,1/2]>) <qubit>
#pragma braket noise phase_flip(<float in [0,1/2]>) <qubit>
#pragma braket noise pauli_channel(<float>, <float>, <float>) <qubit>
#pragma braket noise depolarizing(<float in [0,3/4]>) <qubit>
#pragma braket noise two_qubit_depolarizing(<float in [0,15/16]>) <qubit>, <qubit>
#pragma braket noise two_qubit_dephasing(<float in [0,3/4]>) <qubit>, <qubit>
#pragma braket noise amplitude_damping(<float in [0,1]>) <qubit>
#pragma braket noise generalized_amplitude_damping(<float in [0,1]> <float in [0,1]>)
 <qubit>
#pragma braket noise phase_damping(<float in [0,1]>) <qubit>
#pragma braket noise kraus([[<complex m0_00>, ], ...], [[<complex m1_00>, ], ...], ...)
 <qubit>[, <qubit>] // maximum of 2 qubits and maximum of 4 matrices for 1 qubit, 16
 for 2
Kraus Operator
In order to generate a Kraus operator, you can iterate through a list of matrices, printing each element of
the matrix as a complex expression.
When using Kraus operators, remember the following:
• The number of qubits must not exceed 2. The current definition in the schemas sets this limit.
• The length of the argument list must be a multiple of 8. This means it must be composed only of 2x2
matrices.
• The total length does not exceed 2
2*num_qubits matrices. This means 4 matrices for 1 qubit and 16 for 2
qubits.
• All supplied matrices are completely positive trace preserving (CPTP).
• The product of the Kraus operators with their transpose conjugates need to add up to an identity
matrix.
Qubit rewiring with OpenQASM 3.0
Amazon Braket supports the physical qubit notation within OpenQASM on Rigetti devices (to learn more
see this page). When using physical qubits with the naive rewiring strategy, ensure that the qubits are
connected on the selected device. Alternatively, if qubit registers are used instead, the PARTIAL rewiring
strategy is enabled by default on Rigetti devices.
// ghz.qasm
// Prepare a GHZ state
OPENQASM 3;
h $0;
cnot $0, $1;
cnot $1, $2;
measure $0;
measure $1;
measure $2;
82
Amazon Braket Developer Guide
Verbatim Compilation with OpenQASM 3.0
Verbatim Compilation with OpenQASM 3.0
When you run a quantum circuit on quantum computers from Rigetti, OQC, and IonQ, you can direct
the compiler to run your circuits exactly as defined, without any modifications. This feature is known
as verbatim compilation. With Rigetti devices, you can specify precisely what gets preserved—either an
entire circuit or only specific parts of it. To preserve only specific parts of a circuit, you’ll need to use
native gates within the preserved regions. Currently, IonQ and OQC only support verbatim compilation
for the entire circuit, so every instruction in the circuit needs to be enclosed in a verbatim box.
With OpenQASM, you can specify a verbatim pragma around a box of code that is untouched and not
optimized by the low-level compilation routine of the hardware. The following code example shows how
to use the #pragma braket verbatim.
OPENQASM 3;
bit[2] c;
#pragma braket verbatim
box{
 rx(0.314159) $0;
 rz(0.628318) $0, $1;
 cz $0, $1;
}
c[0] = measure $0;
c[1] = measure $1;
For more information on verbatim compilation, see the Verbatim compilation sample notebook.
The Braket console
OpenQASM 3.0 tasks are available and can be managed within the Amazon Braket console. On the
console, you have the same experience submitting quantum tasks in OpenQASM 3.0 as you had
submitting existing quantum tasks.
More resources
OpenQASM is available in all Amazon Braket Regions.
For an example notebook for getting started with OpenQASM on Amazon Braket, see Braket Tutorials
GitHub.
Computing gradients with OpenQASM 3.0
Amazon Braket supports computing gradients on both on-demand and local simulators in shots=0
(exact) mode using the adjoint differentiation method. You can provide the appropriate pragma to
specify the gradient you want to compute as shown in the following example.
OPENQASM 3.0;
input float alpha;
bit[2] b;
qubit[2] q;
h q[0];
h q[1];
rx(alpha) q[0];
83
Amazon Braket Developer Guide
Submitting quantum tasks to QPUs and simulators
rx(alpha) q[1];
b[0] = measure q[0];
b[1] = measure q[1];
#pragma braket result adjoint_gradient h(q[0]) @ i(q[1]) alpha
Instead of listing all the parameters individually, you can also specify all in the pragma. This computes
the gradient with respect to all input parameters listed. This can be convenient when the number of
parameters is very large. In this case, the pragma will look like the following example.
#pragma braket result adjoint_gradient h(q[0]) @ i(q[1]) all
All observable types are supported, including individual operators, tensor products, Hermitian
observables, and Sum. The operator you want to use to compute the gradient must be wrapped in the
expectation() encapsulator and the qubits each term acts on must be specified.
Submitting quantum tasks to QPUs and simulators
Amazon Braket provides access to several devices that can run quantum tasks. You can submit quantum
tasks individually or you can set up quantum task batching.
QPUs
You can submit quantum tasks to QPUs at any time, but the task runs within certain availability windows
that are displayed on the Devices page of the Amazon Braket console. You can retrieve the results of the
quantum task with the quantum task ID, which is introduced in the next section.
• IonQ Aria 1 : arn:aws:braket:us-east-1::device/qpu/ionq/Aria-1
• IonQ Harmony : arn:aws:braket:us-east-1::device/qpu/ionq/Harmony
• OQC Lucy : arn:aws:braket:eu-west-2::device/qpu/oqc/Lucy
• QuEra Aquila : arn:aws:braket:us-east-1::device/qpu/quera/Aquila
• Rigetti Aspen-M-3 : arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3
Simulators
• Density matrix simulator, DM1 : arn:aws:braket:::device/quantum-simulator/amazon/dm1
• State vector simulator, SV1 : arn:aws:braket:::device/quantum-simulator/amazon/sv1
• Tensor network simulator, TN1 : arn:aws:braket:::device/quantum-simulator/amazon/
tn1
• The local simulator : LocalSimulator()
Note
You can cancel quantum tasks in the CREATED state for QPUs and on-demand simulators. You
can cancel quantum tasks in the QUEUED state on a best-effort basis for on-demand simulators
and QPUs. Note that QPU QUEUED quantum tasks are unlikely to be cancelled successfully
during QPU availability windows.
In this section:
• Example quantum tasks on Amazon Braket (p. 85)
• Submitting quantum tasks to a QPU (p. 88)
• Running a quantum task with the local simulator (p. 90)
• Quantum task batching (p. 90)
84
Amazon Braket Developer Guide
Example quantum tasks on Amazon Braket
• Set up SNS notifications (optional) (p. 91)
• Inspecting compiled circuits (p. 92)
Example quantum tasks on Amazon Braket
This section walks through the stages of running an example quantum task, from selecting the device to
viewing the result. As a best practice for Amazon Braket, we recommend that you begin by running the
circuit on a simulator, such as SV1.
In this section:
• Specify the device (p. 85)
• Submit an example quantum task (p. 85)
• Submit a parametrized task (p. 86)
• Specify shots (p. 86)
• Poll for results (p. 87)
• View the example results (p. 87)
Specify the device
First, select and specify the device for your quantum task. This example shows how to choose the
simulator, SV1.
# choose the on-demand simulator to run the circuit
from braket.aws import AwsDevice
device = AwsDevice("arn:aws:braket:::device/quantum-simulator/amazon/sv1")
You can view some of the properties of this device as follows:
print (device.name)
for iter in device.properties.action['braket.ir.jaqcd.program']:
 print(iter)
SV1
('version', ['1.0', '1.1'])
('actionType', <DeviceActionType.JAQCD: 'braket.ir.jaqcd.program'>)
('supportedOperations', ['ccnot', 'cnot', 'cphaseshift', 'cphaseshift00', 'cphaseshift01',
 'cphaseshift10', 'cswap', 'cy', 'cz', 'h', 'i', 'iswap', 'pswap', 'phaseshift', 'rx',
 'ry', 'rz', 's', 'si', 'swap', 't', 'ti', 'unitary', 'v', 'vi', 'x', 'xx', 'xy', 'y',
 'yy', 'z', 'zz'])
('supportedResultTypes', [ResultType(name='Sample', observables=['x', 'y', 'z', 'h',
 'i', 'hermitian'], minShots=1, maxShots=100000), ResultType(name='Expectation',
 observables=['x', 'y', 'z', 'h', 'i', 'hermitian'], minShots=0, maxShots=100000),
 ResultType(name='Variance', observables=['x', 'y', 'z', 'h', 'i', 'hermitian'],
 minShots=0, maxShots=100000), ResultType(name='Probability', observables=None, minShots=1,
 maxShots=100000), ResultType(name='Amplitude', observables=None, minShots=0, maxShots=0)])
Submit an example quantum task
Submit an example quantum task to run on the on-demand simulator.
# create a circuit with a result type
circ = Circuit().rx(0, 1).ry(1, 0.2).cnot(0,2).variance(observable=Observable.Z(),
 target=0)
# add another result type
85
Amazon Braket Developer Guide
Example quantum tasks on Amazon Braket
circ.probability(target=[0, 2])
# set up S3 bucket (where results are stored)
my_bucket = "amazon-braket-your-s3-bucket-name" # the name of the bucket
my_prefix = "your-folder-name" # the name of the folder in the bucket
s3_location = (my_bucket, my_prefix)
# submit the quantum task to run
my_task = device.run(circ, s3_location, shots=1000, poll_timeout_seconds = 100,
 poll_interval_seconds = 10)
# the positional argument for the S3 bucket is optional if you want to specify a bucket
 other than the default
# get results of the quantum task
result = my_task.result()
The device.run() command creates a quantum task through the CreateQuantumTask API. After a
short initialization time, the quantum task is queued until capacity exists to run the quantum task on a
device. In this case, the device is SV1. After the device completes the computation, Amazon Braket writes
the results to the Amazon S3 location specified in the call. The positional argument s3_location is
required for all devices except the local simulator.
Note
The Braket quantum task action is limited to 3MB in size.
Submit a parametrized task
Amazon Braket on-demand and local simulators and QPUs also support specifying values of free
parameters at task submission. You can do this by using the inputs argument to device.run(), as
shown in the following example. The inputs must be a dictionary of string-float pairs, where the keys
are the parameter names.
Parametric compilation can improve the performance of executing parametric circuits on certain QPUs.
When submitting a parametric circuit as a quantum task to a supported QPU, Braket will compile the
circuit once, and cache the result. There is no recompilation for subsequent parameter updates to the
same circuit, resulting in faster runtimes for tasks that use the same circuit. Braket automatically uses the
updated calibration data from the hardware provider when compiling your circuit to ensure the highest
quality results.
Note
Parametric compilation is supported on all superconducting, gate-based QPUs from Rigetti
Computing.
from braket.circuits import Circuit, FreeParameter, Observable
# create the free parameters
alpha = FreeParameter('alpha')
beta = FreeParameter('beta')
# create a circuit with a result type
circ = Circuit().rx(0, alpha).ry(1, alpha).cnot(0,2).xx(0, 2, beta)
circ.variance(observable=Observable.Z(), target=0)
# add another result type
circ.probability(target=[0, 2])
# submit the quantum task to run
my_task = device.run(circ, inputs={'alpha': 0.1, 'beta':0.2})
Specify shots
The shots argument refers to the number of desired measurement shots. Simulators such as SV1 support
two simulation modes.
86
Amazon Braket Developer Guide
Example quantum tasks on Amazon Braket
• For shots = 0, the simulator performs an exact simulation, returning the true values for all result types.
(Not available on TN1.)
• For non-zero values of shots, the simulator samples from the output distribution to emulate the shot
noise of real QPUs. QPU devices only allow shots > 0.
For information about the maximum number of shots per quantum task, please refer to Braket
Quotas (p. 23).
Poll for results
When executing my_task.result(), the SDK begins polling for a result with the parameters you
define upon quantum task creation:
• poll_timeout_seconds is the number of seconds to poll the quantum task before it times out
when running the quantum task on the on-demand simulator and or QPU devices. The default value is
432,000 seconds, which is 5 days.
• Note: For QPU devices such as Rigetti and IonQ, we recommend that you allow a few days. If your
polling timeout is too short, results may not be returned within the polling time. For example, when a
QPU is unavailable, a local timeout error is returned.
• poll_interval_seconds is the frequency with which the quantum task is polled. It specifies how
often you call the Braket API to get the status when the quantum task is run on the on-demand
simulator and on QPU devices. The default value is 1 second.
This asynchronous execution facilitates the interaction with QPU devices that are not always available.
For example, a device could be unavailable during a regular maintenance window.
The returned result contains a range of metadata associated with the quantum task. You can check the
measurement result with the following commands:
print('Measurement results:\n',result.measurements)
print('Counts for collapsed states:\n',result.measurement_counts)
print('Probabilities for collapsed states:\n',result.measurement_probabilities)
Measurement results:
 [[1 0 1]
 [0 0 0]
 [1 0 1]
 ...
 [0 0 0]
 [0 0 0]
 [0 0 0]]
Counts for collapsed states:
 Counter({'000': 761, '101': 226, '010': 10, '111': 3})
Probabilities for collapsed states:
 {'101': 0.226, '000': 0.761, '111': 0.003, '010': 0.01}
View the example results
Because you’ve also specified the ResultType, you can view the returned results. The result types
appear in the order in which they were added to the circuit.
print('Result types include:\n', result.result_types)
print('Variance=',result.values[0])
print('Probability=',result.values[1])
# you can plot the result and do some analysis
87
Amazon Braket Developer Guide
Submitting quantum tasks to a QPU
import matplotlib.pyplot as plt
plt.bar(result.measurement_counts.keys(), result.measurement_counts.values());
plt.xlabel('bitstrings');
plt.ylabel('counts');
Result types include:
 [ResultTypeValue(type={'observable': ['z'], 'targets': [0], 'type': 'variance'},
 value=0.7062359999999999), ResultTypeValue(type={'targets': [0, 2], 'type':
 'probability'}, value=array([0.771, 0. , 0. , 0.229]))]
Variance= 0.7062359999999999
Probability= [0.771 0. 0. 0.229]
Submitting quantum tasks to a QPU
Amazon Braket allows you to run a quantum circuit on a QPU device. The following example shows how
to submit a quantum task to Rigetti or IonQ devices.
Choose the Rigetti Aspen-M-3 device, then look at the associated connectivity graph
# import the QPU module
from braket.aws import AwsDevice
# choose the Rigetti device
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
# take a look at the device connectivity graph
device.properties.dict()['paradigm']['connectivity']
{'fullyConnected': False,
 'connectivityGraph': {'0': ['1', '7'],
 '1': ['0', '16'],
88
Amazon Braket Developer Guide
Submitting quantum tasks to a QPU
 '2': ['3', '15'],
 '3': ['2', '4'],
 '4': ['3', '5'],
 '5': ['4', '6'],
 '6': ['5', '7'],
 '7': ['0', '6'],
 '11': ['12', '26'],
 '12': ['13', '11'],
 '13': ['12', '14'],
 '14': ['13', '15'],
 '15': ['2', '14', '16'],
 '16': ['1', '15', '17'],
 '17': ['16'],
 '20': ['21', '27'],
 '21': ['20', '36'],
 '22': ['23', '35'],
 '23': ['22', '24'],
 '24': ['23', '25'],
 '25': ['24', '26'],
 '26': ['11', '25', '27'],
 '27': ['20', '26'],
 '30': ['31', '37'],
 '31': ['30', '32'],
 '32': ['31', '33'],
 '33': ['32', '34'],
 '34': ['33', '35'],
 '35': ['22', '34', '36'],
 '36': ['21', '35', '37'],
 '37': ['30', '36']}}
The preceding dictionary connectivityGraph contains information about the connectivity of the
current Rigetti device.
Choose the IonQ Harmony device
For the IonQ Harmony device, the connectivityGraph is empty, as shown in the following example,
because the device offers all-to-all connectivity. Therefore, a detailed connectivityGraph is not
needed.
# or choose the IonQ Harmony device
device = AwsDevice("arn:aws:braket:us-east-1::device/qpu/ionq/Harmony")
# take a look at the device connectivity graph
device.properties.dict()['paradigm']['connectivity']
{'fullyConnected': True, 'connectivityGraph': {}}
As shown in the following example, you have the option to adjust the shots (default=1000), the
poll_timeout_seconds (default = 432000 = 5 days), the poll_interval_seconds (default = 1),
and the location of the S3 bucket (s3_location) where your results will be stored if you choose to
specify a location other than the default bucket.
my_task = device.run(circ, s3_location = 'amazon-braket-my-folder', shots=100,
 poll_timeout_seconds = 100, poll_interval_seconds = 10)
The IonQ and Rigetti devices compile the provided circuit into their respective native gate sets
automatically, and they map the abstract qubit indices to physical qubits on the respective QPU.
Note
QPU devices have limited capacity. You can expect longer wait times when capacity is reached.
89
Amazon Braket Developer Guide
Running a quantum task with the local simulator
Amazon Braket can run QPU quantum tasks within certain availability windows, but you can still submit
quantum tasks any time (24/7) because all corresponding data and metadata are stored reliably in
the appropriate S3 bucket. As shown in the next section, you can recover your quantum task using
AwsQuantumTask and your unique quantum task ID.
Running a quantum task with the local simulator
You can send quantum tasks directly to a local simulator for rapid prototyping and testing. This
simulator runs in your local environment, so you do not need to specify an Amazon S3 location. The
results are computed directly in your session. To run a quantum task on the local simulator, you must
only specify the shots parameter.
Note
The execution speed and maximum number of qubits the local simulator can process depends
on the Amazon Braket notebook instance type, or on your local hardware specifications.
The following commands are all identical and instantiate the state vector (noise free) local simulator.
# import the LocalSimulator module
from braket.devices import LocalSimulator
# the following are identical commands
device = LocalSimulator()
device = LocalSimulator("default")
device = LocalSimulator(backend="default")
device = LocalSimulator(backend="braket_sv")
Then run a quantum task with the following.
my_task = device.run(circ, shots=1000)
To instantiate the local density matrix (noise) simulator customers change the backend as follows.
# import the LocalSimulator module
from braket.devices import LocalSimulator
device = LocalSimulator(backend="braket_dm")
Quantum task batching
Quantum task batching is available on every Amazon Braket device, except the local simulator. Batching
is especially useful for quantum tasks you run on the on-demand simulators (TN1 or SV1) because they
can process multiple quantum tasks in parallel. To help you set up various quantum tasks, Amazon
Braket provides example notebooks.
Batching allows you to launch quantum tasks in parallel. For example, if you wish to make a calculation
that requires 10 quantum tasks and the circuits in those quantum tasks are independent of each other,
it is a good idea to use batching. That way, you don’t have to wait for one quantum task to be complete
before another task begins.
The following example shows how to run a batch of quantum tasks:
circuits = [bell for _ in range(5)]
batch = device.run_batch(circuits, s3_folder, shots=100)
print(batch.results()[0].measurement_counts) # The result of the first quantum task in the
 batch
For more information, see the Amazon Braket examples on GitHub or Quantum task batching, which has
more specific information about batching.
90
Amazon Braket Developer Guide
Set up SNS notifications (optional)
About quantum task batching and costs
A few caveats to keep in mind regarding quantum task batching and billing costs:
• By default, quantum task batching retries all time out or fail quantum tasks 3 times.
• A batch of long running quantum tasks, such as 34 qubits for SV1, can incur large costs. Be sure to
double check the run_batch assignment values carefully before you start a batch of quantum tasks.
We do not recommend using TN1 with run_batch.
• TN1 can incur costs for failed rehearsal phase tasks (see the TN1 description for more information).
Automatic retries can add to the cost and so we recommend setting the number of 'max_retries' on
batching to 0 when using TN1 (see Quantum Task Batching, Line 186).
Quantum task batching and PennyLane
Take advantage of batching when you’re using PennyLane on Amazon Braket by setting parallel =
True when you instantiate an Amazon Braket device, as shown in the following example.
device = qml.device("braket.aws.qubit",device_arn="arn:aws:braket:::device/quantumsimulator/amazon/sv1",wires=wires,s3_destination_folder=s3_folder,parallel=True,)
For more information about batching with PennyLane, see Parallelized optimization of quantum circuits.
Task batching and parametrized circuits
When submitting a quantum task batch that contains parametrized circuits, you can either provide an
inputs dictionary, which is used for all quantum tasks in the batch, or a list of input dictionaries, in
which case the i-th dictionary is paired with the i-th task, as shown in the following example.
from braket.circuits import Circuit, FreeParameter, Observable
from braket.aws import AwsQuantumTaskBatch
# create the free parameters
alpha = FreeParameter('alpha')
beta = FreeParameter('beta')
# create two circuits
circ_a = Circuit().rx(0, alpha).ry(1, alpha).cnot(0,2).xx(0, 2, beta)
circ_a.variance(observable=Observable.Z(), target=0)
circ_b = Circuit().rx(0, alpha).rz(1, alpha).cnot(0,2).zz(0, 2, beta)
circ_b.expectation(observable=Observable.Z(), target=2)
# use the same inputs for both circuits in one batch
tasks = device.run_batch([circ_a, circ_b], inputs={'alpha': 0.1, 'beta':0.2})
# or provide each task its own set of inputs
inputs_list = [{'alpha': 0.3,'beta':0.1}, {'alpha': 0.1,'beta':0.4}]
tasks = device.run_batch([circ_a, circ_b], inputs=inputs_list)
Set up SNS notifications (optional)
You can set up notifications through the Amazon Simple Notification Service (SNS) so that you receive an
alert when your Amazon Braket quantum task is complete. Active notifications are useful if you expect a
91
Amazon Braket Developer Guide
Inspecting compiled circuits
long wait time; for example, when you submit a large quantum task or when you submit a quantum task
outside of a device’s availability window. If you do not want to wait for the quantum task to complete,
you can set up an SNS notification.
An Amazon Braket notebook walks you through the setup steps. For more information, see the Amazon
Braket examples on GitHub and, specifically, the example notebook for setting up notifications.
Inspecting compiled circuits
When a circuit runs on a hardware device, it must be compiled in an acceptable format such as
transpiling the circuit down to the native gates that are supported by the QPU. Inspecting the actual
compiled output can be very useful for debugging purposes. You can view this circuit, which is stored in
the object named compiledProgram, for both Rigetti and OQC devices using the code below.
task = AwsQuantumTask(arn=task_id, aws_session=session)
# after task finished
task_result = task.result()
# For Rigetti
compiledProgram = task_result.additional_metadata.rigettiMetadata.compiledProgram
# For OQC
compiledProgram = task_result.additional_metadata.oqcMetadata.compiledProgram
Note
Today you cannot view your compiled circuit for IonQ devices.
Submit an analog program using QuEra’s Aquila
This page provides a comprehensive documentation about the capabilities of the Aquila machine from
QuEra. Details covered here are the following: 1) The parameterized Hamiltonian simulated by Aquila, 2)
AHS program parameters, 3) AHS result content, 4) Aquila capabilities parameter. We suggest using Ctrl
+F text search to find parameters relevant to your questions.
Hamiltonian
The Aquila machine from QuEra simulates the following (time-dependent) Hamiltonian natively:
where
• Hdrive,k(t)=( 1
/2 Ω(t)e
iϕ(t)
S−,k + 1
/2 Ω(t)e
−iϕ(t)
 S+,k) + (−Δglobal(t)nk),
• Ω(t) is the time-dependent, global driving amplitude (aka Rabi frequency), in units of (rad / us)
• ϕ(t) is the time-dependent, global phase, measured in radians
• S−,k and S+,k are the spin lowering and raising operators of atom k (in the basis |#⟩=|g⟩, |#⟩=|r⟩, they
are S−=|g⟩⟨r|, S+=(S−)
†
=|r⟩⟨g|)
• Δglobal(t) is the time-dependent, global detuning
• nk is the projection operator on the Rydberg state of atom k (i.e. n=|r⟩⟨r|)
• Vvdw,k,l=C6/(dk,l)
6
nknl
,
• C6 is the van der Waals coefficient, in units of (rad / s) * (m)^6
• dk,l is the Euclidean distance between atom k and l, measured in um.
92
Amazon Braket Developer Guide
Braket AHS program schema
The users have control over the following parameters via the Braket AHS program schema.
• 2-d atom arrangement (xk and yk coordinates of each atom k, in units of um), which controls the
pairwise atomic distances dk,l with k,l=1,2,…N
• Ω(t), the time-dependent, global Rabi frequency, in units of (rad / s)
• ϕ(t), the time-dependent, global phase, in units of (rad / s)
• Δglobal(t), the time-dependent, global detuning, in units of (rad / s)
Note
The user cannot control which levels are involved (i.e. S−,S+,n operators are fixed) nor the
strength of the Rydberg-Rydberg interaction coefficient (C6).
Braket AHS program schema
braket.ir.ahs.program_v1.Program object (example)
Program(
 braketSchemaHeader=BraketSchemaHeader(
 name='braket.ir.ahs.program',
 version='1'
 ),
 setup=Setup(
 ahs_register=AtomArrangement(
 sites=[[Decimal('0'), Decimal('0')]],
 filling=[1]
 )
 ),
 hamiltonian=Hamiltonian(
 drivingFields=[
 DrivingField(
 amplitude=PhysicalField(
 time_series=TimeSeries(
 values=[Decimal('0'), Decimal('15700000.0')],
 times=[Decimal('0'), Decimal('0.000001')]
 ),
 pattern='uniform'
 ),
 phase=PhysicalField(
 time_series=TimeSeries(
 values=[Decimal('0'), Decimal('0')],
 times=[Decimal('0'), Decimal('0.000001')]
 ),
 pattern='uniform'
 ),
 detuning=PhysicalField(
 time_series=TimeSeries(
 values=[Decimal('-54000000.0'), Decimal('54000000.0')],
 times=[Decimal('0'), Decimal('0.000001')]
 ),
 pattern='uniform'
 )
 )
 ],
 shiftingFields=[]
 )
)
JSON (example)
{
93
Amazon Braket Developer Guide
Braket AHS program schema
 "braketSchemaHeader": {
 "name": "braket.ir.ahs.program",
 "version": "1"
 },
 "setup": {
 "ahs_register": {
 "sites": [[0E-7, 0E-7]],
 "filling": [1]
 }
 },
 "hamiltonian": {
 "drivingFields": [
 {
 "amplitude": {
 "time_series": {
 "values": [0.0, 15700000.0],
 "times": [0E-9, 0.000001000]
 },
 "pattern": "uniform"
 },
 "phase": {
 "time_series": {
 "values": [0E-7, 0E-7],
 "times": [0E-9, 0.000001000]
 },
 "pattern": "uniform"
 },
 "detuning": {
 "time_series": {
 "values": [-54000000.0, 54000000.0],
 "times": [0E-9, 0.000001000]
 },
 "pattern": "uniform"
 }
 }
 ],
 "shiftingFields": []
 }
}
Main fields
Program field type description
setup.ahs_register.sites List[List[Decimal]] List of 2-d
coordinates where
the tweezers trap
atoms
setup.ahs_register.filling List[int] Marks atoms that
occupy the trap sites
with 1, and empty
sites with 0
hamiltonian.drivingFields[].amplitude.time_series.times List[Decimal] time points of
driving amplitude,
Omega(t)
hamiltonian.drivingFields[].amplitude.time_series.values List[Decimal] values of driving
amplitude, Omega(t)
hamiltonian.drivingFields[].amplitude.pattern str spatial pattern of
driving amplitude,
94
Amazon Braket Developer Guide
Braket AHS task result schema
Program field type description
Omega(t); must be
'uniform'
hamiltonian.drivingFields[].phase.time_series.times List[Decimal] time points of
driving phase, phi(t)
hamiltonian.drivingFields[].phase.time_series.values List[Decimal] values of driving
phase, phi(t)
hamiltonian.drivingFields[].phase.pattern str spatial pattern of
driving phase, phi(t);
must be 'uniform'
hamiltonian.drivingFields[].detuning.time_series.times List[Decimal] time points of
driving detuning,
Delta_global(t)
hamiltonian.drivingFields[].detuning.time_series.values List[Decimal] values of driving
detuning,
Delta_global(t)
hamiltonian.drivingFields[].detuning.pattern str spatial pattern of
driving detuning,
Delta_global(t); must
be 'uniform'
hamiltonian.shiftingFields List must be empty
Metadata fields
Program field type description
braketSchemaHeader.name str name of the schema; must be
'braket.ir.ahs.program'
braketSchemaHeader.version str version of the schema
Braket AHS task result schema
braket.tasks.analog_hamiltonian_simulation_quantum_task_result.AnalogHamiltonianSimulationQuantumTaskRe(example)
AnalogHamiltonianSimulationQuantumTaskResult(
 task_metadata=TaskMetadata(
 braketSchemaHeader=BraketSchemaHeader(
 name='braket.task_result.task_metadata',
 version='1'
 ),
 id='arn:aws:braket:us-east-1:123456789012:quantum-task/12345678-90abcdef-1234-567890abcdef',
 shots=2,
 deviceId='arn:aws:braket:us-east-1::device/qpu/quera/Aquila',
 deviceParameters=None,
 createdAt='2022-10-25T20:59:10.788Z',
 endedAt='2022-10-25T21:00:58.218Z',
 status='COMPLETED',
95
Amazon Braket Developer Guide
Braket AHS task result schema
 failureReason=None
 ),
 measurements=[
 ShotResult(
 status=<AnalogHamiltonianSimulationShotStatus.SUCCESS: 'Success'>,
 pre_sequence=array([1, 1, 1, 1]),
 post_sequence=array([0, 1, 1, 1])
 ),
 ShotResult(
 status=<AnalogHamiltonianSimulationShotStatus.SUCCESS: 'Success'>,
 pre_sequence=array([1, 1, 0, 1]),
 post_sequence=array([1, 0, 0, 0])
 )
 ]
)
JSON (example)
{
 "braketSchemaHeader": {
 "name": "braket.task_result.analog_hamiltonian_simulation_task_result",
 "version": "1"
 },
 "taskMetadata": {
 "braketSchemaHeader": {
 "name": "braket.task_result.task_metadata",
 "version": "1"
 },
 "id": "arn:aws:braket:us-east-1:123456789012:quantum-task/12345678-90abcdef-1234-567890abcdef",
 "shots": 2,
 "deviceId": "arn:aws:braket:us-east-1::device/qpu/quera/Aquila",
 "createdAt": "2022-10-25T20:59:10.788Z",
 "endedAt": "2022-10-25T21:00:58.218Z",
 "status": "COMPLETED"
 },
 "measurements": [
 {
 "shotMetadata": {"shotStatus": "Success"},
 "shotResult": {
 "preSequence": [1, 1, 1, 1],
 "postSequence": [0, 1, 1, 1]
 }
 },
 {
 "shotMetadata": {"shotStatus": "Success"},
 "shotResult": {
 "preSequence": [1, 1, 0, 1],
 "postSequence": [1, 0, 0, 0]
 }
 }
 ],
 "additionalMetadata": {
 "action": {...}
 "queraMetadata": {
 "braketSchemaHeader": {
 "name": "braket.task_result.quera_metadata",
 "version": "1"
 },
 "numSuccessfulShots": 100
96
Amazon Braket Developer Guide
Braket AHS task result schema
 }
 }
}
Main fields
Task result field type description
measurements[].shotResult.preSequence List[int] Pre-sequence measurement bits
(one for each atomic site) for each
shot: 0 if site is empty, 1 if site
is filled, measured before the
sequences of pulses that run the
quantum evolution
measurements[].shotResult.postSequence List[int] Post-sequence measurement
bits for each shot: 0 if atom is in
Rydberg state or site is empty, 1 if
atom is in ground state, measured
at the end of the sequences of
pulses that run the quantum
evolution
Metadata fields
Task result field type description
braketSchemaHeader.name str name of the
schema; must be
'braket.task_result.analog_hambraketSchemaHeader.version str version of the
schema
taskMetadata.braketSchemaHeader.name str name of the
schema; must be
‘braket.task_result.task_metadataskMetadata.braketSchemaHeader.version str version of the
schema
taskMetadata.id str The ID of
the quantum
task. For AWS
quantum tasks,
this is the
quantum task
ARN.
taskMetadata.shots int The number of
shots for the
quantum task
taskMetadata.shots.deviceId str The ID of the
device on which
the quantum
task ran. For
AWS devices,
97
Amazon Braket Developer Guide
Braket AHS task result schema
Task result field type description
this is the device
ARN.
taskMetadata.shots.createdAt str The timestamp
of creation; the
format must be
in ISO-8601/
RFC3339
string format
YYYY-MMDDTHH:mm:ss.sssZ.
Default is None.
taskMetadata.shots.endedAt str The timestamp
of when the
quantum task
ended; the
format must be
in ISO-8601/
RFC3339
string format
YYYY-MMDDTHH:mm:ss.sssZ.
Default is None.
taskMetadata.shots.status str The status of
the quantum
task (CREATED,
QUEUED,
RUNNING,
COMPLETED,
FAILED). Default
is None.
taskMetadata.shots.failureReason str The failure
reason of the
quantum task.
Default is None.
additionalMetadata.action braket.ir.ahs.program_v1.Program (See the Braket
AHS program
schema (p. 93)
section)
additionalMetadata.action.braketSchemaHeaderstr .queraMetadata.name name of the
schema; must be
'braket.task_result.quera_metaadditionalMetadata.action.braketSchemaHeaderstr .queraMetadata.version version of the
schema
additionalMetadata.action.numSuccessfulShots int number of
completely
successful shots;
must be equal
to the requested
number of shots
98
Amazon Braket Developer Guide
QuEra device properties schema
Task result field type description
measurements[].shotMetadata.shotStatus int The status of the
shot, (Success,
Partial success,
Failure); must be
"Success"
QuEra device properties schema
braket.device_schema.quera.quera_device_capabilities_v1.QueraDeviceCapabilities (example)
QueraDeviceCapabilities(
 service=DeviceServiceProperties(
 braketSchemaHeader=BraketSchemaHeader(
 name='braket.device_schema.device_service_properties',
 version='1'
 ),
 executionWindows=[
 DeviceExecutionWindow(
 executionDay=<ExecutionDay.TUESDAY: 'Tuesday'>,
 windowStartHour=datetime.time(16, 0),
 windowEndHour=datetime.time(20, 0)
 )
 ],
 shotsRange=(1, 1000),
 deviceCost=DeviceCost(
 price=0.01,
 unit='shot'
 ),
 deviceDocumentation=
 DeviceDocumentation(
 imageUrl='https://
a.b.cdn.console.awsstatic.com/59534b58c709fc239521ef866db9ea3f1aba73ad3ebcf60c23914ad8c5c5c878/
a6cfc6fca26cf1c2e1c6.png',
 summary='Analog quantum processor based on neutral atom arrays',
 externalDocumentationUrl='https://www.quera.com/aquila'
 ),
 deviceLocation='Boston, USA',
 updatedAt=datetime.datetime(2022, 10, 24, 15, 45, tzinfo=datetime.timezone.utc)
 ),
 action={
 <DeviceActionType.AHS: 'braket.ir.ahs.program'>: DeviceActionProperties(
 version=['1'],
 actionType=<DeviceActionType.AHS: 'braket.ir.ahs.program'>
 )
 },
 deviceParameters={},
 braketSchemaHeader=BraketSchemaHeader(
 name='braket.device_schema.quera.quera_device_capabilities',
 version='1'
 ),
 paradigm=QueraAhsParadigmProperties(
 braketSchemaHeader=BraketSchemaHeader(
 name='braket.device_schema.quera.quera_ahs_paradigm_properties',
 version='1'
 ),
 qubitCount=256,
 lattice=Lattice(
 area=Area(
 width=Decimal('0.000075'),
99
Amazon Braket Developer Guide
QuEra device properties schema
 height=Decimal('0.0001')
 ),
 geometry=Geometry(
 spacingRadialMin=Decimal('0.000004'),
 spacingVerticalMin=Decimal('0.000004'),
 positionResolution=Decimal('1E-7'),
 numberSitesMax=256
 )
 ),
 rydberg=Rydberg(
 c6Coefficient=Decimal('5.42E-24'),
 rydbergGlobal=RydbergGlobal(
 rabiFrequencyRange=(Decimal('0.0'), Decimal('15800000.0')),
 rabiFrequencyResolution=Decimal('400.0'),
 rabiFrequencySlewRateMax=Decimal('250000000000000.0'),
 detuningRange=(Decimal('-125000000.0'), Decimal('125000000.0')),
 detuningResolution=Decimal('0.2'),
 detuningSlewRateMax=Decimal('2500000000000000.0'),
 phaseRange=(Decimal('-99.0'), Decimal('99.0')),
 phaseResolution=Decimal('5E-7'),
 timeResolution=Decimal('1E-9'),
 timeDeltaMin=Decimal('1E-8'),
 timeMin=Decimal('0.0'),
 timeMax=Decimal('0.000004')
 )
 ),
 performance=Performance(
 lattice=PerformanceLattice(
 positionErrorAbs=Decimal('1E-7')
 ),
 rydberg=PerformanceRydberg(
 rydbergGlobal=PerformanceRydbergGlobal(
 rabiFrequencyErrorRel=Decimal('0.02')
 )
 )
 )
 )
)
JSON (example)
{
 "service": {
 "braketSchemaHeader": {
 "name": "braket.device_schema.device_service_properties",
 "version": "1"
 },
 "executionWindows": [
 {
 "executionDay": "Tuesday",
 "windowStartHour": "16:00:00",
 "windowEndHour": "20:00:00"
 }
 ],
 "shotsRange": [1, 1000],
 "deviceCost": {
 "price": 0.01,
 "unit": "shot"
 },
 "deviceDocumentation": {
 "imageUrl": "https://
a.b.cdn.console.awsstatic.com/59534b58c709fc239521ef866db9ea3f1aba73ad3ebcf60c23914ad8c5c5c878/
a6cfc6fca26cf1c2e1c6.png",
 "summary": "Analog quantum processor based on neutral atom arrays",
100
Amazon Braket Developer Guide
QuEra device properties schema
 "externalDocumentationUrl": "https://www.quera.com/aquila"
 },
 "deviceLocation": "Boston, USA",
 "updatedAt": "2022-10-24T15:45:00+00:00"
 },
 "action": {
 "braket.ir.ahs.program": {
 "version": ["1"],
 "actionType": "braket.ir.ahs.program"
 }
 },
 "deviceParameters": {},
 "braketSchemaHeader": {
 "name": "braket.device_schema.quera.quera_device_capabilities",
 "version": "1"
 },
 "paradigm": {
 "braketSchemaHeader": {
 "name": "braket.device_schema.quera.quera_ahs_paradigm_properties",
 "version": "1"
 },
 "qubitCount": 256,
 "lattice": {
 "area": {
 "width": 7.5e-05,
 "height": 0.0001
 },
 "geometry": {
 "spacingRadialMin": 4e-06,
 "spacingVerticalMin": 4e-06,
 "positionResolution": 1e-07,
 "numberSitesMax": 256
 }
 },
 "rydberg": {
 "c6Coefficient": 5.42e-24,
 "rydbergGlobal": {
 "rabiFrequencyRange": [0.0,15800000.0],
 "rabiFrequencyResolution": 400.0,
 "rabiFrequencySlewRateMax": 250000000000000.0,
 "detuningRange": [-125000000.0, 125000000.0],
 "detuningResolution": 0.2,
 "detuningSlewRateMax": 2500000000000000.0,
 "phaseRange": [-99.0, 99.0],
 "phaseResolution": 5e-07,
 "timeResolution": 1e-09,
 "timeDeltaMin": 1e-08,
 "timeMin": 0.0,
 "timeMax": 4e-06
 }
 },
 "performance": {
 "lattice": {
 "positionErrorAbs": 1e-07
 },
 "rydberg": {
 "rydbergGlobal": {
 "rabiFrequencyErrorRel": 0.02
 }
 }
 }
 }
}
101
Amazon Braket Developer Guide
QuEra device properties schema
Capabilities fields
Task result field type description
paradigm.qubitCount int the number of
qubits
paradigm.lattice.area.width Decimal Largest allowed
difference
between x
coordinates of
any two sites
(measured in
meters)
paradigm.lattice.area.height Decimal Largest allowed
difference
between y
coordinates of
any two sites
(measured in
meters)
paradigm.lattice.geometry.spacingRadialMin Decimal Minimum radial
spacing between
any two sites
in the lattice
(measured in
meters)
paradigm.lattice.geometry.spacingVerticalMin Decimal Minimum spacing
between any two
rows in the lattice
(measured in
meters)
paradigm.lattice.geometry.positionResolution Decimal Resolution
with which site
positions can
be specified
(measured in
meters)
paradigm.lattice.geometry.numberSitesMax int Maximum number
of sites that can
be placed in the
lattice
paradigm.rydberg.c6Coefficient Decimal Rydberg-Rydberg
C6 interaction
coefficient
(measured in (rad/
s)*m^6)
paradigm.rydberg.rydbergGlobal.rabiFrequencyRange Tuple[Decimal,
Decimal]
Achievable Rabi
frequency range
for the global
Rydberg drive time
102
Amazon Braket Developer Guide
QuEra device properties schema
Task result field type description
series (measured
in rad/s)
paradigm.rydberg.rydbergGlobal.rabiFrequencyResolution Decimal Resolution with
which global
Rabi frequency
amplitude can
be specified
(measured in rad/
s)
paradigm.rydberg.rydbergGlobal.rabiFrequencySlewRateMax Decimal Maximum slew
rate for changing
the global
Rabi frequency
(measured in (rad/
s)/s)
paradigm.rydberg.rydbergGlobal.detuningRange Tuple[Decimal,
Decimal]
Achievable
detuning range
for the global
Rydberg pulse
(measured in rad/
s)
paradigm.rydberg.rydbergGlobal.detuningResolution Decimal Resolution with
which global
detuning can
be specified
(measured in rad/
s)
paradigm.rydberg.rydbergGlobal.detuningSlewRateMax Decimal Maximum slew
rate for detuning
(measured in (rad/
s)/s)
paradigm.rydberg.rydbergGlobal.phaseRange Tuple[Decimal,
Decimal]
Achievable phase
range for the
global Rydberg
pulse (measured in
rad)
paradigm.rydberg.rydbergGlobal.phaseResolution Decimal Resolution with
which global Rabi
frequency phase
can be specified
(measured in rad)
paradigm.rydberg.rydbergGlobal.timeResolution Decimal Resolution with
which times for
global Rydberg
drive parameters
can be specified
(measured in s)
103
Amazon Braket Developer Guide
QuEra device properties schema
Task result field type description
paradigm.rydberg.rydbergGlobal.timeDeltaMin Decimal Minimum time
step with which
times for global
Rydberg drive
parameters can
be specified
(measured in s)
paradigm.rydberg.rydbergGlobal.timeMin Decimal Minimum duration
of Rydberg drive
(measured in s)
paradigm.rydberg.rydbergGlobal.timeMax Decimal Maximum duration
of Rydberg drive
(measured in s)
Performance fields
Task result field type description
paradigm.peformance.lattice.positionErrorAbs Decimal Error between
target and actual
site position
(measured in
meters)
paradigm.peformance.rydberg.rydbergGlobal.rabiFrequencyErrorRel Decimal random error
in the Rabi
frequency, relative
(unitless)
Service properties fields
Task result field type description
service.executionWindows[].executionDay ExecutionDay Days of the execution
window; must be 'Everyday',
'Weekdays', 'Weekend',
'Monday', 'Tuesday',
'Wednesday', Thursday',
'Friday', 'Saturday' or
'Sunday'
service.executionWindows[].windowStartHour datetime.time UTC 24-hour format of the
time when the execution
window starts
service.executionWindows[].windowEndHour datetime.time UTC 24-hour format of the
time when the execution
window ends
service.qpu_capabilities.service.shotsRange Tuple[int, int] Minimum and maximum
number of shots for the
device
104
Amazon Braket Developer Guide
Monitoring and tracking quantum tasks
Task result field type description
service.qpu_capabilities.service.deviceCost.price float Price of the device in terms
of US dollars
service.qpu_capabilities.service.deviceCost.unit str unit for charging the price,
e.g: 'minute', 'hour', 'shot',
'task'
Metadata fields
Task result field type description
paradigm.braketSchemaHeader.name str name of the
schema; must be
'braket.device_schema.quera.quera_ahparadigm.braketSchemaHeader.version str version of the schema
action[].version str version of the AHS
program schema
action[].actionType ActionType AHS program schema
name; must be
'braket.ir.ahs.program'
service.braketSchemaHeader.name str name of the
schema; must be
'braket.device_schema.device_service_service.braketSchemaHeader.version str version of the schema
service.deviceDocumentation.imageUrl str URL for the image of
the device
service.deviceDocumentation.summary str brief description on the
device
service.deviceDocumentation.externalDocumentationUrl str external documentation
URL
service.deviceLocation str geographic location fo
the device
service.updatedAt datetime time when the device
properties were last
updated
Monitoring and tracking quantum tasks
After you submit a quantum task, you can keep track of its status through the Amazon Braket SDK
and console. When the quantum task completes, Braket saves the results in your specified Amazon S3
location. Completion may take some time, especially for QPU devices, depending on the length of the
queue. Status types include:
• CREATED – Amazon Braket received your quantum task.
105
Amazon Braket Developer Guide
Tracking quantum tasks from the Amazon Braket SDK
• QUEUED – Amazon Braket processed your quantum task and it is now waiting to run on the device.
• RUNNING – Your quantum task is running on a QPU or on-demand simulator.
• COMPLETED – Your quantum task finished running on the QPU or on-demand simulator.
• FAILED – Your quantum task attempted to run and failed. Depending on the reason your quantum
task failed, try submitting your quantum task again.
• CANCELLED – You cancelled the quantum task. The quantum task didn't run.
In this section:
• Tracking quantum tasks from the Amazon Braket SDK (p. 106)
• Advanced logging (p. 107)
• Monitoring quantum tasks through the Amazon Braket console (p. 109)
Tracking quantum tasks from the Amazon Braket SDK
The command device.run(…) defines a quantum task with a unique quantum task ID. You can query
and track the status with task.state() as shown in the following example.
Note: task = device.run() is an asynchronous operation, which means that you can keep working
while the system processes your quantum task in the background.
Retrieve a result
When you call task.result(), the SDK begins polling Amazon Braket to see whether the quantum
task is complete. The SDK uses the polling parameters you defined in .run(). After the quantum task
is complete, the SDK retrieves the result from the S3 bucket and returns it as a QuantumTaskResult
object.
# create a circuit, specify the device and run the circuit
circ = Circuit().rx(0, 0.15).ry(1, 0.2).cnot(0,2)
device = AwsDevice("arn:aws:braket:::device/quantum-simulator/amazon/sv1")
task = device.run(circ, s3_location, shots=1000)
# get ID and status of submitted task
task_id = task.id
status = task.state()
print('ID of task:', task_id)
print('Status of task:', status)
# wait for job to complete
while status != 'COMPLETED':
 status = task.state()
 print('Status:', status)
ID of task:
arn:aws:braket:us-west-2:123412341234:quantum-task/b68ae94b-1547-4d1d-aa92-1500b82c300d
Status of task: QUEUED
Status: QUEUED
Status: QUEUED
Status: QUEUED
Status: QUEUED
Status: QUEUED
Status: QUEUED
Status: QUEUED
Status: RUNNING
Status: RUNNING
Status: COMPLETED
106
Amazon Braket Developer Guide
Advanced logging
Cancel a quantum task
To cancel a quantum task, call the cancel() method, as shown in the following example.
# cancel quantum task
task.cancel()
status = task.state()
print('Status of task:', status)
Status of task: CANCELLING
Check the metadata
You can check the metadata of the finished quantum task, as shown in the following example.
# get the metadata of the quantum task
metadata = task.metadata()
# example of metadata
shots = metadata['shots']
date = metadata['ResponseMetadata']['HTTPHeaders']['date']
# print example metadata
print("{} shots taken on {}.".format(shots, date))
# print name of the s3 bucket where the result is saved
results_bucket = metadata['outputS3Bucket']
print('Bucket where results are stored:', results_bucket)
# print the s3 object key (folder name)
results_object_key = metadata['outputS3Directory']
print('S3 object key:', results_object_key)
# the entire look-up string of the saved result data
look_up = 's3://'+results_bucket+'/'+results_object_key
print('S3 URI:', look_up)
1000 shots taken on Wed, 05 Aug 2020 14:44:22 GMT.
Bucket where results are stored: amazon-braket-123412341234
S3 object key: simulation-output/b68ae94b-1547-4d1d-aa92-1500b82c300d
S3 URI: s3://amazon-braket-123412341234/simulation-output/b68ae94b-1547-4d1daa92-1500b82c300d
Retrieve a quantum task or result
If your kernel dies after you submit the quantum task or if you close your notebook or computer, you can
reconstruct the task object with its unique ARN (quantum task ID). Then you can call task.result()
to get the result from the S3 bucket where it is stored.
from braket.aws import AwsSession, AwsQuantumTask
# restore task with unique arn
task_load = AwsQuantumTask(arn=task_id)
# retrieve the result of the task
result = task_load.result()
Advanced logging
You can record the whole task-processing process using a logger. These advanced logging techniques
allow you to see the background polling and create a record for later debugging.
107
Amazon Braket Developer Guide
Advanced logging
To use the logger, we recommend changing the poll_timeout_seconds and
poll_interval_seconds parameters, so that a quantum task can be long-running and the quantum
task status is logged continuously, with results saved to a file. You can transfer this code to a Python
script instead of a Jupyter notebook, so that the script can run as a process in the background.
Configure the logger
First, configure the logger so that all logs are written into a text file automatically, as shown in the
following example lines.
# import the module
import logging
from datetime import datetime
# set filename for logs
log_file = 'device_logs-'+datetime.strftime(datetime.now(), '%Y%m%d%H%M%S')+'.txt'
print('Task info will be logged in:', log_file)
# create new logger object
logger = logging.getLogger("newLogger")
# configure to log to file device_logs.txt in the appending mode
logger.addHandler(logging.FileHandler(filename=log_file, mode='a'))
# add to file all log messages with level DEBUG or above
logger.setLevel(logging.DEBUG)
Task info will be logged in: device_logs-20200803203309.txt
Create and run the circuit
Now you can create a circuit, submit it to a device to run, and see what happens as shown in this
example.
# define circuit
circ_log = Circuit().rx(0, 0.15).ry(1, 0.2).rz(2, 0.25).h(3).cnot(control=0,
 target=2).zz(1, 3, 0.15).x(4)
print(circ_log)
# define backend
device = AwsDevice("arn:aws:braket:::device/quantum-simulator/amazon/sv1")
# define what info to log
logger.info(
 device.run(circ_log, s3_location,
 poll_timeout_seconds=1200, poll_interval_seconds=0.25, logger=logger,
 shots=1000)
 .result().measurement_counts
)
Check the log file
You can check what is written into the file by entering the following command.
# print logs
! cat {log_file}
Task arn:aws:braket:us-west-2:123412341234:quantumtask/5088ec6c-89cf-4338-9750-9f5bb12a0dc4: start polling for completion
Task arn:aws:braket:us-west-2:123412341234:quantumtask/5088ec6c-89cf-4338-9750-9f5bb12a0dc4: task status CREATED
108
Amazon Braket Developer Guide
Monitoring quantum tasks through
the Amazon Braket console
Task arn:aws:braket:us-west-2:123412341234:quantumtask/5088ec6c-89cf-4338-9750-9f5bb12a0dc4: task status CREATED
Task arn:aws:braket:us-west-2:123412341234:quantumtask/5088ec6c-89cf-4338-9750-9f5bb12a0dc4: task status QUEUED
Task arn:aws:braket:us-west-2:123412341234:quantumtask/5088ec6c-89cf-4338-9750-9f5bb12a0dc4: task status RUNNING
Task arn:aws:braket:us-west-2:123412341234:quantumtask/5088ec6c-89cf-4338-9750-9f5bb12a0dc4: task status RUNNING
Task arn:aws:braket:us-west-2:123412341234:quantumtask/5088ec6c-89cf-4338-9750-9f5bb12a0dc4: task status COMPLETED
Counter({'00001': 493, '00011': 493, '01001': 5, '10111': 4, '01011': 3, '10101': 2})
Get the ARN from the log file
From the log file output that’s returned, as shown in the previous example, you can obtain the ARN
information. With the ARN ID, you can retrieve the result of the completed quantum task.
# parse log file for arn
with open(log_file) as openfile:
 for line in openfile:
 for part in line.split():
 if "arn:" in part:
 arn = part
 break
# remove final semicolon in logs
arn = arn[:-1]
# with this arn you can restore again task from unique arn
task_load = AwsQuantumTask(arn=arn, aws_session=AwsSession())
# get results of task
result = task_load.result()
Monitoring quantum tasks through the Amazon
Braket console
Amazon Braket offers a convenient way of monitoring the quantum task through the Amazon Braket
console. All submitted quantum tasks are listed in the Quantum Tasks field as shown in the following
figure. This service is Region-specific, which means that you can only view those quantum tasks created in
the specific AWS Region.
109
Amazon Braket Developer Guide
Monitoring quantum tasks through
the Amazon Braket console
You can search for particular quantum tasks through the navigation bar. The search can be based on
Quantum Task ARN (ID), status, device, and creation time. The options appear automatically when you
select the navigation bar, as shown in the following example.
The following image shows an example of searching for a quantum task based on its unique quantum
task ID, which can be obtained by calling task.id.
Additionally, seen in the figure below, the status of a quantum task can be monitored while it is in a
QUEUED state. Clicking on the quantum task ID shows the details page. This page displays the dynamic
queue position for your quantum task relative to the device it will process on.
Quantum tasks submitted as part of a hybrid job will have priority when in queue. Quantum tasks
submitted outside of a hybrid job will have normal queuing priority.
Customers wishing to query the Braket SDK, can obtain their quantum task and hybrid job queue
positions programmatically. For more information see the When will my task run (p. 33) page.
110
Amazon Braket Developer Guide
Working with Boto3
Working with Boto3
Boto3 is the AWS SDK for Python. With Boto3, Python developers can create, configure, and manage
AWS services, such as Amazon Braket. Boto3 provides an object-oriented API, as well as low-level access
to Amazon Braket.
Follow the instructions in the Boto3 Quickstart guide to learn how to install and configure Boto3.
Boto3 provides the core functionality that works along with the Amazon Braket Python SDK to help you
configure and run your quantum tasks. Python customers always need to install Boto3, because that is
the core implementation. If you want to make use of additional helper methods, you also need to install
the Amazon Braket SDK.
For example, when you call CreateQuantumTask, the Amazon Braket SDK submits the request to
Boto3, which then calls the AWS API.
In this section:
• Turn on the Amazon Braket Boto3 client (p. 111)
• Configure AWS CLI profiles for Boto3 and the Amazon Braket SDK (p. 114)
Turn on the Amazon Braket Boto3 client
To use Boto3 with Amazon Braket, you must import Boto3 and then define a client that you use to
connect to the Amazon Braket API. In the following example, the Boto3 client is named braket.
Note
For backwards compatibility with older versions of BraketSchemas, OpenQASM information is
omitted from GetDevice API calls. To get this information, the user-agent needs to present
a recent version of the BraketSchemas (1.8.0 or later). The Braket SDK automatically reports
this for you. If you do not see OpenQASM results in the GetDevice response when using a
Braket SDK, you may need to set the AWS_EXECUTION_ENV environment variable to configure
the user-agent. See the code examples provided in the GetDevice does not return OpenQASM
results error (p. 194) topic for how to do this for the AWS CLI, Boto3, and the Go, Java, and
JavaScript/TypeScript SDKs.
import boto3
import botocore
braket = boto3.client("braket",
 config=botocore.client.Config(user_agent_extra="BraketSchemas/1.8.0"))
Now that you have a braket client established, you can make requests and process responses from the
Amazon Braket service. You can get more detail on request and response data in the API Reference.
The following examples show how to work with devices and quantum tasks.
• Search for devices (p. 112)
• Retrieve a device (p. 112)
• Create a quantum task (p. 112)
• Retrieve a quantum task (p. 113)
• Search for quantum tasks (p. 113)
• Cancel quantum task (p. 113)
111
Amazon Braket Developer Guide
Turn on the Amazon Braket Boto3 client
Search for devices
• search_devices(**kwargs)
Search for devices using the specified filters.
# Pass search filters and optional parameters when sending the
# request and capture the response
response = braket.search_devices(filters=[{
 'name': 'deviceArn',
 'values': ['arn:aws:braket:::device/quantum-simulator/amazon/sv1']
}], maxResults=10)
print(f"Found {len(response['devices'])} devices")
for i in range(len(response['devices'])):
 device = response['devices'][i]
 print(device['deviceArn'])
Retrieve a device
• get_device(deviceArn)
Retrieve the devices available in Amazon Braket.
# Pass the device ARN when sending the request and capture the repsonse
response = braket.get_device(deviceArn='arn:aws:braket:::device/quantum-simulator/amazon/
sv1')
print(f"Device {response['deviceName']} is {response['deviceStatus']}")
Create a quantum task
• create_quantum_task(**kwargs)
Create a quantum task.
# Create parameters to pass into create_quantum_task()
kwargs = {
 # Create a Bell pair
 'action': '{"braketSchemaHeader": {"name": "braket.ir.jaqcd.program", "version": "1"},
 "results": [], "basis_rotation_instructions": [], "instructions": [{"type": "h", "target":
 0}, {"type": "cnot", "control": 0, "target": 1}]}',
 # Specify the SV1 Device ARN
 'deviceArn': 'arn:aws:braket:::device/quantum-simulator/amazon/sv1',
 # Specify 2 qubits for the Bell pair
 'deviceParameters': '{"braketSchemaHeader": {"name":
 "braket.device_schema.simulators.gate_model_simulator_device_parameters",
 "version": "1"}, "paradigmParameters": {"braketSchemaHeader": {"name":
 "braket.device_schema.gate_model_parameters", "version": "1"}, "qubitCount": 2}}',
 # Specify where results should be placed when the quantum task completes.
 # You must ensure the S3 Bucket exists before calling create_quantum_task()
 'outputS3Bucket': 'amazon-braket-examples',
 'outputS3KeyPrefix': 'boto-examples',
 # Specify number of shots for the quantum task
 'shots': 100
}
112
Amazon Braket Developer Guide
Turn on the Amazon Braket Boto3 client
# Send the request and capture the response
response = braket.create_quantum_task(**kwargs)
print(f"Quantum task {response['quantumTaskArn']} created")
Retrieve a quantum task
• get_quantum_task(quantumTaskArn)
Retrieve the specified quantum task.
# Pass the quantum task ARN when sending the request and capture the response
response = braket.get_quantum_task(quantumTaskArn='arn:aws:braket:uswest-1:123456789012:quantum-task/ce78c429-cef5-45f2-88da-123456789012')
print(response['status'])
Search for quantum tasks
• search_quantum_tasks(**kwargs)
Search for quantum tasks that match the specified filter values.
# Pass search filters and optional parameters when sending the
# request and capture the response
response = braket.search_quantum_tasks(filters=[{
 'name': 'deviceArn',
 'operator': 'EQUAL',
 'values': ['arn:aws:braket:::device/quantum-simulator/amazon/sv1']
}], maxResults=25)
print(f"Found {len(response['quantumTasks'])} quantum tasks")
for n in range(len(response['quantumTasks'])):
 task = response['quantumTasks'][n]
 print(f"Quantum task {task['quantumTaskArn']} for {task['deviceArn']} is
 {task['status']}")
Cancel quantum task
• cancel_quantum_task(quantumTaskArn)
Cancel the specified quantum task.
# Pass the quantum task ARN when sending the request and capture the response
response = braket.cancel_quantum_task(quantumTaskArn='arn:aws:braket:uswest-1:123456789012:quantum-task/ce78c429-cef5-45f2-88da-123456789012')
print(f"Quantum task {response['quantumTaskArn']} is {response['cancellationStatus']}")
113
Amazon Braket Developer Guide
Configure AWS CLI profiles for
Boto3 and the Amazon Braket SDK
Configure AWS CLI profiles for Boto3 and the
Amazon Braket SDK
The Amazon Braket SDK relies upon the default AWS CLI credentials, unless you explicitly specify
otherwise. We recommend that you keep the default when you run on a managed Amazon Braket
notebook because you must provide an IAM role that has permissions to launch the notebook instance.
Optionally, if you run your code locally (on an Amazon EC2 instance, for example), you can establish
named AWS CLI profiles. You can give each profile a different permission set, rather than regularly
overwriting the default profile.
This section provides a brief explanation of how to configure such a CLI profile and how to incorporate
that profile into Amazon Braket so that API calls are made with the permissions from that profile.
In this section:
• Step 1: Configure a local AWS CLIprofile (p. 114)
• Step 2: Establish a Boto3 session object (p. 114)
• Step 3: Incorporate the Boto3 session into the Braket AwsSession (p. 114)
Step 1: Configure a local AWS CLIprofile
It is beyond the scope of this document to explain how to create a user and how to configure a nondefault profile. For information on these topics, see:
• Getting started
• Configuring the AWS CLI to use AWS IAM Identity Center
To use Amazon Braket, you must provide this user — and the associated CLI profile — with the
necessary Braket permissions. For instance, you can attach the AmazonBraketFullAccess policy.
Step 2: Establish a Boto3 session object
from boto3 import Session
# Insert CLI profile name here
boto_sess = Session(profile_name=`profile`)
Note
If the expected API calls have Region-based restrictions that are not aligned with your profile
default Region, you can specify a Region for the Boto3 session as shown in the following
example.
# Insert CLI profile name _and_ region
boto_sess = Session(profile_name=`profile`, region_name=`region`)
For the argument designated as region, substitute a value that corresponds to one of the AWS Regions
in which Amazon Braket is available such as us-east-1, us-west-1, and so forth.
Step 3: Incorporate the Boto3 session into the Braket
AwsSession
The following example shows how to initialize a Boto3 Braket session and instantiate a device in that
session.
114
Amazon Braket Developer Guide
Configure AWS CLI profiles for
Boto3 and the Amazon Braket SDK
from braket.aws import AwsSession, AwsDevice
# Initialize Braket session with Boto3 Session credentials
aws_session = AwsSession(boto_session=boto_sess)
# Instantiate any Braket QPU device with the previously initiated AwsSession
sim_arn = 'arn:aws:braket:::device/quantum-simulator/amazon/sv1'
device = AwsDevice(sim_arn, aws_session=aws_session)
After this setup is complete, you can submit quantum tasks to that instantiated AwsDevice object (by
calling the device.run(…) command for example). All API calls made by that device can leverage the
IAM credentials associated with the CLI profile that you previously designated as profile.
115
Amazon Braket Developer Guide
Braket Pulse
Pulse control on Amazon Braket
This section explains how to use pulse control on various QPUs in Amazon Braket.
In this section:
• Braket Pulse (p. 116)
• Roles of frames and ports (p. 117)
• Hello Pulse (p. 119)
• Accessing native gates using pulses (p. 122)
• Hello Pulse using OpenPulse (p. 123)
Braket Pulse
Pulses are the analog signals that control the qubits in a quantum computer. With certain devices on
Amazon Braket, you can access the pulse control feature to submit circuits using pulses. You can access
pulse control through the Braket SDK, using OpenQASM 3.0, or directly through the Braket APIs. First,
let’s introduce some key concepts for pulse control in Braket.
Frames
A frame is a software abstraction that acts as both a clock within the quantum program and a phase.
The clock time is incremented on each usage and a stateful carrier signal that is defined by a frequency.
When transmitting signals to the qubit, a frame determines the qubit’s carrier frequency, phase offset,
and the time at which the waveform envelope is emitted. In Braket Pulse, constructing frames depends
on the device, frequency, and phase. Depending on the device, you can either choose a predefined frame
or instantiate new frames by providing a port.
from braket.pulse import Frame
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
drive_frame = device.frames["q0_rf_frame"]
device = AwsDevice("arn:aws:braket:eu-west-2::device/qpu/oqc/Lucy")
readout_frame = Frame(name="r0_measure", port=port0, frequency=5e9, phase=0)
Ports
A port is a software abstraction representing any input/output hardware component controlling qubits.
It helps hardware vendors provide an interface with which users can interact to manipulate and observe
qubits. Ports are characterized by a single string that represents the name of the connector. This string
also exposes a minimum time increment that specifies how finely we can define the waveforms.
from braket.pulse import Port
Port0 = Port("channel_0", dt=1e-9)
Waveforms
A waveform is a time-dependent envelope that we can use to emit signals on an output port or capture
signals through an input port. You can specify your waveforms directly either through a list of complex
numbers or by using a waveform template to generate a list from the hardware provider.
116
Amazon Braket Developer Guide
Roles of frames and ports
from braket.pulse import ArbitraryWaveform, ConstantWaveform
cst_wfm = ConstantWaveform(length=1e-7, iq=0.1)
arb_wf = ArbitraryWaveform(amplitudes=np.linspace(0, 100))
Braket Pulse provides a standard library of waveforms, including a constant waveform, a Gaussian
waveform, and a Derivative Removal by Adiabatic Gate (DRAG) waveform. You can retrieve the waveform
data through the sample function to draw the shape of the waveform as shown in the following
example.
gaussian_waveform = GaussianWaveform(1e-7, 25e-9, 0.1)
x = np.arange(0, gaussian_waveform.length, drive_frame.port.dt)
plt.plot(x, gaussian_waveform.sample(drive_frame.port.dt))
The preceding image depicts the Gaussian waveforms created from GaussianWaveform. We chose a
pulse length of 100 ns, a width of 25 ns, and an amplitude of 0.1 (arbitrary units). The waveforms are
centered in the pulse window. GaussianWaveform accepts a boolean argument zero_at_edges (ZaE
in the legend). When set to True, this argument offsets the Gaussian waveform such that the points at
t=0 and t=length are at zero and rescales its amplitude such that the maximum value corresponds to
the amplitude argument.
Now that we have covered the basic concepts for pulse-level access, next we’ll see how to construct a
circuit using gates and pulses.
Roles of frames and ports
This section describes the predefined frames and ports available for each device. We will also briefly
discuss the mechanisms involved when pulses are played on certain frames.
117
Amazon Braket Developer Guide
Rigetti
Rigetti
Frames
Rigetti devices support predefined frames that have their frequency and phase calibrated to be on
resonance with the associated qubit. The naming convention is q{i}[_q{j}]_{role}_frame where
{i} refers to the first qubit number, {j} refers to the second qubit number in case the frame serves to
activate a two-qubit interaction, and {role} refers to the role of the frame. The roles are as follows:
• rf is the frame to drive the 0-1 transition of the qubit. Pulses are transmitted as microwave transient
signals of frequency and phase previously provided through the set and shift functions. The timedependent amplitude of the signal is given by the waveform played on the frame. The frame plugs a
single-qubit, off-diagonal interaction. For more information, see Krantz et al. and Rahamim et al..
• rf_f12 is similar to rf and its parameters target the 1-2 transition.
• ro_rx is used to achieve dispersive readout of the qubit through a coupled coplanar waveguide. The
frequency, phase, and full set of parameters for the readout waveform are precalibrated. It is currently
used via the capture_v0, which does not require any argument besides the frame identifier.
• ro_tx is for transmitting signals from the resonator. It is currently unused.
• cz is a frame calibrated to enable the two-qubit cz gate. As with all the frames associated with an ff
port, it turns on an entangling interaction through the flux line by modulating the tunable qubit of
the pair on resonance with its neighbor. For more information about the entangling mechanism, see
Reagor et al., Caldwell et al., and Didier et al..
• cphase is a frame calibrated to enable the two-qubit cphaseshift gate and is linked to an ff port.
For more information about the entangling mechanism, see the description for the cz frame.
• xy is a frame calibrated to enable the two-qubit XY(θ) gates and is linked to an ff port. For more
information about the entangling mechanism and how to achieve XY gates, see the description for the
cz frame and Abrams et al..
As frames based on the ff port shift the frequency of the tunable qubit, all the other driving frames
related to the qubit will be dephased by an amount that is related to the amplitude and the duration of
the frequency shift. Consequently, you must compensate for this effect by adding a corresponding phase
shift to the frames of the neighboring qubits.
Ports
The Rigetti devices provide a list of ports that you can inspect through the device capabilities. Port
names follow the convention q{i}_{type} where {i} refers to the qubit number and {type} refers to
the type of the port. Note that not all of the qubits have a complete set of ports. The types of ports are
as follows:
• rf represents the main interface to drive the single-qubit transition. It is associated with the rf and
rf_f12 frames. It is capacitively coupled to the qubit, allowing microwave driving in the gigahertz
range.
• ro_tx serves to transmit signals to the readout resonator capacitively coupled to the qubit. Readout
signal delivery is multiplexed eight-fold by octagon.
• ro_rx serves to receive signals from the readout resonator coupled to the qubit.
• ff represents the fast-flux line inductively coupled to the qubit. We can use this to tune the frequency
of the transmon. Only qubits designed to be highly tunable have an ff port. This port serves
to activate qubit-qubit interaction as there is a static capacitive coupling between each pair of
neighboring transmons.
For more information about the architecture, see Valery et al..
118
Amazon Braket Developer Guide
OQC
OQC
Frames
OQC devices support predefined frames that have their frequency and phase calibrated to be on
resonance with the associated qubit. The naming convention for these frames is as follows:
• driving frame: q{i}[_q{j}]_{role} where {i} refers to the first qubit number, {j} refers to the
second qubit number in case the frame serves to activate a two-qubit interaction, and {role} refers
to the role of the frame as described below.
• qubit readout frame: r{i}_{role} where {i} refers to the qubit number and {role} refers to the
role of the frame as described below.
We recommend using each frame for its designed role as follows:
• drive is used as the main frame to drive the 0-1 transition of the qubit. Pulses are transmitted as
microwave transient signals of frequency and phase previously provided through the set and shift
functions. The time-dependent amplitude of the signal is given by the waveform played on the frame.
The frame plugs a single-qubit, off-diagonal interaction. For more information, see Krantz et al. and
Rahamim et al..
• second_state is equivalent to the drive frame but its frequency is tuned on resonance with the 1-2
transition.
• measure is for readout. The frequency, phase, and full set of parameters for the readout waveform
are precalibrated. It is currently used through the capture_v0, which does not require any argument
besides the frame identifier.
• acquire is for capturing signals from the resonator. It is currently unused.
• cross_resonance activates the cross resonance interaction between the qubits i and j by
driving the control qubit i at the transition frequency of the target qubit j. Consequently, the
frame frequency is set using the frequency of the target qubit. The interaction occurs with a rate
proportional to the amplitude of this cross-resonant drive. Different types of crosstalks induces
unwanted effects which requires corrections. See Patterson et al. for more information about the
cross-resonance interaction with coaxially-shaped transmon qubits (‘coaxmons’).
• cross_resonance_cancellation helps you add corrections to suppress deleterious effects induced
by crosstalks when the cross-resonance interaction is activated. The initial frame frequency is set to
the transition frequency of the control qubit i. For more information about the cancellation method,
see Patterson et al..
Ports
The OQC devices provide a list of ports that you can inspect through the device capabilities. The
previously described frames are associated with ports that are identified by their id channel_{N} where
{N} is an integer. Ports are the interface to control lines (direction tx) and readout resonators (direction
rx) connected to coaxmons. Each qubit is associated to one control line and one readout resonator. The
transmission port is the interface for single-qubit and two-qubit manipulation. The reception port serves
for qubit readout.
Hello Pulse
Here, you will learn how to construct a simple Bell pair directly with pulses, and execute this pulse
program on the Rigetti device. A Bell pair is a two-qubit circuit consisting of a Hadamard gate on the
first qubit followed by a cnot gate between the first and second qubits. Creating entangled states with
pulses requires specific mechanisms that are dependent on the hardware type and device architecture.
We will not use a native mechanism to create the cnot gate. Instead, we’ll use specific waveforms and
119
Amazon Braket Developer Guide
Hello Pulse
frames that enable the cz gate natively. In this example, we will create a Hadamard gate using the
single-qubit native gates rx and rz and express the cz gate using pulses.
First, let’s import the necessary libraries. In addition to the Circuit class, you will now also need to
import the PulseSequence class.
from braket.aws import AwsDevice
from braket.pulse import PulseSequence, ArbitraryWaveform, GaussianWaveform
from braket.circuits import Circuit
import braket.circuits.circuit as circuit
Next, instantiate a new Braket device using the Amazon Resource Name (ARN) of the Rigetti Aspen-M-3
device. Refer to the Devices page on the Amazon Braket console to view the layout of the Rigetti AspenM-3 device.
a=10 #specifies the control qubit
b=113 #specifies the target qubit
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
As the Hadamard gate is not a native gate of the Rigetti device, it cannot be used in combination with
pulses. You therefore need to decompose it into a sequence of the rx and rz native gates.
import numpy as np
import matplotlib.pyplot as plt
@circuit.subroutine(register=True)
def rigetti_native_h(q0):
 return (
 Circuit()
 .rz(q0, np.pi)
 .rx(q0, np.pi/2)
 .rz(q0, np.pi/2)
 .rx(q0, -np.pi/2)
 )
For the cz gate, we will use an arbitrary waveform with parameters (amplitude, rise/fall time, and
duration) that have been predetermined by the hardware provider during a calibration stage. This
waveform will be applied on the q10_q113_cz_frame. For a more recent version of the arbitrary
waveform used here, see QCS, on the Rigetti website. You may be required to create a QCS account.
a_b_cz_wfm = ArbitraryWaveform([0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
 0.00017888439538396808, 0.00046751103636033026, 0.0011372942989106456,
 0.002577059611929697, 0.005443941944632366, 0.010731922770068104, 0.01976701723583167,
 0.03406712171899736, 0.05503285980691202, 0.08350670755829034, 0.11932853352131022,
 0.16107456696238298, 0.20614055551722368, 0.2512065440720643, 0.292952577513137,
 0.328774403476157, 0.3572482512275353, 0.3782139893154499, 0.3925140937986156,
 0.40154918826437913, 0.4068371690898149, 0.4097040514225177, 0.41114381673553674,
 0.411813599998087, 0.4121022266390633, 0.4122174383870584, 0.41226003881132406,
 0.4122746298554775, 0.4122792591252675, 0.4122806196003006, 0.41228098995582513,
 0.41228108334474756, 0.4122811051578895, 0.4122811098772742, 0.4122811108230642,
 0.4122811109986316, 0.41228111102881937, 0.41228111103362725, 0.4122811110343365,
 0.41228111103443343, 0.4122811110344457, 0.4122811110344471, 0.41228111103444737,
 0.41228111103444737, 0.41228111103444737, 0.41228111103444737, 0.41228111103444737,
 0.41228111103444737, 0.41228111103444737, 0.41228111103444737, 0.41228111103444737,
 0.41228111103444737, 0.41228111103444737, 0.41228111103444737, 0.41228111103444737,
 0.41228111103444737, 0.41228111103444737, 0.41228111103444737, 0.41228111103444737,
 0.41228111103444737, 0.41228111103444737, 0.41228111103444737, 0.41228111103444737,
 0.41228111103444737, 0.41228111103444737, 0.41228111103444737, 0.41228111103444737,
 0.4122811110344471, 0.4122811110344457, 0.41228111103443343, 0.4122811110343365,
 0.41228111103362725, 0.41228111102881937, 0.4122811109986316, 0.4122811108230642,
 0.4122811098772742, 0.4122811051578895, 0.41228108334474756, 0.41228098995582513,
120
Amazon Braket Developer Guide
Hello Pulse
 0.4122806196003006, 0.4122792591252675, 0.4122746298554775, 0.41226003881132406,
 0.4122174383870584, 0.4121022266390633, 0.411813599998087, 0.41114381673553674,
 0.4097040514225176, 0.4068371690898149, 0.40154918826437913, 0.3925140937986155,
 0.37821398931544986, 0.3572482512275351, 0.32877440347615655, 0.2929525775131368,
 0.2512065440720641, 0.20614055551722307, 0.16107456696238268, 0.11932853352131002,
 0.08350670755829034, 0.05503285980691184, 0.03406712171899729, 0.01976701723583167,
 0.010731922770068058, 0.005443941944632366, 0.002577059611929697, 0.0011372942989106229,
 0.00046751103636033026, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0])
a_b_cz_frame = device.frames[f'q{a}_q{b}_cz_frame']
dt = a_b_cz_frame.port.dt
a_b_cz_wfm_duration = len(a_b_cz_wfm.amplitudes)*dt
print('CZ pulse duration:', a_b_cz_wfm_duration*1e9, 'ns')
This should return:
CZ pulse duration: 124 ns
Now we can construct the cz gate using the waveform we just defined. Recall that the cz gate consists
of a phase flip of the target qubit if the control qubit is in the |1> state.
phase_shift_a=1.1733407221086924
phase_shift_b=6.269846678712192
a_rf_frame = device.frames[f'q{a}_rf_frame']
b_rf_frame = device.frames[f'q{b}_rf_frame']
frames = [a_rf_frame, b_rf_frame, a_b_cz_frame]
cz_pulse_sequence = (
 PulseSequence()
 .barrier(frames)
 .play(a_b_cz_frame, a_b_cz_wfm)
 .delay(a_rf_frame, a_b_cz_wfm_duration)
 .shift_phase(a_rf_frame, phase_shift_a)
 .delay(b_rf_frame, a_b_cz_wfm_duration)
 .shift_phase(b_rf_frame, phase_shift_b)
 .barrier(frames)
)
The a_b_cz_wfm waveform is played on a frame that is associated to a fast-flux port. Its role is to shift
the qubit frequency to activate a qubit-qubit interaction. For more information, see Roles of frames
and ports (p. 117). As the frequency varies, the qubit frames rotate at different rates than the singlequbit rf frames that are kept untouched: the latter ones are getting dephased. These phase shifts were
calibrated through Ramsey sequences beforehand and are provided here as hardcoded information
through phase_shift_a and phase_shift_b (Full period). We correct this dephasing by using
shift_phase instructions on rf frames. Note that this sequence will only work in programs where no
XY frame related to qubit a and b is used as we do not compensate for the phase shift that occurs on
these frames. This is the case for this single Bell pair program, which uses only rf and cz frames. For
more information, see Caldwell et al..
Now we’re ready to create a Bell pair with pulses.
bell_circuit_pulse = (
 Circuit()
 .rigetti_native_h(a)
 .rigetti_native_h(b)
 .pulse_gate([a, b], cz_pulse_sequence)
 .rigetti_native_h(b)
)
print(bell_circuit_pulse)
121
Amazon Braket Developer Guide
Accessing native gates using pulses
T : | 0 | 1 | 2 | 3 |4 | 5 | 6 | 7 | 8 |
q5 : -Rz(3.14)-Rx(1.57)-Rz(1.57)-Rx(-1.57)-PG--------------------------------------
 |
q6 : -Rz(3.14)-Rx(1.57)-Rz(1.57)-Rx(-1.57)-PG-Rz(3.14)-Rx(1.57)-Rz(1.57)-Rx(-1.57)-
T : | 0 | 1 | 2 | 3 |4 | 5 | 6 | 7 | 8 |
Let’s run this Bell pair on the Rigetti device. Note that running this code block will incur a charge. For
more information about these costs, see the Amazon Braket Pricing page. We recommend that you test
your circuits using a small amount of shots to ensure that it can run on the device before increasing the
shot count.
task = device.run(bell_pair_pulses, shots=100)
counts = task.result().measurement_counts
plt.bar(sorted(counts), [counts[k] for k in sorted(counts)])
Accessing native gates using pulses
Researchers often need to know exactly how the native gates supported by a particular QPU are
implemented as pulses. Pulse sequences are carefully calibrated by hardware providers, but accessing
them provides researchers the opportunity to design better gates or explore protocols for error
mitigation such as zero noise extrapolation by stretching the pulses of specific gates.
Amazon Braket supports programmatic access to native gates from Rigetti.
import math
122
Amazon Braket Developer Guide
Hello Pulse using OpenPulse
from braket.aws import AwsDevice
from braket.circuits import Circuit, GateCalibrations, QubitSet
from braket.circuits.gates import Rx
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
calibrations = device.gate_calibrations
print(f"Downloaded {len(calibrations)} calibrations.")
Note
Hardware providers periodically calibrate the QPU, often more than once a day. The Braket SDK
enables you to obtain the latest gate calibrations.
device.refresh_gate_calibrations()
To retrieve a given native gate, such as the RX or XY gate, you need to pass the Gate object and the
qubits of interest. For example, you can inspect the pulse implementation of the RX(π/2) applied on
qubit 0.
rx_pi_2_q0 = (Rx(math.pi/2), QubitSet(0))
pulse_sequence_rx_pi_2_q0 = calibrations.pulse_sequences[rx_pi_2_q0]
You can create a filtered set of calibrations using the filter function. You pass a list of gates or a list
of QubitSet. The following code creates two sets that contain all of the calibrations for RX(π/2) and for
qubit 0.
rx_calibrations = calibrations.filter(gates=[Rx(math.pi/2)])
q0_calibrations = calibrations.filter(qubits=QubitSet([0])
Now you can provide or modify the action of native gates by attaching a custom calibration set. For
example, consider the following circuit.
bell_circuit = (
Circuit()
.rx(0,math.pi/2)
.rx(1,math.pi/2)
.cz(0,1)
.rx(1,-math.pi/2)
)
You can run it with a custom gate calibration for the rx gate on qubit 0 by passing a dictionary of
PulseSequence objects to the gate_definitions keyword argument. You can construct a dictionary
from the attribute pulse_sequences of the GateCalibrations object. All gates not specified are
replaced with the quantum hardware provider's pulse calibration.
nb_shots = 50
custom_calibration = GateCalibrations({rx_pi_2_q0: pulse_sequence_rx_pi_2_q0})
task=device.run(bell_circuit, gate_definitions=custom_calibration.pulse_sequences,
 shots=nb_shots)
Hello Pulse using OpenPulse
OpenPulse is a language for specifying pulse-level control of a general quantum device and is part of the
OpenQASM 3.0 specification. Amazon Braket supports OpenPulse for directly programming pulses using
the OpenQASM 3.0 representation.
123
Amazon Braket Developer Guide
Hello Pulse using OpenPulse
Braket uses OpenPulse as the underlying intermediate representation for expressing pulses in native
instructions. OpenPulse supports the addition of instruction calibrations in the form of defcal (short
for “define calibration”) declarations. With these declarations, you can specify an implementation of a
gate instruction within a lower-level control grammar.
In this example, we’ll construct a Bell circuit using OpenQASM 3.0 and OpenPulse on a device using
frequency-tunable transmons. Recall that a Bell circuit is a two-qubit circuit that consists of a Hadamard
gate on the first qubit followed by a cnot gate between the two qubits. As cnot gates differ from
cz gates only through a basis transform, here we will define a Bell pair using Hadamard and cz gates
instead as the device provides a simpler way to create cz gates for this demonstration.
Let’s begin with defining the Hadamard gate using native gates of the device.
client = boto3.client('braket', region_name='us-west-1')
defcal h $10 {
 rz(pi) $10;
 rx(pi/2) $10;
 rz(pi/2) $10;
 rx(-pi/2) $10;
}
defcal h $113 {
 rz(pi) $113;
 rx(pi/2) $113;
 rz(pi/2) $113;
 rx(-pi/2) $113;
}
For the CZ gate, we will use an arbitrary waveform with parameters (amplitude, rise/fall time,
and duration) that have been predetermined beforehand. This waveform will be applied on the
q10_q113_cz_frame.
cal {
 waveform q10_q113_cz_wfm = {0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
 0.00021019328936380065, 0.0008644760431374357, 0.003028104466884364, 0.009058671036471382,
 0.02322670104785881, 0.05128438687551476, 0.09812230691191462, 0.16403303942241076,
 0.24221990600377236, 0.32040677258513395, 0.38631750509563006, 0.43315542513203,
 0.4612131109596859, 0.4753811409710734, 0.4814117075406603, 0.48357533596440727,
 0.48422961871818093, 0.4843963766398558, 0.4844321964728096, 0.4844386806183817,
 0.4844396697373718, 0.48443979687791755, 0.48443981064783953, 0.48443981190433844,
 0.4844398120009317, 0.48443981200718716, 0.4844398120075284, 0.48443981200754405,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
124
Amazon Braket Developer Guide
Hello Pulse using OpenPulse
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.48443981200754405, 0.4844398120075284, 0.48443981200718716,
 0.4844398120009317, 0.48443981190433844, 0.48443981064783953, 0.48443979687791755,
 0.4844396697373718, 0.4844386806183817, 0.4844321964728096, 0.4843963766398558,
 0.48422961871818093, 0.48357533596440727, 0.4814117075406603, 0.4753811409710734,
 0.46121311095968553, 0.4331554251320285, 0.38631750509562957, 0.32040677258513167,
 0.24221990600377236, 0.16403303942240913, 0.0981223069119151, 0.0512843868755143,
 0.023226701047858084, 0.009058671036471328, 0.0030281044668842563, 0.0008644760431374626,
 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0};
}
defcal cz $10, $113 {
 barrier q10_rf_frame, q113_rf_frame, q10_q113_cz_frame;
 play(q10_q113_cz_frame, q10_q113_cz_wfm);
 delay[124ns] q10_rf_frame;
 shift_phase(q10_rf_frame, 1.1733407221086924);
 delay[124ns] q113_rf_frame;
 shift_phase(q113_rf_frame, 6.269846678712192);
 barrier q10_rf_frame, q113_rf_frame, q10_q113_cz_frame;
}
The duration of the q10_q113_cz_wfm waveform is 124 samples, which corresponds to 124 ns as the
minimum time increment dt is 1 ns.
The q10_q113_cz_wfm waveform is played on a frame that is bound to a fast-flux port. Its role is
to shift the qubit frequency to activate a qubit-qubit interaction. For more information, see Roles of
frames and ports (p. 117). As the frequency varies, the qubit frames rotate at different rates compared
to the single-qubit rf frames that are kept untouched: the latter ones are getting dephased. This
dephasing can be measured with Ramsey sequences during a calibration stage and compensated with
shift_phase instructions on rf and xy frames. For more information, see Caldwell et al..
We can now execute the Bell pair circuit where we decomposed the cnot gate using a couple of
Hadamard and cz gates.
125
Amazon Braket Developer Guide
Hello Pulse using OpenPulse
bit[2] c;
h $10;
h $113;
cz $10, $113;
h $113;
c[0] = measure $10;
c[1] = measure $113;
The full OpenQASM 3.0 representation for the Bell circuit constructed using a combination of native
gates and pulses is as follows.
// bell_pair_with_pulse.qasm
OPENQASM 3.0;
cal {
 waveform q10_q113_cz_wfm = {0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
 0.00021019328936380065, 0.0008644760431374357, 0.003028104466884364, 0.009058671036471382,
 0.02322670104785881, 0.05128438687551476, 0.09812230691191462, 0.16403303942241076,
 0.24221990600377236, 0.32040677258513395, 0.38631750509563006, 0.43315542513203,
 0.4612131109596859, 0.4753811409710734, 0.4814117075406603, 0.48357533596440727,
 0.48422961871818093, 0.4843963766398558, 0.4844321964728096, 0.4844386806183817,
 0.4844396697373718, 0.48443979687791755, 0.48443981064783953, 0.48443981190433844,
 0.4844398120009317, 0.48443981200718716, 0.4844398120075284, 0.48443981200754405,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
126
Amazon Braket Developer Guide
Hello Pulse using OpenPulse
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.4844398120075447, 0.4844398120075447, 0.4844398120075447,
 0.4844398120075447, 0.48443981200754405, 0.4844398120075284, 0.48443981200718716,
 0.4844398120009317, 0.48443981190433844, 0.48443981064783953, 0.48443979687791755,
 0.4844396697373718, 0.4844386806183817, 0.4844321964728096, 0.4843963766398558,
 0.48422961871818093, 0.48357533596440727, 0.4814117075406603, 0.4753811409710734,
 0.46121311095968553, 0.4331554251320285, 0.38631750509562957, 0.32040677258513167,
 0.24221990600377236, 0.16403303942240913, 0.0981223069119151, 0.0512843868755143,
 0.023226701047858084, 0.009058671036471328, 0.0030281044668842563, 0.0008644760431374626,
 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0};
}
defcal h $10 {
 rz(pi) $10;
 rx(pi/2) $10;
 rz(pi/2) $10;
 rx(-pi/2) $10;
}
defcal h $113 {
 rz(pi) $113;
 rx(pi/2) $113;
 rz(pi/2) $113;
 rx(-pi/2) $113;
}
defcal cz $10, $113 {
 barrier q10_rf_frame, q113_rf_frame, q10_q113_cz_frame;
 play(q10_q113_cz_frame, q10_q113_cz_wfm);
 delay[124ns] q10_rf_frame;
 shift_phase(q10_rf_frame, 1.1733407221086924);
 delay[124ns] q113_rf_frame;
 shift_phase(q113_rf_frame, 6.269846678712192);
 barrier q10_rf_frame, q113_rf_frame, q10_q113_cz_frame;
}
bit[2] c;
h $10;
h $113;
cz $10, $113;
h $113;
c[0] = measure $10;
c[1] = measure $113;
You can now use the Braket SDK to execute this OpenQASM 3.0 program on the Rigetti device using the
following code.
# import the device module
from braket.aws import AwsDevice
from braket.ir.openqasm import Program
client = boto3.client('braket', region_name='us-west-1')
with open("pulse.qasm", "r") as pulse:
 pulse_qasm_string = pulse.read()
127
Amazon Braket Developer Guide
Hello Pulse using OpenPulse
# choose the Rigetti device
device = AwsDevice("arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3")
program = Program(source=pulse_qasm_string)
my_task = device.run(program)
# You can also specify an optional s3 bucket location and number of shots,
 # if you so choose, when running the program
s3_location = ("amazon-braket-my-bucket", "openqasm-tasks")
my_task = device.run(
 program,
 s3_location,
 shots=100,
)
128
Amazon Braket Developer Guide
What is a Hybrid Job
Amazon Braket Hybrid Jobs User
Guide
This section provides instructions about how to set up and manage hybrid jobs in Amazon Braket.
You can access hybrid jobs in Braket using:
• The Amazon Braket Python SDK.
• The Amazon Braket console.
• The Amazon Braket API.
In this section:
• What is a Hybrid Job (p. 129)
• When to use Amazon Braket Hybrid Jobs (p. 130)
• Run your local code as a hybrid job (p. 130)
• Run a hybrid job with Amazon Braket Hybrid Jobs (p. 135)
• Create your first Hybrid Job (p. 136)
• Inputs, outputs, environmental variables, and helper functions (p. 142)
• Save job results (p. 144)
• Save and restart hybrid jobs using checkpoints (p. 145)
• Define the environment for your algorithm script (p. 146)
• Use hyperparameters (p. 148)
• Configure the hybrid job instance to run your algorithm script (p. 149)
• Cancel a Hybrid Job (p. 151)
• Using parametric compilation to speed up Hybrid Jobs (p. 152)
• Use Amazon Braket Hybrid Jobs and PennyLane to run a QAOA algorithm (p. 153)
• Accelerate your hybrid workloads with embedded simulators from PennyLane (p. 155)
• Build and debug a hybrid job with local mode (p. 160)
• Bring your own container (BYOC) (p. 161)
• Configure the default bucket in AwsSession (p. 166)
• Interact with hybrid jobs directly using the API (p. 166)
What is a Hybrid Job
Amazon Braket Hybrid Jobs offers a way for you to run hybrid quantum-classical algorithms requiring
both classical AWS resources and quantum processing units (QPUs). Hybrid Jobs is designed to spin up
the requested classical resources, run your algorithm, and release the instances after completion so you
only pay for what you use.
Hybrid Jobs is ideal for long-running iterative algorithms involving both classical and quantum resources.
You submit your algorithm to run, Braket runs it in a scalable containerized environment, and you
retrieve the results when the algorithm is complete.
Additionally, quantum tasks created from a hybrid job benefit from higher priority queueing to a target
QPU. This ensures your quantum tasks are processed and executed ahead of others in the queue. This is
129
Amazon Braket Developer Guide
When to use Amazon Braket Hybrid Jobs
particularly beneficial for iterative hybrid algorithms where subsequent task depend on the outcomes
of prior quantum tasks. Examples of such algorithms include the Quantum Approximate Optimization
Algorithm (QAOA), variational quantum eigensolver, or quantum machine learning. You can also
monitor your algorithm progress in near-real time, enabling you to keep track of costs, budget, or
custom metrics such as training loss or expectation values.
When to use Amazon Braket Hybrid Jobs
Amazon Braket Hybrid Jobs enables you to run hybrid quantum-classical algorithms, such as the
Variational Quantum Eigensolver (VQE) and the Quantum Approximate Optimization Algorithm (QAOA),
that combine classical compute resources with quantum computing devices to optimize the performance
of today’s quantum systems. Amazon Braket Hybrid Jobs provides three main benefits:
1. Performance: Amazon Braket Hybrid Jobs provides better performance than running hybrid
algorithms from your own environment. While your job is running, it has priority access to the selected
target QPU. Tasks from your job run ahead of other tasks queued on the device. This results in shorter
and more predictable runtimes for hybrid algorithms. Amazon Braket Hybrid Jobs also supports
parametric compilation. You can submit a circuit using free parameters and Braket compiles the circuit
once, without the need to recompile for subsequent parameter updates to the same circuit, resulting
in even faster runtimes.
2. Convenience: Amazon Braket Hybrid Jobs simplifies setting up and managing your compute
environment and keeping it running while your hybrid algorithm runs. You just provide your algorithm
script and select a quantum device (either a quantum processing unit or a simulator) on which to
run. Amazon Braket waits for the target device to become available, spins up the classical resources,
runs the workload in pre-built container environments, returns the results to Amazon Simple Storage
Service (Amazon S3), and releases the compute resources.
3. Metrics: Amazon Braket Hybrid Jobs provides on-the-fly insights into running algorithms and delivers
customizable algorithm metrics in near real-time to Amazon CloudWatch and the Amazon Braket
console so you can track the progress of your algorithms.
Run your local code as a hybrid job
Amazon Braket Hybrid Jobs provides a fully managed orchestration of hybrid quantum-classical
algorithms, combining Amazon EC2 compute resources with Amazon Braket Quantum Processing Unit
(QPU) access. Quantum tasks created in a hybrid job have priority queueing over individual quantum
tasks so that your algorithms will not be interrupted by fluctuations in the quantum task queue. Each
QPU maintains a separate hybrid jobs queue, ensuring that only one hybrid job can run at any given
time.
In the following example we will:
• Create a hybrid job from local Python code (p. 130)
• Install additional Python packages and source code (p. 132)
• Save and load data into a hybrid job instance (p. 133)
• Best practices for hybrid job decorators (p. 21)
Create a hybrid job from local Python code
You can run your local Python code as an Amazon Braket Hybrid Job. You can do this by annotating
your code with an @hybrid_job decorator, as shown in the following code example. For custom
environments, you can opt to use a custom container (p. 161) from Amazon Elastic Container Registry
(ECR).
130
Amazon Braket Developer Guide
Create a hybrid job from local Python code
Note
Only Python 3.10 is supported by default.
You can use the @hybrid_job decorator to annotate a function. Braket will transform the code inside
the decorator into a Braket hybrid job algorithm script (p. 136). The hybrid job will then invoke the
function inside the decorator on an Amazon EC2 instance. You can monitor the progress of the job with
job.state() or with the Braket console. The following code example shows how to run a sequence of
five Bell states on Rigetti-Aspen M-3.
from braket.aws import AwsDevice
from braket.circuits import Circuit, FreeParameter, Observable
from braket.devices import Devices
from braket.jobs.hybrid_job import hybrid_job
from braket.jobs.metrics import log_metric
device_arn = Devices.Amazon.SV1
@hybrid_job(device=device_arn) # choose priority device
def run_hybrid_job(num_tasks=1):
 device = AwsDevice(device_arn) # declare AwsDevice within the hybrid job
 # create a parametric circuit
 circ = Circuit()
 circ.rx(0, FreeParameter("theta"))
 circ.cnot(0, 1)
 circ.expectation(observable=Observable.X(), target=0)
 theta = 0.0 # initial parameter
 for i in range(num_tasks):
 task = device.run(circ, shots=100, inputs={"theta": theta}) # input parameters
 exp_val = task.result().values[0]
 theta += exp_val # modify the parameter (possibly gradient descent)
 log_metric(metric_name="exp_val", value=exp_val, iteration_number=i)
 return {"final_theta": theta, "final_exp_val": exp_val}
You create the hybrid job by invoking the function as you would normal Python functions. However, the
decorator function returns the hybrid job handle rather than the result of the function. To retrieve the
results after it has completed, use job.result().
job = run_hybrid_job(num_tasks=1)
result = job.result()
The device argument in the @hybrid_job decorator specifies the device that the hybrid job will have
priority access to - in this case, Rigetti Aspen-M-3. To get QPU priority, you must ensure that the device
ARN used within the function matches that specified in the decorator. For convenience, you can use the
helper function get_job_device_arn() to capture the device ARN declared in @hybrid_job.
Note
Each hybrid job has at least a one minute startup time since it creates a containerized
environment on Amazon EC2. So for very short workloads, such as a single circuit or a batch of
circuits, it may suffice for you to use quantum tasks.
Hyperparameters
The run_hybrid_job() function takes the argument num_tasks to control the number of quantum
tasks created. The hybrid job automatically captures this as a hyperparameter (p. 148).
131
Amazon Braket Developer Guide
Install additional Python packages and source code
Note
Hyperparameters are displayed in the Braket console as strings, which are limited to 2500
characters.
Metrics and logging
Within the run_hybrid_job() function, metrics from iterative algorithms are recorded with
log_metrics. Metrics are automatically plotted in the Braket console page under the hybrid job tab.
You can use metrics to track the quantum task costs in near-real time during the hybrid job run with the
Braket cost tracker (p. 20). The example above uses the metric name “probability” which records the first
probability from the result type (p. 63).
Retrieving results
After the hybrid job has completed, you use job.result() to retrieve the hybrid jobs results. Any
objects in the return statement are automatically captured by Braket. Note that the objects returned
by the function must be a tuple with each element being serializable. For example, the following code
shows a working, and a failing example.
@hybrid_job(device=Devices.Amazon.SV1, local=True)
def passing():
 np_array = np.random.rand(5)
 return 1, "string", np_array.tolist() # tuple of serializable values

@hybrid_job(device=Devices.Amazon.SV1, local=True)
def failing():
 np_array = np.random.rand(5)
 return np_array # not serializable
Job name
By default, the name for this hybrid job will be inferred from the function name followed by the
timestamp. You may also specify a unique custom name up to 50 characters long. For example, below we
set the job name to be "my-job-name":
@hybrid_job(device=Devices.Amazon.SV1, job_name="my-job-name")
def function():
 pass
Local mode
Local jobs (p. 160) are be created by adding the argument local=True to the decorator. This runs the
hybrid job in a containerized environment on your local compute environment, such as your laptop. Local
jobs do not have priority queueing for quantum tasks. For advanced cases such as multi-node or MPI,
local jobs may have access to the required Braket environment variables. The code below creates a local
hybrid job with the device as the SV1 simulator.
@hybrid_job(device=Devices.Amazon.SV1, local=True)
def run_hybrid_job(num_tasks = 1):
 return ...
All other hybrid job options are supported. For a list of options see the braket.jobs.quantum_job_creation
module.
Install additional Python packages and source code
You can customize your runtime environment to use your preferred Python packages. You can use either
a requirements.txt file, or bring your own container (BYOC) (p. 161). To customize a runtime
environment using a requirements.txt file, refer to the following code example:
132
Amazon Braket Developer Guide
Save and load data into a hybrid job instance
@hybrid_job(device=Devices.Rigetti.M3, dependencies="requirements.txt")
def run_hybrid_job(num_tasks = 1):
 return ...
For example, the requirements.txt file may include other packages to install:
qiskit
pennylane >= 0.31
mitiq == 0.29
Additional source code can be used within the hybrid job with the following code example.
@hybrid_job(device=Devices.Rigetti.M3, include_modules="my_module")
def run_hybrid_job(num_tasks = 1):
 return ...
Save and load data into a hybrid job instance
Specifying input training data
When you create a hybrid job, you may provide an input training datasets by specifying an Amazon
Simple Storage Service (Amazon S3) bucket. You may also specify a local path, in which case Braket will
automatically upload the data to Amazon S3 at s3://<default_bucket_name>/jobs/<job_name>/
data/<channel_name> . If you specify a local path, the channel name defaults to “input”. The
following code shows a numpy file from the local path data/file.npy:
@hybrid_job(device=Devices.Rigetti.M3, input_data="data/file.npy")
def run_hybrid_job(num_tasks = 1):
 data = np.load("data/file.npy")
 return ...
For S3, you must use the get_input_data_dir() helper funciton
s3_path = "s3://amazon-braket-us-west-1-961591465522/job-data/file.npy"
@hybrid_job(device=None, input_data=s3_path)
def job_s3_input():
 np.load(get_input_data_dir() + "/file.npy")

@hybrid_job(device=None, input_data={"channel": s3_path})
def job_s3_input_channel():
 np.load(get_input_data_dir("channel") + "/file.npy")
You may specify multiple input data sources by providing a dictionary of channel values and S3 URIs or
local paths.
input_data = {
 "input": "data/file.npy",
 "input_2": "s3://my-bucket/data.json"
}
@hybrid_job(device=None, input_data=input_data)
def multiple_input_job():
 np.load(get_input_data_dir("input") + "/file.npy")
 np.load(get_input_data_dir("input_2") + "/data.json")
133
Amazon Braket Developer Guide
Best practices for hybrid job decorators
Note
When the input data is large (>1GB), there will be a long wait time before the job is created. This
is due to the fact that the local input data will first be uploaded to an S3 bucket, then the S3
path will be added to the job request.Finally, the job request is submitted to the Braket service.
Saving results to S3
To save results not included in the return statement of the decorated function, you must append
the correct directory to all file writing operations. The example below, shows saving a numpy array
and a matplotlib figure by using the get_results_dir() function to access the output directory
opt/braket/model to write job results to. This is also available as the environment variable
os.environ["AMZN_BRAKET_JOB_RESULTS_DIR"] .
@hybrid_job(device=Devices.Rigetti.M3)
def run_hybrid_job(num_tasks = 1):
 result = np.random.rand(5)

 # save a numpy array
 np.save(get_results_dir() + "/result.npy", result)

 # save a matplotlib figure
 plt.plot(result)
 plt.savefig(get_results_dir() + "fig.png")
 return ...
All results are compressed into a file named model.tar.gz. You can download the results with the
Python function job.result() , or by navigating to the results folder from the hybrid job page in the
Braket management console.
Best practices for hybrid job decorators
Embrace asynchronicity
Hybrid jobs created with the decorator annotation are asynchronous - they will run once the classical and
quantum resources are available. You monitor the progress of the algorithm via the Braket Management
Console or Amazon CloudWatch. When you submit your algorithm to run, Braket runs your algorithm in a
scalable containerized environment and results are retrieved when the algorithm is complete.
Run iterative variational algorithms
Hybrid jobs gives you the tools to run iterative quantum-classical algorithms. For purely quantum
problems, use quantum tasks (p. 84) or a batch of quantum tasks (p. 90). The priority access to certain
QPUs is most beneficial for long-running variational algorithms requiring multiple iterative calls to the
QPUs with classical processing in between.
Debug using local mode
Before you run a hybrid job on a QPU, its recommended to first run on the simulator SV1 to confirm it
runs as expected. For small scale tests, you can run with local mode for rapid iteration and debugging.
Improve reproducibility with Bring your own container (BYOC) (p. 161)
Create a reproducible experiment by encapsulating your software and its dependencies within a
containerized environment. By packaging all your code, dependencies, and settings in a container, you
prevent potential conflicts and versioning issues.
Multi-instance distributed simulators
If you want to run a large number of circuits, consider using built-in MPI support to run local
simulators on multiple instances within a single hybrid job. For more information, see embedded
simulators (p. 155).
134
Amazon Braket Developer Guide
Run a hybrid job with Amazon Braket Hybrid Jobs
Use parametric circuits
Parametric circuits that you submit from a hybrid job are automatically compiled on certain QPUs using
parametric compilation (p. 152) to improve the runtimes of your algorithms.
Checkpoint periodically
For long-running hybrid jobs, its recommended to periodically save the intermediate state of
the algorithm. You can use the built-in save_job_checkpoint() helper function, or save files
to the AMZN_BRAKET_JOB_RESULTS_DIR path. The later is available with the helper function
get_job_results_dir() . See Save and restart jobs using checkpoints (p. 145) for a complete
example.
For further examples, use cases, and best-practices, see Amazon Braket examples GitHub.
Run a hybrid job with Amazon Braket Hybrid Jobs
To run a hybrid job with Amazon Braket Hybrid Jobs, you first need to define your algorithm. You can
define it by writing the algorithm script and, optionally, other dependency files using the Amazon Braket
Python SDK or PennyLane. If you want to use other (open source or proprietary) libraries, you can define
your own custom container image using Docker, which includes these libraries. For more information, see
Bring your own container (BYOC) (p. 161).
In either case, next you create a hybrid job using the Amazon Braket API, where you provide your
algorithm script or container, select the target quantum device the hybrid job is to use, and then choose
from a variety of optional settings. The default values provided for these optional settings work for the
majority of use cases. For the target device to run your Hybrid Job, you have a choice between a QPU,
an on-demand simulator (such as SV1, DM1 or TN1), or the classical hybrid job instance itself. With an
on-demand simulator or QPU, your hybrid jobs container makes API calls to a remote device. With the
embedded simulators, the simulator is embedded in the same container as your algorithm script. The
lightning simulators from PennyLane are embedded with the default pre-built hybrid jobs container for
you to use. If you run your code using an embedded PennyLane simulator or a custom simulator, you
can specify an instance type as well as how many instances you wish to use. Refer to the Amazon Braket
Pricing page for the costs associated with each choice.
If your target device is an on-demand or embedded simulator, Amazon Braket starts running the hybrid
job right away. It spins up the hybrid job instance (you can customize the instance type in the API call),
runs your algorithm, writes the results to Amazon S3, and releases your resources. This release of
resources ensures that you only pay for what you use.
135
Amazon Braket Developer Guide
Create your first Hybrid Job
The total number of concurrent hybrid jobs per quantum processing unit (QPU) is restricted. Today, only
one hybrid job can run on a QPU at any given time. Queues are used to control the number of hybrid
jobs allowed to run so as not to exceed the limit allowed. If your target device is a QPU, your hybrid job
first enters the job queue of the selected QPU. Amazon Braket spins up the hybrid job instance needed
and runs your hybrid job on the device. For the duration of your algorithm, your hybrid job has priority
access, meaning that quantum tasks from your hybrid job run ahead of other Braket quantum tasks
queued up on the device, provided the job quantum tasks are submitted to the QPU once every few
minutes. Once your hybrid job is complete, resources are released, meaning you only pay for what you
use.
Note
Devices are regional and your hybrid job runs in the same AWS Region as your primary device.
In both the simulator and QPU target scenarios, you have the option to define custom algorithm metrics,
such as the energy of your Hamiltonian, as part of your algorithm. These metrics are automatically
reported to Amazon CloudWatch and from there, they display in near real-time in the Amazon Braket
console.
Note
If you wish to use a GPU based instance, be sure to use one of the GPU-based simulators
available with the embedded simulators on Braket (for example, lightning.gpu). If you
choose one of the CPU-based embedded simulators (for example, lightning.qubit, or
braket:default-simulator), the GPU will not be used and you may incur unnecessary costs.
Create your first Hybrid Job
This section shows you how to create a Hybrid Job using a Python script. Alternatively, to create a hybrid
job from local Python code, such as your preferred integrated development environment (IDE) or a
Braket notebook, see Run your local code as a hybrid job (p. 130).
Before you run your first hybrid job, you must ensure that you have sufficient permissions to proceed
with this task. To determine that you have the correct permissions, select Permissions from the menu
on left side of the Braket Console. The Permissions management for Amazon Braket page helps you
verifiy whether one of your existing roles has permissions that are sufficient to run your hybrid job or
guides you through the creation of a default role that can be used to run your hybrid job if you do not
already have such a role.
136
Amazon Braket Developer Guide
Create your first Hybrid Job
To verify that you have roles with suficient permissions to execute a hybrid job, select the Verify existing
role button. If you do, you get a message that the roles were found. To see the names of the roles and
their role ARNs, select the Show roles button.
If you do not have a role with sufficient permissions to execute a hybrid job, you get a message that no
such role was found. Select the Create default role button to obtain a role with sufficient permissions.
If the role was created successfully, you get a message confirming this.
137
Amazon Braket Developer Guide
Create your first Hybrid Job
If you do not have permissions to make this inquiry, you will be denied access. In this case, contact your
internal AWS administrator.
Once you have a role with permissions to run a hybrid job, you are ready to proceed. The key piece of
your first Braket hybrid job is the algorithm script. It defines the algorithm you want to run and contains
the classical logic and quantum tasks that are part of your algorithm. In addition to your algorithm
script, you can provide other dependency files. The algorithm script together with its dependencies is
called the source module. The entry point defines the first file or function to run in your source module
when the hybrid job starts.
138
Amazon Braket Developer Guide
Create your first Hybrid Job
First, consider the following basic example of an algorithm script that creates five bell states and prints
the corresponding measurement results.
import os
from braket.aws import AwsDevice
from braket.circuits import Circuit
def start_here():
 print("Test job started!!!!!")
 # Use the device declared in the job script
 device = AwsDevice(os.environ["AMZN_BRAKET_DEVICE_ARN"])
 bell = Circuit().h(0).cnot(0, 1)
 for count in range(5):
 task = device.run(bell, shots=100)
 print(task.result().measurement_counts)
 print("Test job completed!!!!!")
Save this file with the name algorithm_script.py in your current working directory on your Braket
notebook or local environment. The algorithm_script.py file has start_here() as the planned entry
point.
Next, create a Python file or Python notebook in the same directory as the algorithm_script.py file. This
script kicks off the hybrid job and handles any asynchronous processing, such as printing the status or
key outcomes that we are interested in. At a minimum, this script needs to specify your hybrid job script
and your primary device.
Note
For more information about how to create a Braket notebook or upload a file, such as the
algorithm_script.py file, in the same directory as the notebooks, see Run your first circuit using
the Amazon Braket Python SDK (p. 39)
For this basic first case, you target a simulator. Whichever type of quantum device you target, a simulator
or an actual quantum processing unit (QPU), the device you specify with device in the following script
is used to schedule the hybrid job and is available to the algorithm scripts as the environment variable
AMZN_BRAKET_DEVICE_ARN.
139
Amazon Braket Developer Guide
Create your first Hybrid Job
Note
You can only use devices that are available in the AWS Region of your hybrid job. The Amazon
Braket SDK autoselects this AWS Region. For example, a hybrid job in us-east-1 can use IonQ,
SV1, DM1, and TN1 devices, but not Rigetti devices.
If you choose a quantum computer instead of a simulator, Braket schedules your hybrid jobs to run all of
their quantum tasks with priority access.
from braket.aws import AwsQuantumJob
job = AwsQuantumJob.create(
 "arn:aws:braket:::device/quantum-simulator/amazon/sv1",
 source_module="algorithm_script.py",
 entry_point="algorithm_script:start_here",
 wait_until_complete=True
)
The parameter wait_until_complete=True sets a verbose mode so that your job prints output from
the actual job as it’s running. You should see an output similar to the following example.
job = AwsQuantumJob.create(
 "arn:aws:braket:::device/quantum-simulator/amazon/sv1",
 source_module="algorithm_script.py",
 entry_point="algorithm_script:start_here",
 wait_until_complete=True,
)
Initializing Braket Job: arn:aws:braket:us-west-2:<accountid>:job/braket-jobdefault-1631915042705
.........................................
.
.
.
Completed 36.1 KiB/36.1 KiB (692.1 KiB/s) with 1 file(s) remaining#015download:
 s3://braket-external-assets-preview-us-west-2/HybridJobsAccess/models/
braket-2019-09-01.normal.json to ../../braket/additional_lib/original/
braket-2019-09-01.normal.json
Running Code As Process
Test job started!!!!!
Counter({'00': 55, '11': 45})
Counter({'11': 59, '00': 41})
Counter({'00': 55, '11': 45})
Counter({'00': 58, '11': 42})
Counter({'00': 55, '11': 45})
Test job completed!!!!!
Code Run Finished
2021-09-17 21:48:05,544 sagemaker-training-toolkit INFO Reporting training SUCCESS
Alternatively, you can access the log output from Amazon CloudWatch. To do this, go to the Log groups
tab on the left menu of the job detail page, select the log group aws/braket/jobs, and then choose
the log stream that contains the last part of your job-arn in the name. In the example above, this is
braket-job-default-1631915042705/algo-1-1631915190.
140
Amazon Braket Developer Guide
Create your first Hybrid Job
You can also view the status of the hybrid job in the console by selecting the Hybrid Jobs page and then
choose Settings.
Your hybrid job produces some artifacts in Amazon S3 while it runs. The default S3 bucket name is
amazon-braket-<region>-<accountid> and the content is in the jobs/<jobname> directory. You
can configure the S3 locations where these artifacts are stored by specifying a different code_location
when the hybrid job is created with the Braket Python SDK.
Note
This S3 bucket must be located in the same AWS Region as your job script.
The jobs/<jobname> directory contains a subfolder with the output from the entry point script in a
model.tar.gz file. There is also a directory called script that contains your algorithm script artifacts
in a source.tar.gz file. The results from your actual quantum tasks are in the directory named jobs/
<jobname>/tasks.
141
Amazon Braket Developer Guide
Inputs, outputs, environmental
variables, and helper functions
Inputs, outputs, environmental variables, and
helper functions
In addition to the file or files that makes up your complete algorithm script, your hybrid job can have
additional inputs and outputs. When your hybrid job starts, Amazon Braket copies inputs provided as
part of the hybrid job creation into the container that runs the algorithm script. When the hybrid job
completes, all outputs defined during the algorithm are copied to the Amazon S3 location specified.
Note
Algorithm metrics are reported in real time and do not follow this output procedure.
Amazon Braket also provides several environment variables and helper functions to simplify the
interactions with container inputs and outputs.
This section explains the key concepts of the AwsQuantumJob.create function provided by the
Amazon Braket Python SDK and their mapping to the container file structure.
In this section:
• Inputs (p. 142)
• Outputs (p. 143)
• Environmental variables (p. 143)
• Helper functions (p. 144)
Inputs
Input data: Input data can be provided to the hybrid algorithm by specifying the input data file, which
is set up as a dictionary, with the input_data argument. The user defines the input_data argument
within the AwsQuantumJob.create function in the SDK. This copies the input data to to the container
file system at the location given by the environment variable "AMZN_BRAKET_INPUT_DIR". For a couple
examples of how input data is used in a hybrid algorithm, see the QAOA with Amazon Braket Hybrid Jobs
and PennyLane and Quantum machine learning in Amazon Braket Hybrid Jobs Jupyter notebooks.
Note
When the input data is large (>1GB), there will be a long wait time before the hybrid job is
submitted. This is due to the fact that the local input data will first be uploaded to an S3 bucket,
then the S3 path will be added to the hybrid job request, and, finally, the hybrid job request is
submitted to Braket service.
Hyperparameters: If you pass in hyperparameters, they are available under the environment variable
"AMZN_BRAKET_HP_FILE".
Note
For more information about how to create hyperparameters and input data and then pass this
information to the hybrid job script, see the Use hyperparameters (p. 148) section and this
github page.
Checkpoints: To specify a job-arn whose checkpoint you want to use in a new hybrid job, use the
copy_checkpoints_from_job command. This command copies over the checkpoint data to the
checkpoint_configs3Uri of the new hybrid job, making it available at the path given by the
environment variable AMZN_BRAKET_CHECKPOINT_DIR while the job runs. The default is None,
meaning checkpoint data from another hybrid job will not be used in the new hybrid job.
142
Amazon Braket Developer Guide
Outputs
Outputs
Quantum Tasks: Quantum task results are stored in the S3 location specified in output_data_config.
If you don’t specify this value, it defaults to s3://amazon-braket-<region>-<accountID>/jobs/
<job-name>/tasks.
Job results: Everything that your algorithm script saves to the directory given by the environment
variable "AMZN_BRAKET_JOB_RESULTS_DIR" is copied to the S3 location specified in
output_data_config. If you don’t specify this value, it defaults to s3://amazon-braket-
<region>-<accountID>/jobs/<job-name>/data. We provide the SDK helper function
save_job_result , which you can use to store results conveniently in the form of a dictionary when
called from your algorithm script.
Checkpoints: If you want to use checkpoints, you can save them in the directory given by the
environment variable "AMZN_BRAKET_CHECKPOINT_DIR". You can also use the SDK helper function
save_job_checkpoint instead.
Algorithm metrics: You can define algorithm metrics as part of your algorithm script that are emitted
to Amazon CloudWatch and displayed in real time in the Amazon Braket console while your hybrid job is
running. For an example of how to use algorithm metrics, see Use Amazon Braket Hybrid Jobs to run a
QAOA algorithm_ (p. 153).
Environmental variables
Amazon Braket provides several environment variables to simplify the interactions with container inputs
and outputs. The folllowing code lists the environmental variables that Braket uses.
# the input data directory opt/braket/input/data
os.environ["AMZN_BRAKET_INPUT_DIR"]
# the output directory opt/braket/model to write job results to
os.environ["AMZN_BRAKET_JOB_RESULTS_DIR"]
# the name of the job
os.environ["AMZN_BRAKET_JOB_NAME"]
# the checkpoint directory
os.environ["AMZN_BRAKET_CHECKPOINT_DIR"]
# the file containing the hyperparameters
os.environ["AMZN_BRAKET_HP_FILE"]
# the device ARN (AWS Resource Name)
os.environ["AMZN_BRAKET_DEVICE_ARN"]
# the output S3 bucket, as specified in the CreateJob request’s OutputDataConfig
os.environ["AMZN_BRAKET_OUT_S3_BUCKET"]
# the entry point as specified in the CreateJob request’s ScriptModeConfig
os.environ["AMZN_BRAKET_SCRIPT_ENTRY_POINT"]
# the compression type as specified in the CreateJob request’s ScriptModeConfig
os.environ["AMZN_BRAKET_SCRIPT_COMPRESSION_TYPE"]
# the S3 location of the user’s script as specified in the CreateJob request’s
 ScriptModeConfig
os.environ["AMZN_BRAKET_SCRIPT_S3_URI"]
# the S3 location where the SDK would store the quantum task results by default for the job
os.environ["AMZN_BRAKET_TASK_RESULTS_S3_URI"]
# the S3 location where the job results would be stored, as specified in CreateJob
 request’s OutputDataConfig
os.environ["AMZN_BRAKET_JOB_RESULTS_S3_PATH"]
# the string that should be passed to CreateQuantumTask’s jobToken parameter for quantum
 tasks created in the job container
os.environ["AMZN_BRAKET_JOB_TOKEN"]
143
Amazon Braket Developer Guide
Helper functions
Helper functions
Amazon Braket provides several helper functions to simplify the interactions with container inputs and
outputs. These helper functions would be called from within the algorithm script that is used to run your
Hybrid Job. The following example demonstrates how to use them.
get_checkpoint_dir() # get the checkpoint directory
get_hyperparameters() # get the hyperparameters as strings
get_input_data_dir() # get the input data directory
get_job_device_arn() # get the device specified by the hybrid job
get_job_name() # get the name of the hybrid job.
get_results_dir() # get the path to a results directory
save_job_result() # save hybrid job results
save_job_checkpoint() # save a checkpoint
load_job_checkpoint() # load a previously saved checkpoint
Save job results
You can save the results generated by the algorithm script so that they are available from the hybrid job
object in the hybrid job script as well as from the output folder in Amazon S3 (in a tar-zipped file named
model.tar.gz). The output must be saved in a file using a JavaScript Object Notation (JSON) format. To
save the results of the hybrid jobs, you add the following lines commented with #ADD to the algorithm
script.
from braket.aws import AwsDevice
from braket.circuits import Circuit
from braket.jobs import save_job_result #ADD
def start_here():
 print("Test job started!!!!!")
 device = AwsDevice(os.environ['AMZN_BRAKET_DEVICE_ARN'])
 results = [] #ADD
 bell = Circuit().h(0).cnot(0, 1)
 for count in range(5):
 task = device.run(bell, shots=100)
 print(task.result().measurement_counts)
 results.append(task.result().measurement_counts) #ADD
 save_job_result({ "measurement_counts": results }) #ADD
 print("Test job completed!!!!!")
You can then display the results of the job from your job script by appending the line
print(job.result()) commented with #ADD.
import time
from braket.aws import AwsQuantumJob
job = AwsQuantumJob.create(
 source_module="algorithm_script.py",
 entry_point="algorithm_script:start_here",
 device_arn="arn:aws:braket:::device/quantum-simulator/amazon/sv1",
)
144
Amazon Braket Developer Guide
Save and restart hybrid jobs using checkpoints
print(job.arn)
while job.state() not in AwsQuantumJob.TERMINAL_STATES:
 print(job.state())
 time.sleep(10)
print(job.state())
print(job.result()) #ADD
In this example, we have removed wait_until_complete=True to suppress verbose output. You can
add it back in for debugging. When you run this hybrid job, it outputs the identifier and the job-arn,
followed by the state of the hybrid job every 10 seconds until the hybrid job is COMPLETED, after which it
shows you the results of the bell circuit. See the following example.
arn:aws:braket:us-west-2:111122223333:job/braket-job-default-1234567890123
INITIALIZED
RUNNING
RUNNING
RUNNING
RUNNING
RUNNING
RUNNING
RUNNING
RUNNING
RUNNING
RUNNING
...
RUNNING
RUNNING
COMPLETED
{'measurement_counts': [{'11': 53, '00': 47},..., {'00': 51, '11': 49}]}
Save and restart hybrid jobs using checkpoints
You can save intermediate iterations of your hybrid jobs using checkpoints. In the algorithm script
example from the previous section, you would add the following lines commented with #ADD to create
checkpoint files.
from braket.aws import AwsDevice
from braket.circuits import Circuit
from braket.jobs import save_job_checkpoint #ADD
import os
def start_here():
 print("Test job starts!!!!!")
 device = AwsDevice(os.environ["AMZN_BRAKET_DEVICE_ARN"])
 #ADD the following code
 job_name = os.environ["AMZN_BRAKET_JOB_NAME"]
 save_job_checkpoint(
 checkpoint_data={"data": f"data for checkpoint from {job_name}"},
 checkpoint_file_suffix="checkpoint-1",
 ) #End of ADD
 bell = Circuit().h(0).cnot(0, 1)
 for count in range(5):
 task = device.run(bell, shots=100)
 print(task.result().measurement_counts)
145
Amazon Braket Developer Guide
Define the environment for your algorithm script
 print("Test hybrid job completed!!!!!")
When you run the hybrid job, it creates the file <jobname>-checkpoint-1.json in your hybrid job artifacts
in the checkpoints directory with a default /opt/jobs/checkpoints path. The hybrid job script
remains unchanged unless you want to change this default path.
If you want to load a hybrid job from a checkpoint generated by a previous hybrid job, the algorithm
script uses from braket.jobs import load_job_checkpoint. The logic to load in your algorithm
script is as follows.
checkpoint_1 = load_job_checkpoint(
 "previous_job_name",
 checkpoint_file_suffix="checkpoint-1",
)
After loading this checkpoint, you can continue your logic based on the content loaded to
checkpoint-1.
Note
The checkpoint_file_suffix must match the suffix previously specified when creating the
checkpoint.
Your orchestration script needs to specify the job-arn from the previous hybrid job with the line
commented with #ADD.
job = AwsQuantumJob.create(
 source_module="source_dir",
 entry_point="source_dir.algorithm_script:start_here",
 device_arn="arn:aws:braket:::device/quantum-simulator/amazon/sv1",
 copy_checkpoints_from_job="arn:aws:braket:<region>:<account-id>:job/
<previous_job_name>", #ADD
 )
Define the environment for your algorithm script
Amazon Braket supports three environments defined by containers for your algorithm script:
• A base container (the default, if no image_uri is specified)
• A container with Tensorflow and PennyLane
• A container with PyTorch and PennyLane
The following table provides details about the containers and the libraries they include.
Amazon Braket containers
Type PennyLaneTensorFlow:2.11.0-gpupy39-ubuntu20.04
PennyLanePyTorch1.13.1-gpu-py39-
ubuntu20.04
Braket-Base:1.0.0-cpu-py39-
ubuntu22.04
Base 292282985366.dkr.ecr.useast-1.amazonaws.com/
amazon-brakettensorflow-jobs:2.11.0-
292282985366.dkr.ecr.uswest-2.amazonaws.com/
amazon-braket-pytorchjobs:1.13.1-gpu-py39-
cu117-ubuntu20.04
292282985366.dkr.ecr.uswest-2.amazonaws.com/
amazon-braket-base-jobs:1.0-
cpu-py39-ubuntu22.04
146
Amazon Braket Developer Guide
Define the environment for your algorithm script
Type PennyLaneTensorFlow:2.11.0-gpupy39-ubuntu20.04
PennyLanePyTorch1.13.1-gpu-py39-
ubuntu20.04
Braket-Base:1.0.0-cpu-py39-
ubuntu22.04
gpu-py39-cu112-
ubuntu20.04
Inherited
Libraries
• awscli
• numpy
• pandas
• scipy
• awscli
• numpy
• pandas
• scipy
Additional
Libraries
• amazon-braket-defaultsimulator
• amazon-braketpennylane-plugin
• amazon-braket-schemas
• amazon-braket-sdk
• ipykernel
• keras
• matplotlib
• networkx
• openbabel
• PennyLane
• protobuf
• psi4
• rsa
• PennyLane-Lightninggpu
• cuQuantum
• amazon-braket-defaultsimulator
• amazon-braketpennylane-plugin
• amazon-braket-schemas
• amazon-braket-sdk
• ipykernel
• keras
• matplotlib
• networkx
• openbabel
• PennyLane
• protobuf
• psi4
• rsa
• PennyLane-Lightninggpu
• cuQuantum
• amazon-braket-defaultsimulator
• amazon-braket-pennylaneplugin
• amazon-braket-schemas
• amazon-braket-sdk
• awscli
• boto3
• ipykernel
• matplotlib
• networkx
• numpy
• openbabel
• pandas
• PennyLane
• protobuf
• psi4
• rsa
• scipy
You can view and access the open source container definitions at aws/amazon-braket-containers. Choose
the container that best matches your use case. The container must be in the AWS Region from which
you invoke your hybrid job. You specify the container image when you create a hybrid job by adding
one of the following three arguments to your create(…) call in the hybrid job script. You can install
additional dependencies into the container you choose at runtime (at the cost of startup or runtime)
because the Amazon Braket containers have internet connectivity. The following example is for the uswest-2 Region.
• Base image image_uri="292282985366.dkr.ecr.us-west-2.amazonaws.com/amazon-braket-basejobs:1.0-cpu-py39-ubuntu22.04"
• Tensorflow image image_uri="292282985366.dkr.ecr.us-east-1.amazonaws.com/amazon-brakettensorflow-jobs:2.11.0-gpu-py39-cu112-ubuntu20.04"
• PyTorch image image_uri="292282985366.dkr.ecr.us-west-2.amazonaws.com/amazon-braketpytorch-jobs:1.13.1-gpu-py39-cu117-ubuntu20.04"
The image-uris can also be retrieved using the retrieve_image() function in the Amazon Braket
SDK. The following example shows how to retrieve them from the us-west-2 AWS Region.
from braket.jobs.image_uris import retrieve_image, Framework
147
Amazon Braket Developer Guide
Use hyperparameters
image_uri_base = retrieve_image(Framework.BASE, "us-west-2")
image_uri_tf = retrieve_image(Framework.PL_TENSORFLOW, "us-west-2")
image_uri_pytorch = retrieve_image(Framework.PL_PYTORCH, "us-west-2")
Use hyperparameters
You can define hyperparameters needed by your algorithm, such as the learning rate or step size, when
you create a hybrid job. Hyperparameter values are typically used to control various aspects of the
algorithm, and can often be tuned to optimize the algorithm’s performance. To use hyperparameters in
a Braket hybrid job, you need to specify their names and values explicitly as a dictionary. Note that the
values must be of the string datatype. You specify the hyperparameter values that you want to test when
searching for the optimal set of values. The first step to using hyperparameters is to set up and define
the hyperparameters as a dictionary, which can be seen in the following code:
#defining the number of qubits used
n_qubits = 8
#defining the number of layers used
n_layers = 10
#defining the number of iterations used for your optimization algorithm
n_iterations = 10
hyperparams = {
 "n_qubits": n_qubits,
 "n_layers": n_layers,
 "n_iterations": n_iterations
}
You would then pass the hyperparameters defined in the code snippet given above to be used in the
algorithm of your choice with something that looks like the following:
import time
from braket.aws import AwsQuantumJob
#Name your job so that it can be later identified
job_name = f"qcbm-gaussian-training-{n_qubits}-{n_layers}-" + str(int(time.time()))
job = AwsQuantumJob.create(
 #Run this hybrid job on the SV1 simulator
 device="arn:aws:braket:::device/quantum-simulator/amazon/sv1",
 #The directory or single file containing the code to run.
 source_module="qcbm",
 #The main script or function the job will run.
 entry_point="qcbm.qcbm_job:main",
 #Set the job_name
 job_name=job_name,
 #Set the hyperparameters
 hyperparameters=hyperparams,
 #Define the file that contains the input data
 input_data="data.npy", # or input_data=s3_path
 # wait_until_complete=False,
)
Note
In order to learn more about input data see the Inputs (p. 142) section.
The hyperparameters would then be loaded into the hybrid job script using the following code:
import json
148
Amazon Braket Developer Guide
Configure the hybrid job instance
to run your algorithm script
import os
#Load the Hybrid Job hyperparameters
hp_file = os.environ["AMZN_BRAKET_HP_FILE"]
with open(hp_file, "r") as f:
 hyperparams = json.load(f)
Note
For more information about how to pass information like the input data and the device arn to
the hybrid job script, see this github page.
A couple guides that are very useful for learning about how to use hyperparameters are given by the
QAOA with Amazon Braket Hybrid Jobs and PennyLane and Quantum machine learning in Amazon
Braket Hybrid Jobs tutorials.
Configure the hybrid job instance to run your
algorithm script
Depending on your algorithm, you may have different requirements. By default, Amazon Braket runs
your algorithm script on an ml.m5.large instance. However, you can customize this instance type when
you create a hybrid job using the following import and configuration argument.
from braket.jobs.config import InstanceConfig
job = AwsQuantumJob.create(
 ...
 instance_config=InstanceConfig(instanceType="ml.p3.8xlarge"), # Use NVIDIA Tesla V100
 instance with 4 GPUs.
 ...
 ),
If you are running an embedded simulation and have specified a local device in the device configuration,
you will be able to additionally request more than one instance in the InstanceConfig by specifying the
instanceCount and setting it to be greater than one. The upper limit is 5. For instance, you can choose 3
instances as follows.
from braket.jobs.config import InstanceConfig
job = AwsQuantumJob.create(
 ...
 instance_config=InstanceConfig(instanceType="ml.p3.8xlarge", instanceCount=3), # Use 3
 NVIDIA Tesla V100
 ...
 ),
When you use multiple instances, consider distributing your hybrid job using the data parallel feature.
See the following example notebook for more details on how-to see this Braket example.
The following three tables list the available instance types and specs for standard, compute optimized,
and accelerated computing instances.
Note
To view the default classical compute instance quotas for Hybrid Jobs, see this page (p. 23).
Standard Instances vCPU Memory
ml.m5.large (default) 2 8 GiB
149
Amazon Braket Developer Guide
Configure the hybrid job instance
to run your algorithm script
Standard Instances vCPU Memory
ml.m5.xlarge 4 16 GiB
ml.m5.2xlarge 8 32 GiB
ml.m5.4xlarge 16 64 GiB
ml.m5.12xlarge 48 192 GiB
ml.m5.24xlarge 96 384 GiB
ml.m4.xlarge 4 16 GiB
ml.m4.2xlarge 8 32 GiB
ml.m4.4xlarge 16 64 GiB
ml.m4.10xlarge 40 256 GiB
Compute Optimized Instances vCPU Memory
ml.c4.xlarge 4 7.5 GiB
ml.c4.2xlarge 8 15 GiB
ml.c4.4xlarge 16 30 GiB
ml.c4.8xlarge 36 192 GiB
ml.c5.xlarge 4 8 GiB
ml.c5.2xlarge 8 16 GiB
ml.c5.4xlarge 16 32 GiB
ml.c5.9xlarge 36 72 GiB
ml.c5.18xlarge 72 144 GiB
ml.c5n.xlarge 4 10.5 GiB
ml.c5n.2xlarge 8 21 GiB
ml.c5n.4xlarge 16 42 GiB
ml.c5n.9xlarge 36 96 GiB
ml.c5n.18xlarge 72 192 GiB
Accelerated Compting
Instances
vCPU Memory
ml.p2.xlarge 4 61 GiB
ml.p2.8xlarge 32 488 GiB
ml.p2.16xlarge 64 732 GiB
150
Amazon Braket Developer Guide
Cancel a Hybrid Job
Accelerated Compting
Instances
vCPU Memory
ml.p3.2xlarge 8 61 GiB
ml.p3.8xlarge 32 244 GiB
ml.p3.16xlarge 64 488 GiB
ml.g4dn.xlarge 4 16 GiB
ml.g4dn.2xlarge 8 32 GiB
ml.g4dn.4xlarge 16 64 GiB
ml.g4dn.8xlarge 32 128 GiB
ml.g4dn.12xlarge 48 192 GiB
ml.g4dn.16xlarge 64 256 GiB
Note
p3 instances are not available in us-west-1. If your hybrid job is unable to provision requested
ML compute capacity, use another Region.
Each instance uses a default configuration of data storage (SSD) of 30 GB. But you can adjust the storage
in the same way that you configure the instanceType. The following example shows how to increase
the total storage to 50 GB.
from braket.jobs.config import InstanceConfig
job = AwsQuantumJob.create(
 ...
 instance_config=InstanceConfig(
 instanceType="ml.p3.8xlarge",
 volumeSizeInGb=50,
 ),
 ...
 ),
Cancel a Hybrid Job
You may need to cancel a hybrid job in a non-terminal state. This can be done either in the console or
with code.
To cancel your hybrid job in the console, select the hybrid job to cancel from the Hybrid Jobs page and
then select Cancel hybrid job from the Actions dropdown menu.
151
Amazon Braket Developer Guide
Using parametric compilation to speed up Hybrid Jobs
To confirm the cancellation, enter cancel into the input field when prompted and then select OK.
To cancel your hybrid job using code from the Braket Python SDK, use the job_arn to identify the
hybrid job and then call the cancel command on it as shown in following code.
job = AwsQuantumJob(arn=job_arn)
job.cancel()
The cancel command terminates the classical hybrid job container immediately and does a best effort
to cancel all of the related quantum tasks that are still in a non-terminal state.
Using parametric compilation to speed up Hybrid
Jobs
Amazon Braket supports parametric compilation on certain QPUs. This enables you to reduce the
overhead associated with the computationally expensive compilation step by compiling a circuit only
once and not for every iteration in your hybrid algorithm. This can improve runtimes dramatically for
Hybrid Jobs, since you avoid the need to recompile your circuit at each step. Just submit parametrized
circuits to one of our supported QPUs as a Braket Hybrid Job. For long running hybrid jobs, Braket
152
Amazon Braket Developer Guide
Use Amazon Braket Hybrid Jobs and
PennyLane to run a QAOA algorithm
automatically uses the updated calibration data from the hardware provider when compiling your circuit
to ensure the highest quality results.
To create a parametric circuit, you first need to provide parameters as inputs in your algorithm script.
In this example, we use a small parametric circuit and ignore any classical processing between each
iteration. For typical workloads, you would submit many circuits in batch and perform classical
processing such as updating the parameters in each iteration.
import os
from braket.aws import AwsDevice
from braket.circuits import Circuit, FreeParameter
def start_here():
 print("Test job started.")
 # Use the device declared in the job script
 device = AwsDevice(os.environ["AMZN_BRAKET_DEVICE_ARN"])
 circuit = Circuit().rx(0, FreeParameter("theta"))
 parameter_list = [0.1, 0.2, 0.3]

 for parameter in parameter_list:
 result = device.run(circuit, shots=1000, inputs={"theta": parameter})
 print("Test job completed.")
You can submit the algorithm script to run as a Hybrid Job with the following job script. When running
the Hybrid Job on a QPU that supports parametric compilation, the circuit is compiled only on the first
run. In following runs, the compiled circuit is reused, increasing the runtime performance of the Hybrid
Job without any additional lines of code.
from braket.aws import AwsQuantumJob
job = AwsQuantumJob.create(
 device=device_arn,
 source_module="algorithm_script.py",
)
Note
Parametric compilation is supported on all superconducting, gate-based QPUs from Rigetti
Computing.
Use Amazon Braket Hybrid Jobs and PennyLane to
run a QAOA algorithm
In this section, you’ll use what you’ve learned to write an actual hybrid program using PennyLane with
parametric compilation. You use the algorithm script to address a Quantum Approximate Optimization
Algorithm (QAOA) problem. The program creates a cost function corresponding to a classical Max Cut
optimization problem, specifies a parametrized quantum circuit, and uses a simple gradient descent
method to optimize the parameters so that the cost function is minimized. In this example, we generate
the problem graph in the algorithm script for simplicity, but for more typical use cases the best practice
is to provide the problem specification through a dedicated channel in the input data configuration.
The flag parametrize_differentiable defaults to True so you automatically get the benefits of
improved runtime performance from parametric compilation on supported QPUs.
153
Amazon Braket Developer Guide
Use Amazon Braket Hybrid Jobs and
PennyLane to run a QAOA algorithm
import os
import json
import time
from braket.jobs import save_job_result
from braket.jobs.metrics import log_metric
import networkx as nx
import pennylane as qml
from pennylane import numpy as np
from matplotlib import pyplot as plt
def init_pl_device(device_arn, num_nodes, shots, max_parallel):
 return qml.device(
 "braket.aws.qubit",
 device_arn=device_arn,
 wires=num_nodes,
 shots=shots,
 # Set s3_destination_folder=None to output task results to a default folder
 s3_destination_folder=None,
 parallel=True,
 max_parallel=max_parallel,
 parametrize_differentiable=True, # This flag is True by default.
 )
def start_here():
 input_dir = os.environ["AMZN_BRAKET_INPUT_DIR"]
 output_dir = os.environ["AMZN_BRAKET_JOB_RESULTS_DIR"]
 job_name = os.environ["AMZN_BRAKET_JOB_NAME"]
 checkpoint_dir = os.environ["AMZN_BRAKET_CHECKPOINT_DIR"]
 hp_file = os.environ["AMZN_BRAKET_HP_FILE"]
 device_arn = os.environ["AMZN_BRAKET_DEVICE_ARN"]
 # Read the hyperparameters
 with open(hp_file, "r") as f:
 hyperparams = json.load(f)
 p = int(hyperparams["p"])
 seed = int(hyperparams["seed"])
 max_parallel = int(hyperparams["max_parallel"])
 num_iterations = int(hyperparams["num_iterations"])
 stepsize = float(hyperparams["stepsize"])
 shots = int(hyperparams["shots"])
 # Generate random graph
 num_nodes = 6
 num_edges = 8
 graph_seed = 1967
 g = nx.gnm_random_graph(num_nodes, num_edges, seed=graph_seed)
 # Output figure to file
 positions = nx.spring_layout(g, seed=seed)
 nx.draw(g, with_labels=True, pos=positions, node_size=600)
 plt.savefig(f"{output_dir}/graph.png")
 # Set up the QAOA problem
 cost_h, mixer_h = qml.qaoa.maxcut(g)
 def qaoa_layer(gamma, alpha):
 qml.qaoa.cost_layer(gamma, cost_h)
 qml.qaoa.mixer_layer(alpha, mixer_h)
 def circuit(params, **kwargs):
 for i in range(num_nodes):
 qml.Hadamard(wires=i)
154
Amazon Braket Developer Guide
Accelerate your hybrid workloads with
embedded simulators from PennyLane
 qml.layer(qaoa_layer, p, params[0], params[1])
 dev = init_pl_device(device_arn, num_nodes, shots, max_parallel)
 np.random.seed(seed)
 cost_function = qml.ExpvalCost(circuit, cost_h, dev, optimize=True)
 params = 0.01 * np.random.uniform(size=[2, p])
 optimizer = qml.GradientDescentOptimizer(stepsize=stepsize)
 print("Optimization start")
 for iteration in range(num_iterations):
 t0 = time.time()
 # Evaluates the cost, then does a gradient step to new params
 params, cost_before = optimizer.step_and_cost(cost_function, params)
 # Convert cost_before to a float so it's easier to handle
 cost_before = float(cost_before)
 t1 = time.time()
 if iteration == 0:
 print("Initial cost:", cost_before)
 else:
 print(f"Cost at step {iteration}:", cost_before)
 # Log the current loss as a metric
 log_metric(
 metric_name="Cost",
 value=cost_before,
 iteration_number=iteration,
 )
 print(f"Completed iteration {iteration + 1}")
 print(f"Time to complete iteration: {t1 - t0} seconds")
 final_cost = float(cost_function(params))
 log_metric(
 metric_name="Cost",
 value=final_cost,
 iteration_number=num_iterations,
 )
 # We're done with the hybrid job, so save the result.
 # This will be returned in job.result()
 save_job_result({"params": params.numpy().tolist(), "cost": final_cost})
Note
Parametric compilation is supported on all superconducting, gate-based QPUs from Rigetti
Computing.
Accelerate your hybrid workloads with embedded
simulators from PennyLane
Let’s look at how you can use embedded simulators from PennyLane on Amazon Braket Hybrid Jobs to
run hybrid workloads. Pennylane’s GPU-based embedded simulator, lightning.gpu, uses the Nvidia
cuQuantum library to accelerate circuit simulations. The embedded GPU simulator is pre-configured in
all of the Braket job containers that users can use out of the box. In this page, we show you how to use
lightning.gpu to speed up your hybrid workloads.
155
Amazon Braket Developer Guide
Using lightning.gpu for Quantum
Approximate Optimization Algorithm workloads
Using lightning.gpu for Quantum Approximate
Optimization Algorithm workloads
Consider the Quantum Approximate Optimization Algorithm (QAOA) examples from this notebook.
To select an embedded simulator, you specify the device argument to be a string of the form:
"local:<provider>/<simulator_name>". For example, you would set "local:pennylane/
lightning.gpu" for lightning.gpu. The device string you give to the Hybrid Job when you launch is
passed to the job as the environment variable "AMZN_BRAKET_DEVICE_ARN".
device_string = os.environ["AMZN_BRAKET_DEVICE_ARN"]
prefix, device_name = device_string.split("/")
device = qml.device(simulator_name, wires=n_wires)
In this page, let’s compare the two embedded PennyLane state vector simulators lightning.qubit
(which is CPU-based) and lightning.gpu (which is GPU-based). You’ll need to provide the simulators
with some custom gate decompositions in order to compute various gradients.
Now you’re ready to prepare the hybrid job launching script. You’ll run the QAOA algorithm using two
instance types: m5.2xlarge and p3.2xlarge. The m5.2xlarge instance type is comparable to a
standard developer laptop. The p3.2xlarge is an accelerated computing instance that has a single
NVIDIA Volta GPU with 16GB of memory.
The hyperparameters for all your hybrid jobs will be the same. All you need to do to try out different
instances and simulators is change two lines as follows.
# Specify device that the hybrid job will primarily be targeting
device = "local:pennylane/lightning.qubit"
# Run on a CPU based instance with about as much power as a laptop
instance_config = InstanceConfig(instanceType='ml.m5.2xlarge')
or:
# Specify device that the hybrid job will primarily be targeting
device = "local:pennylane/lightning.gpu"
# Run on an inexpensive GPU based instance
instance_config = InstanceConfig(instanceType='ml.p3.2xlarge')
Note
If you specify the instance_config as using a GPU-based instance, but choose the device to
be the embedded CPU-based simulator (lightning.qubit), the GPU will not be used. Make
sure to use the embedded GPU-based simulator if you wish to target the GPU!
First, you can create two hybrid jobs and solve Max-Cut with QAOA on a graph with 18 vertices. This
translates to an 18-qubit circuit—relatively small and feasible to run quickly on your laptop or the
m5.2xlarge instance.
num_nodes = 18
num_edges = 24
seed = 1967
graph = nx.gnm_random_graph(num_nodes, num_edges, seed=seed)
# And similarly for the p3 job
m5_job = AwsQuantumJob.create(
 device=device,
 source_module="qaoa_source",
 job_name="qaoa-m5-" + str(int(time.time())),
156
Amazon Braket Developer Guide
Quantum machine learning and data parallelism
 image_uri=image_uri,
 # Relative to the source_module
 entry_point="qaoa_source.qaoa_algorithm_script",
 copy_checkpoints_from_job=None,
 instance_config=instance_config,
 # general parameters
 hyperparameters=hyperparameters,
 input_data={"input-graph": input_file_path},
 wait_until_complete=True,
)
The mean iteration time for the m5.2xlarge instance is about 25 seconds, while for the p3.2xlarge
instance it’s about 12 seconds. For this 18-qubit workflow, the GPU instance gives us a 2x speedup.
If you look at the Amazon Braket Hybrid Jobs pricing page, you can see that the cost per minute for
an m5.2xlarge instance is $0.00768, while for the p3.2xlarge instance it’s $0.06375. To run for 5
total iterations, as you did here, would cost $0.016 using the CPU instance or $0.06375 using the GPU
instance — both pretty inexpensive!
Now let’s make the problem harder, and try solving a Max-Cut problem on a 24-vertex graph, which will
translate to 24 qubits. Run the hybrid jobs again on the same two instances and compare the cost.
Note
You’ll see that the time to run this hybrid job on the CPU instance may be about five hours!
num_nodes = 24
num_edges = 36
seed = 1967
graph = nx.gnm_random_graph(num_nodes, num_edges, seed=seed)
# And similarly for the p3 job
m5_big_job = AwsQuantumJob.create(
 device=device,
 source_module="qaoa_source",
 job_name="qaoa-m5-big-" + str(int(time.time())),
 image_uri=image_uri,
 # Relative to the source_module
 entry_point="qaoa_source.qaoa_algorithm_script",
 copy_checkpoints_from_job=None,
 instance_config=instance_config,
 # general parameters
 hyperparameters=hyperparameters,
 input_data={"input-graph": input_file_path},
 wait_until_complete=True,
)
The mean iteration time for the m5.2xlarge instance is roughly an hour, while for the p3.2xlarge
instance it’s roughly two minutes. For this larger problem, the GPU instance is an order of magnitude
faster! All you had to do to benefit from this speedup was to change two lines of code, swapping out
the instance type and the local simulator used. To run for 5 total iterations, as was done here, would
cost about $2.27072 using the CPU instance or about $0.775625 using the GPU instance. The CPU
usage is not only more expensive, but also takes more time to run. Accelerating this workflow with a
GPU instance available on AWS, using PennyLane’s embedded simulator backed by NVIDIA CuQuantum,
allows you to run workflows with intermediate qubit counts (between 20 and 30) for less total cost and
in less time. This means you can experiment with quantum computing even for problems that are too big
to run quickly on your laptop or a similarly-sized instance.
Quantum machine learning and data parallelism
If your workload type is quantum machine learning (QML) that trains on datasets, you can further
accelerate your workload using data parallelism. In QML, the model contains one or more quantum
157
Amazon Braket Developer Guide
Quantum machine learning and data parallelism
circuits. The model may or may not also contain classical neural nets. When training the model with the
dataset, the parameters in the model are updated to minimize the loss function. A loss function is usually
defined for a single data point, and the total loss for the average loss over the whole dataset. In QML,
the losses are usually computed in serial before averaging to total loss for gradient computations. This
procedure is time consuming, especially when there are hundreds of data points.
Because the loss from one data point does not depend on other data points, the losses can be evaluated
in parallel! Losses and gradients associated with different data points can be evaluated at the same time.
This is known as data parallelism. With SageMaker’s distributed data parallel library, Amazon Braket
Hybrid Jobs make it easier for you to leverage data parallelism to accelerate your training.
Consider the following QML workload for data parallelism which uses the Sonar dataset dataset from
the well-known UCI repository as an example for binary classification. The Sonar dataset have 208 data
points each with 60 features that are collected from sonar signals bouncing off materials. Each data
points is either labeled as "M" for mines or "R" for rocks. Our QML model consists of an input layer, a
quantum circuit as a hidden layer, and an output layer. The input and output layers are classical neural
nets implemented in PyTorch. The quantum circuit is integrated with the PyTorch neural nets using
PennyLane’s qml.qnn module. See our example notebooks for more detail about the workload. Like the
QAOA example above, you can harness the power of GPU by using embedded GPU-based simulators like
PennyLane’s lightning.gpu to improve the performance over embedded CPU-based simulators.
To create a hybrid job, you can call AwsQuantumJob.create and specify the algorithm script, device,
and other configurations through its keyword arguments.
instance_config = InstanceConfig(instanceType='ml.p3.2xlarge')
hyperparameters={"nwires": "10",
 "ndata": "32",
 ...
}
job = AwsQuantumJob.create(
 device="local:pennylane/lightning.gpu",
 source_module="qml_source",
 entry_point="qml_source.train_single",
 hyperparameters=hyperparameters,
 instance_config=instance_config,
 ...
)
In order to use data parallelism, you need to modify few lines of code in the algorithm script for the
SageMaker distributed library to correctly parallelize the training. First, you import the smdistributed
package which does most of the heavy-lifting for distributing your workloads across multiple GPUs and
multiple instances. This package is preconfigured in the Braket PyTorch and TensorFlow containers. The
dist module tells our algorithm script what the total number of GPUs for the training (world_size)
is as well as the rank and local_rank of a GPU core. rank is the absolute index of a GPU across
all instances, while local_rank is the index of a GPU within an instance. For example, if there are
four instances each with eight GPUs allocated for the training, the rank ranges from 0 to 31 and the
local_rank ranges from 0 to 7.
import smdistributed.dataparallel.torch.distributed as dist
dp_info = {
 "world_size": dist.get_world_size(),
 "rank": dist.get_rank(),
 "local_rank": dist.get_local_rank(),
}
batch_size //= dp_info["world_size"] // 8
batch_size = max(batch_size, 1)
158
Amazon Braket Developer Guide
Quantum machine learning and data parallelism
Next, you define a DistributedSampler according to the world_size and rank and then pass it into
the data loader. This sampler avoids GPUs accessing the same slice of a dataset.
train_sampler = torch.utils.data.distributed.DistributedSampler(
 train_dataset,
 num_replicas=dp_info["world_size"],
 rank=dp_info["rank"]
)
train_loader = torch.utils.data.DataLoader(
 train_dataset,
 batch_size=batch_size,
 shuffle=False,
 num_workers=0,
 pin_memory=True,
 sampler=train_sampler,
)
Next, you use the DistributedDataParallel class to enable data parallelism.
from smdistributed.dataparallel.torch.parallel.distributed import DistributedDataParallel
 as DDP
model = DressedQNN(qc_dev).to(device)
model = DDP(model)
torch.cuda.set_device(dp_info["local_rank"])
model.cuda(dp_info["local_rank"])
The above are the changes you need to use data parallelism. In QML, you often want to save results and
print training progress. If each GPU executes the saving and printing command, the log will be flooded
with the repeated information and the results will overwrite each other. To avoid this, you can only save
and print from the GPU that has rank 0.
if dp_info["rank"]==0:
 print('elapsed time: ', elapsed)
 torch.save(model.state_dict(), f"{output_dir}/test_local.pt")
 save_job_result({"last loss": loss_before})
Amazon Braket Hybrid Jobs supports ml.p3.16xlarge instance types for the SageMaker distributed
data parallel library. You configure the instance type through the InstanceConfig argument in Hybrid
Jobs. For the SageMaker distributed data parallel library to know that data parallelism is enabled, you
need to add two additional hyperparameters, "sagemaker_distributed_dataparallel_enabled"
setting to "true" and "sagemaker_instance_type" setting to the instance type you are using.
These two hyperparameters are used by smdistributed package. Your algorithm script does not
need to explicitly use them. In Amazon Braket SDK, it provides a convenient keyword argument
distribution. With distribution="data_parallel" in hybrid job creation, the Amazon Braket
SDK automatically inserts the two hyperparameters for you. If you use the Amazon Braket API, you need
to include these two hyperparameters.
With the instance and data parallelism configured, you can now submit your hybrid job. There are 8 GPUs
in a ml.p3.16xlarge instance. When you set instanceCount=1 , the workload is distributed across
the 8 GPUs in the instance. When you set instanceCount greater than one, the workload is distributed
across GPUs available in all instances. When using multiple instances, each instance incurs a charge
based on how much time you use it. For example, when you use four instances, the billable time is four
times the run time per instance because there are four instances running your workloads at the same
time.
instance_config = InstanceConfig(instanceType='ml.p3.16xlarge',
159
Amazon Braket Developer Guide
Build and debug a hybrid job with local mode
 instanceCount=1,
)
hyperparameters={"nwires": "10",
 "ndata": "32",
 ...,
}
job = AwsQuantumJob.create(
 device="local:pennylane/lightning.gpu",
 source_module="qml_source",
 entry_point="qml_source.train_dp",
 hyperparameters=hyperparameters,
 instance_config=instance_config,
 distribution="data_parallel",
 ...
)
Note
In the above hybrid job creation, train_dp.py is the modified algorithm script for using
data parallelism. Keep in mind that data parallelism only works correctly when you modify
your algorithm script according to the above section. If the data parallelism option is enabled
without a correctly modified algorithm script, the hybrid job may throw errors, or each GPU may
repeatedly process the same data slice, which is inefficient.
Let’s compare the run time and cost in an example where when train a model with a 26-qubit quantum
circuit for the binary classification problem mentioned above. The ml.p3.16xlarge instance used
in this example costs $0.4692 per minute. Without data parallelism, it takes the simulator about 45
minutes to train the model for 1 epoch (i.e., over 208 data points) and it costs about $20. With data
parallelism across 1 instance and 4 instances, it only takes 6 minutes and 1.5 minutes respectively, which
translates to roughly $2.8 for both. By using data parallelism across 4 instances, you not only improve
the run time by 30x, but also reduce costs by an order of magnitude!
Build and debug a hybrid job with local mode
If you are building a new hybrid algorithm, local mode helps you to debug and test your algorithm script.
Local mode is a feature that allows you to run code you plan to use in Amazon Braket Hybrid Jobs, but
without needing Braket to manage the infrastructure for running the hybrid job. Instead, you run hybrid
jobs locally on your Braket Notebook instance or on some other preferred client such as a laptop or
desktop computer. In local mode, you can still send quantum tasks to actual devices, but you do not get
the performance benefits when running against an actual QPU while in local mode.
To use local mode, modify AwsQuantumJob to LocalQuantumJob wherever it occurs. For instance, to
run the example from Create your first hybrid job (p. 136), edit the hybrid job script as follows.
from braket.jobs.local import LocalQuantumJob
job = LocalQuantumJob.create(
 device="arn:aws:braket:::device/quantum-simulator/amazon/sv1",
 source_module="algorithm_script.py",
 entry_point="algorithm_script:start_here",
)
Note
Docker, which is already pre-installed in the Amazon Braket notebooks, needs to be installed in
your local environment to use this feature. Instructions for installing Docker can be found here.
In addition, not all parameters are supported in local mode.
160
Amazon Braket Developer Guide
Bring your own container (BYOC)
Bring your own container (BYOC)
Braket Hybrid Jobs provides three pre-built containers for running code in different environments. If
one of these containers supports your use case, you only have to provide your algorithm script when
you create a hybrid job. Minor missing dependencies can be added from your algorithm script or a
requirements.txt file by using pip.
If none of these containers support your use case or if you wish to expand on them, Braket Hybrid Jobs
supports running hybrid jobs with your own custom Docker container image or bring your own container
(BYOC). But before we dive in, let’s make sure it’s actually the right feature for your use case.
When is bringing my own container the right
decision?
Bringing your own container (BYOC) to Braket Hybrid Jobs offers the flexibility to use your own software
by installing it in a packaged environment. Depending on your specific needs, there may be ways to
achieve the same flexibility without having to go through the full BYOC Docker build - Amazon ECR
upload - custom image URI cycle.
Note
BYOC may not be the right choice if you want to add a small (generally fewer than 10) number
of additional Python packages which are publicly available (for example, via PyPi).
In this case, you can use one of the prebuilt Braket images, and then include a requirements.txt file
in your source directory at job submission, which will automatically be read. pip will install the packages
with specified versions as normal. If you are installing a large number of packages, the runtime of your
jobs may be substantially increased. Check the Python and, if applicable, CUDA version of the prebuilt
container you want to use to test if your software will work.
BYOC is necessary when you want to use a non-Python language (like C++ or Rust) for your job script, or
if you want to use a Python version not available through the Braket prebuilt containers. It’s also a good
choice if:
• You are using software with a license key, and you need to authenticate that key against a licensing
server in order to run the software. With BYOC, you can embed the license key in your Docker image
and include code to authenticate it.
• You are using software that isn’t publicly available. For example, the software is hosted on a private
GitLab or GitHub repository, which you need a particular SSH key to access.
• You need to install a large suite of software which isn’t packaged in the Braket provided containers.
BYOC will allow you to eliminate long startup times for your Jobs containers due to software
installation.
BYOC also enables you to make your custom SDK or algorithm available to customers by building a
Docker container with your software and making it available to your users. You can do this by setting
appropriate permissions in Amazon ECR.
Note
You must comply with all applicable software licenses.
Recipe for bringing your own container
In this section, we provide a step-by-step guide of what you’ll need to Bring Your Own Container (BYOC)
to Braket Hybrid Jobs — the scripts, files, and steps to combine them in order to get up and running with
your custom Docker images. Here, we provide recipes for two common cases:
161
Amazon Braket Developer Guide
Recipe for bringing your own container
1. Install additional software in a Docker image and use only Python algorithm scripts in your jobs.
2. Use algorithm scripts written in a non-Python language with Hybrid Jobs, or a CPU architecture
besides x86.
Defining the container entry script is more complex for case 2.
When Braket runs your Hybrid Job, it launches the requested number and type of Amazon EC2 instances,
then runs the Docker image specified by the Image URI input to job creation on them. When using the
BYOC feature, you specify an Image URI hosted in a private Amazon ECR repository to which you have
Read access, and Braket Jobs uses that custom image to run the job.
Ingredients
Here we break out the specific components you will need to build a Docker image that can be used with
Hybrid Jobs. If you’re unfamiliar with writing and building Dockerfiles, we suggest you refer to the
Dockerfile documentation and the Amazon ECR CLI documentation as needed while you read these
instructions.
Here’s an overview of what you’ll need:
• A base image for your Dockerfile. (p. 162)
• (Optional) A modified container entry point script (p. 162)
• A Dockerfile which installs any necessary software and includes the container script (p. 163)
A base image for your Dockerfile.
If you are using Python, and want to install software on top of what’s provided in the Braket vended
containers, a good option for a base image is one of the Braket container images, hosted in our
GitHub repo and on Amazon ECR. You will need to authenticate to Amazon ECR in order to pull the
image and build on top of it. For example, your first line of your BYOC Docker file could read: FROM
[IMAGE_URI_HERE]
Then you can fill out the rest of the Dockerfile to install and setup whatever software you want to add
to the container. The prebuilt Braket images will already contain the appropriate container entry point
script, so you don’t need to worry about including that.
If you want to use a non-Python language, such as C++, Rust, or Julia, or want to build an image for a
non-x86 CPU architecture, like ARM, you may need to build on top of a more barebones public image.
You can find many such images at the Amazon Elastic Container Registry Public Gallery. Make sure you
choose one that is appropriate for the CPU architecture and if necessary, the GPU you want to use.
(Optional) A modified container entry point script
Note
If you are simply adding additional software to a prebuilt Braket image, you can skip this
section!
If you wish to run non-Python code as part of your hybrid job, you’ll need to modify the Python script
which defines the container entry point. An example can be found here. This is the script the images
prebuilt by Braket use to launch your algorithm script and set appropriate environment variables. The
container entry point script itself must be in Python, but can launch non-Python scripts. In the prebuilt
example, you can see that Python algorithm scripts are launched either as a Python subprocess or as a
fully new process. By modifying this logic, you can enable the entry point script to launch non-Python
algorithm scripts. For example, you could modify thekick_off_customer_script() function to
launch Rust processes, dependent on the file extension ending.
162
Amazon Braket Developer Guide
Recipe for bringing your own container
You may also choose to write a completely new braket_container.py if you wish. It should copy
input data, source archives, and other necessary files from S3 into the container, and define the
appropriate environment variables.
A Dockerfile which installs any necessary software and
includes the container script
Note
If you used a prebuilt Braket image as your Docker base image, the container script is already
present.
If you created a modified container script in the previous step, you will need to copy it into the container
and define the environment variable SAGEMAKER_PROGRAM to braket_container.py . Or what you
have named your new container entry point script.
Below we show a minimal example of a Dockerfile which allows you to use Julia on GPU-accelerated
Jobs instances:
FROM nvidia/cuda:12.2.0-devel-ubuntu22.04

 ARG DEBIAN_FRONTEND=noninteractive
 ARG JULIA_RELEASE=1.8
 ARG JULIA_VERSION=1.8.3
 ARG PYTHON=python3.11
 ARG PYTHON_PIP=python3-pip
 ARG PIP=pip
 ARG JULIA_URL = https://julialang-s3.julialang.org/bin/linux/x64/${JULIA_RELEASE}/
 ARG TAR_NAME = julia-${JULIA_VERSION}-linux-x86_64.tar.gz
 ARG PYTHON_PKGS = # list your Python packages and versions here
 RUN curl -s -L ${JULIA_URL}/${TAR_NAME} | tar -C /usr/local -x -z --strip-components=1 -f
 -
 RUN apt-get update \
 && apt-get install -y --no-install-recommends \
 build-essential \
 tzdata \
 openssh-client \
 openssh-server \
 ca-certificates \
 curl \
 git \
 libtemplate-perl \
163
Amazon Braket Developer Guide
Recipe for bringing your own container
 libssl1.1 \
 openssl \
 unzip \
 wget \
 zlib1g-dev \
 ${PYTHON_PIP} \
 ${PYTHON}-dev \
 RUN ${PIP} install --no-cache --upgrade ${PYTHON_PKGS}
 RUN ${PIP} install --no-cache --upgrade sagemaker-training==4.1.3
 # Add EFA and SMDDP to LD library path
 ENV LD_LIBRARY_PATH="/opt/conda/lib/python${PYTHON_SHORT_VERSION}/site-packages/
smdistributed/dataparallel/lib:$LD_LIBRARY_PATH"
 ENV LD_LIBRARY_PATH=/opt/amazon/efa/lib/:$LD_LIBRARY_PATH
 # Julia specific installation instructions
 COPY Project.toml /usr/local/share/julia/environments/v${JULIA_RELEASE}/
 RUN JULIA_DEPOT_PATH=/usr/local/share/julia \
 julia -e 'using Pkg; Pkg.instantiate(); Pkg.API.precompile()'
 # generate the device runtime library for all known and supported devices
 RUN JULIA_DEPOT_PATH=/usr/local/share/julia \
 julia -e 'using CUDA; CUDA.precompile_runtime()'
 # Open source compliance scripts
 RUN HOME_DIR=/root \
 && curl -o ${HOME_DIR}/oss_compliance.zip https://aws-dlinfra-utilities.s3.amazonaws.com/
oss_compliance.zip \
 && unzip ${HOME_DIR}/oss_compliance.zip -d ${HOME_DIR}/ \
 && cp ${HOME_DIR}/oss_compliance/test/testOSSCompliance /usr/local/bin/testOSSCompliance \
 && chmod +x /usr/local/bin/testOSSCompliance \
 && chmod +x ${HOME_DIR}/oss_compliance/generate_oss_compliance.sh \
 && ${HOME_DIR}/oss_compliance/generate_oss_compliance.sh ${HOME_DIR} ${PYTHON} \
 && rm -rf ${HOME_DIR}/oss_compliance*
 # Copying the container entry point script
 COPY braket_container.py /opt/ml/code/braket_container.py
 ENV SAGEMAKER_PROGRAM braket_container.py
In this example, we download and run scripts provided by AWS to ensure we comply with all relevant
Open-Source licenses, for example by properly attributing any installed code governed by an MIT license.
164
Amazon Braket Developer Guide
Running Braket hybrid jobs in your own container
If you need to include non-public code, for instance code that is hosted in a private GitHub or GitLab
repository, do not embed SSH keys in the Docker image to access it. Instead, you should use Docker
Compose when you build to allow Docker to access SSH on the host machine it is built on. For more
information, see the Securely using SSH keys in Docker to access private Github repositories guide.
Building and uploading your Docker image
With a properly defined Dockerfile, you are now ready to follow the steps to create a private Amazon
ECR repository, if one does not already exist, and to build, tag, and upload your container image to it,
following the steps in the Braket Developer Guide (p. 161).
Now you are ready to build, tag, and push the image. See the Docker build documentation for a full
explanation of options to docker build and some examples.
For the sample file defined above, you could run:
aws ecr get-login-password --region ${your_region} | docker login --username AWS --
password-stdin ${aws_account_id}.dkr.ecr.${your_region}.amazonaws.com
 docker build -t braket-julia .
 docker tag braket-julia:latest ${aws_account_id}.dkr.ecr.${your_region}.amazonaws.com/
braket-julia:latest
 docker push ${aws_account_id}.dkr.ecr.${your_region}.amazonaws.com/braket-julia:latest
Assigning appropriate Amazon ECR permissions
Braket Jobs Docker images must be hosted in private Amazon ECR repositories. By default, a private
Amazon ECR repo will not provide read access to the Braket Jobs IAM Role or to any other users who
might want to use your image, such as a collaborator or student. You will need to set a repository
policy in order to grant the appropriate permissions. In general, it’s advisable to provide “as needed”
permissions — only greenlist those specific users and IAM roles you want to allow to access your images,
rather than allowing anyone with the Image URI to pull them.
Running Braket hybrid jobs in your own container
To create a hybrid job with your own container, call AwsQuantumJob.create() with the argument
image_uri specified. You can use a QPU, an on-demand simulator, or run your code locally on the
classical processor available with Braket Hybrid jobs. We recommend testing your code out on a
simulator, like SV1, DM1, or TN1 before running on a real QPU.
To run your code on the classical processor, specify the instanceType and the instanceCount you
wish to use by updating the InstanceConfig. Note that if you specify an instance_count > 1, you
will need to make sure that your code has the ability to run across multiple hosts. The upper limit for the
number of instances you can choose is 5. For example:
job = AwsQuantumJob.create(
 source_module="source_dir",
 entry_point="source_dir.algorithm_script:start_here",
 image_uri="111122223333.dkr.ecr.us-west-2.amazonaws.com/my-byoc-container:latest",
 instance_config=InstanceConfig(instanceType="ml.p3.8xlarge", instanceCount=3),
 device="local:braket/braket.local.qubit",
 # ...)
Note
The device arn allows you to track the simulator you used as hybrid job metadata. Acceptable
values must follow the format device = "local:<provider>/<simulator_name>".
Remember that <provider> and <simulator_name> must consist only of letters, numbers, _,
-, and . . The string is limited to 256 characters.
165
Amazon Braket Developer Guide
Configure the default bucket in AwsSession
If you plan to use BYOC and you are not using the Braket SDK to create quantum tasks, you
should pass the value of the environmental variable AMZN_BRAKET_JOB_TOKEN to the
jobToken parameter in the CreateQuantumTask request. Failing to do so causes the quantum
tasks to not get priority and to be billed as regular standalone quantum tasks.
Configure the default bucket in AwsSession
Providing your own AwsSession gives you greater flexibility, for example, in the location of your
default bucket. By default, an AwsSession has a default bucket location of f"amazon-braket-{id}-
{region}". But you can override that default when creating an AwsSession. Users can optionally pass
in an AwsSession object into AwsQuantumJob.create with the parameter name aws_session as
shown in the following code example.
aws_session = AwsSession(default_bucket="other-default-bucket")
# then you can use that AwsSession when creating a hybrid job
job = AwsQuantumJob.create(
 ...
 aws_session=aws_session
)
Interact with hybrid jobs directly using the API
You can access and interact with Amazon Braket Hybrid Jobs directly using the API. However, defaults
and convenience methods are not available when using the API directly.
Note
We strongly recommend that you interact with Amazon Braket Hybrid Jobs using the Amazon
Braket Python SDK. It offers convenient defaults and protections that help your hybrid jobs run
successfully.
This topic covers the basics of using the API. If you choose to use the API, keep in mind that this
approach can be more complex and be prepared for several iterations to get your hybrid job to run.
To use the API, your account should have a role with the AmazonBraketFullAccess managed policy.
Note
For more information on how to obtain a role with the AmazonBraketFullAccess managed
policy, see the Enable Amazon Braket (p. 36) page.
Additionally, you need an execution role. This role will be passed to the service. You can create the role
using the Amazon Braket console. Use the Execution roles tab on the Permissions and settings page to
create a default role for hybrid jobs.
The CreateJob API requires that you specify all the required parameters for the hybrid job. To use
Python, compress your algorithm script files to a tar bundle, such as an input.tar.gz file, and run the
following script. Update the parts of the code within angled brackets (<>) to match your account
information and entry point that specify the path, file, and method where your hybrid job starts.
from braket.aws import AwsDevice, AwsSession
import boto3
from datetime import datetime
s3_client = boto3.client("s3")
client = boto3.client("braket")
166
Amazon Braket Developer Guide
Interact with hybrid jobs directly using the API
project_name = "job-test"
job_name = project_name + "-" + datetime.strftime(datetime.now(), "%Y%m%d%H%M%S")
bucket = "amazon-braket-<your_bucket>"
s3_prefix = job_name
job_script = "input.tar.gz"
job_object = f"{s3_prefix}/script/{job_script}"
s3_client.upload_file(job_script, bucket, job_object)
input_data = "inputdata.csv"
input_object = f"{s3_prefix}/input/{input_data}"
s3_client.upload_file(input_data, bucket, input_object)
job = client.create_job(
 jobName=job_name,
 roleArn="arn:aws:iam::<your_account>:role/service-role/AmazonBraketJobsExecutionRole",
 # https://docs.aws.amazon.com/braket/latest/developerguide/braket-manageaccess.html#about-amazonbraketjobsexecution
 algorithmSpecification={
 "scriptModeConfig": {
 "entryPoint": "<your_execution_module>:<your_execution_method>",
 "containerImage": {"uri": "292282985366.dkr.ecr.us-west-1.amazonaws.com/amazonbraket-base-jobs:1.0-cpu-py37-ubuntu18.04"} # Change to the specific region you are using
 "s3Uri": f"s3://{bucket}/{job_object}",
 "compressionType": "GZIP"
 }
 },
 inputDataConfig=[
 {
 "channelName": "hellothere",
 "compressionType": "NONE",
 "dataSource": {
 "s3DataSource": {
 "s3Uri": f"s3://{bucket}/{s3_prefix}/input",
 "s3DataType": "S3_PREFIX"
 }
 }
 }
 ],
 outputDataConfig={
 "s3Path": f"s3://{bucket}/{s3_prefix}/output"
 },
 instanceConfig={
 "instanceType": "ml.m5.large",
 "instanceCount": 1,
 "volumeSizeInGb": 1
 },
 checkpointConfig={
 "s3Uri": f"s3://{bucket}/{s3_prefix}/checkpoints",
 "localPath": "/opt/omega/checkpoints"
 },
 deviceConfig={
 "priorityAccess": {
 "devices": [
 "arn:aws:braket:us-west-1::device/qpu/rigetti/Aspen-M-3"
 ]
 }
 },
 hyperParameters={
 "hyperparameter key you wish to pass": "<hyperparameter value you wish to pass>",
 },
 stoppingCondition={
 "maxRuntimeInSeconds": 1200,
 "maximumTaskLimit": 10
 },
167
Amazon Braket Developer Guide
Interact with hybrid jobs directly using the API
)
Once you create your hybrid job, you can access the hybrid job details through the GetJob API or the
console. To get the hybrid job details from the Python session in which you ran the createJob code as
in the previous example, use the following Python command.
getJob = client.get_job(jobArn=job["jobArn"])
To cancel a hybrid job, call the CancelJob API with the Amazon Resource Name of the job ('JobArn').
cancelJob = client.cancel_job(jobArn=job["jobArn"])
You can specify checkpoints as part of the createJob API using the checkpointConfig parameter.
 checkpointConfig = {
 "localPath" : "/opt/omega/checkpoints",
 "s3Uri": f"s3://{bucket}/{s3_prefix}/checkpoints"
 },
Note
The localPath of checkpointConfig cannot start with any of the following reserved paths: /
opt/ml, /opt/braket, /tmp, or /usr/local/nvidia.
168
Amazon Braket Developer Guide
Amazon Braket with PennyLane
Use PennyLane with Amazon Braket
Hybrid algorithms are algorithms that contain both classical and quantum instructions. The classical
instructions are executed on classical hardware (an EC2 instance or your laptop), and the quantum
instructions are executed either on a simulator or on a quantum computer. We recommend that you run
hybrid algorithms using the Hybrid Jobs feature. For more information, see When to use Amazon Braket
Jobs (p. 130).
Amazon Braket enables you to set up and run hybrid quantum algorithms with the assistance of the
Amazon Braket PennyLane plugin, or with the Amazon Braket Python SDK and example notebook
repositories. Amazon Braket example notebooks, based on the SDK, enable you to set up and run certain
hybrid algorithms without the PennyLane plugin. However, we recommend PennyLane because it
provides a richer experience.
About hybrid quantum algorithms
Hybrid quantum algorithms are important to the industry today because contemporary quantum
computing devices generally produce noise, and therefore, errors. Every quantum gate added to
a computation increases the chance of adding noise; therefore, long-running algorithms can be
overwhelmed by noise, which results in faulty computation.
Pure quantum algorithms such as Shor’s (Quantum Phase Estimation example) or Grover’s (Grover’s
example) require thousands, or millions, of operations. For this reason, they can be impractical for
existing quantum devices, which are generally referred to as noisy intermediate-scale quantum (NISQ)
devices.
In hybrid quantum algorithms, quantum processing units (QPUs) work as co-processors for classic CPUs,
specifically to speed up certain calculations in a classical algorithm. Circuit executions become much
shorter, within reach of the capabilities of today’s devices.
Amazon Braket with PennyLane
Amazon Braket provides support for PennyLane, an open-source software framework built around the
concept of quantum differentiable programming. You can use this framework to train quantum circuits
in the same way that you would train a neural network to find solutions for computational problems in
quantum chemistry, quantum machine learning, and optimization.
The PennyLane library provides interfaces to familiar machine learning tools, including PyTorch and
TensorFlow, to make training quantum circuits quick and intuitive.
• The PennyLane Library -– PennyLane is pre-installed in Amazon Braket notebooks. For access to
Amazon Braket devices from PennyLane, open a notebook and import the PennyLane library with the
following command.
import pennylane as qml
Tutorial notebooks help you get started quickly. Alternatively, you can use PennyLane on Amazon Braket
from an IDE of your choice.
• The Amazon Braket PennyLane plugin — To use your own IDE, you can install the Amazon Braket
PennyLane plugin manually. The plugin connects PennyLane with the Amazon Braket Python SDK, so
you can run circuits in PennyLane on Amazon Braket devices. To install the the PennyLane plugin, use
the following command.
169
Amazon Braket Developer Guide
Hybrid algorithms in Amazon Braket example notebooks
pip install amazon-braket-pennylane-plugin
The following example demonstrates how to set up access to Amazon Braket devices in PennyLane:
# to use SV1
import pennylane as qml
s3 = ("my-bucket", "my-prefix")
sv1 = qml.device("braket.aws.qubit", device_arn="arn:aws:braket:::device/quantum-simulator/
amazon/sv1", s3_destination_folder=s3, wires=2)
# to run a circuit:
@qml.qnode(sv1)
def circuit(x):
qml.RZ(x, wires=0)
qml.CNOT(wires=[0,1])
qml.RY(x, wires=1)
return qml.expval(qml.PauliZ(1))
result = circuit(0.543)
#To use the local sim:
local = qml.device("braket.local.qubit", wires=2)
For tutorial examples and more information about PennyLane, see the Amazon Braket examples
repository.
The Amazon Braket PennyLane plugin enables you to switch between Amazon Braket QPU and
embedded simulator devices in PennyLane with a single line of code. It offers two Amazon Braket
quantum devices to work with PennyLane:
• braket.aws.qubit for running with the Amazon Braket service’s quantum devices, including QPUs
and simulators
• braket.local.qubit for running with the Amazon Braket SDK’s local simulator
The Amazon Braket PennyLane plugin is open source. You can install it from the PennyLane Plugin
GitHub repository.
For more information about PennyLane, see the documentation on the PennyLane website.
Hybrid algorithms in Amazon Braket example
notebooks
Amazon Braket does provide a variety of example notebooks that do not rely on the PennyLane
plugin for running hybrid algorithms. You can get started with any of these Amazon Braket hybrid
example notebooks that illustrate variational methods, such as the Quantum Approximate Optimization
Algorithm (QAOA) or Variational Quantum Eigensolver (VQE).
The Amazon Braket example notebooks rely on the Amazon Braket Python SDK. The SDK provides a
framework to interact with quantum computing hardware devices through Amazon Braket. It is an open
source library that is designed to assist you with the quantum portion of your hybrid workflow.
You can explore Amazon Braket further with our example notebooks.
170
Amazon Braket Developer Guide
Hybrid algorithms with embedded PennyLane simulators
Hybrid algorithms with embedded PennyLane
simulators
Amazon Braket Hybrid Jobs now comes with high performance CPU- and GPU-based embedded
simulators from PennyLane. This family of embedded simulators can be embedded directly within
your hybrid jobs container and includes the fast state-vector lightning.qubit simulator, the
lightning.gpu simulator accelerated using NVIDIA’s cuQuantum library, and others. These embedded
simulators are ideally suited for variational algorithms such as quantum machine learning that can
benefit from advanced methods such as the adjoint differentiation method. You can run these embedded
simulators on one or multiple CPU or GPU instances.
With Hybrid Jobs, you can now run your variational algorithm code using a combination of a classical
co-processor and a QPU, an Amazon Braket on-demand simulator such as SV1, or directly using the
embedded simulator from PennyLane.
The embedded simulator is already available with the Hybrid Jobs container, you simply need to specify
the device (e.g device="local:pennylane/lightning.gpu") in the Braket SDK as shown below.
To use the embedded lightning.gpu simulator, you also need to specify a GPU instance in the
InstanceConfig as shown in the code snippet below:
job = AwsQuantumJob.create(
 device="local:pennylane/lightning.gpu",
 source_module="algorithm_script.py",
 instance_config=InstanceConfig(instanceType="ml.p3.8xlarge")
 )
You must also refer to the device in your algorithm code using the environment variable
AMZN_BRAKET_DEVICE_ARN as follows.
import os
import pennylane as qml
device_string = os.environ["AMZN_BRAKET_DEVICE_ARN"]
prefix, simulator_name = device_string.split("/")
device = qml.device(simulator_name, wires=n_wires)
Refer to the example notebook to get started with using a PennyLane embedded simulator with Hybrid
Jobs.
Adjoint gradient on PennyLane with Amazon
Braket simulators
With the PennyLane plugin for Amazon Braket, you can compute gradients using the adjoint
differentiation method when running on the local state vector simulator or SV1.
Note: To use the adjoint differentiation method, you must specify diff_method='device' in your
qnode, and not diff_method='adjoint'. See the following example.
device_arn = "arn:aws:braket:::device/quantum-simulator/amazon/sv1"
dev = qml.device (https://docs.pennylane.ai/en/stable/code/api/
pennylane.device.html#pennylane.device)("braket.aws.qubit", wires=wires, shots=0,
 device_arn=device_arn
171
Amazon Braket Developer Guide
Adjoint gradient on PennyLane
with Amazon Braket simulators
 )
@qml.qnode(dev, diff_method='device')
def cost_function(params):
 circuit(params)
 return qml.expval(cost_h)
gradient = qml.grad(circuit)
initial_gradient = gradient(params0)
Note
Currently, PennyLane will compute grouping indices for QAOA Hamiltonians and use
them to split the Hamiltonian into multiple expectation values. If you want to use
SV1’s adjoint differentiation capability when running QAOA from PennyLane, you
will need reconstruct the cost Hamiltonian by removing the grouping indices, like so:
cost_h, mixer_h = qml.qaoa.max_clique(g, constrained=False) cost_h =
qml.Hamiltonian(cost_h.coeffs, cost_h.ops)
172
Amazon Braket Developer Guide
Error mitigation on IonQ Aria
Error mitigation
Quantum error mitigation is a set of techniques aimed at reducing the effects of errors in quantum
computers.
Quantum devices are subject to environmental noise that degrades the quality of computations
performed. While fault-tolerant quantum computing promises a solution to this problem, current
quantum devices are limited by the number of qubits and relatively high error rates. To combat this
in the near-term, researchers are investigating methods to improve the accuracy of noisy quantum
computation. This approach, known as quantum error mitigation, involves using various techniques to
extract the best signal from noisy measurement data.
Error mitigation on IonQ Aria
Error mitigation involves running multiple physical circuits and combining their measurements to give an
improved result. The IonQ Aria device features an error mitigation method called debiasing.
Debiasing maps a circuit into multiple variants that act on different qubit permutations or with different
gate decompositions. This reduces the effect of systematic errors such as gate over-rotations or a single
faulty qubit by using different implementations of a circuit that could otherwise bias measurement
results. This comes at the expense of extra overhead to calibrate multiple qubits and gates.
For more information on debiasing, see Enhancing quantum computer performance via symmetrization.
Note
Using debiasing requires a minimum of 2500 shots.
You can run a quantum task with debiasing on an IoQ Aria device using the following code:
from braket.aws import AwsDevice
from braket.circuits import Circuit
from braket.mitigation import Debias
device = AwsDevice("arn:aws:braket:us-east-1::device/qpu/ionq/Aria-1")
circuit = Circuit().h(0).cnot(0, 1)
task = device.run(circuit, shots=2500, device_parameters={"errorMitigation": Debias()})
result = task.result()
print(result.measurement_counts)
>>> {"00": 1245, "01": 5, "10": 10 "11": 1240} # result from debiasing
When the quantum task is complete you can see the measurement probabilities and any result types
from the quantum task. The measurement probabilities and counts from all variants are aggregated into
a single distribution. Any result types specified in the circuit, such as expectation values, are computed
using the aggregate measurement counts.
Sharpening
You can also access measurement probabilities computed with a different post-processing strategy called
sharpening. Sharpening compares the results of each variant and discards inconsistent shots, favoring
the most likely measurement outcome across variants. For more information, see Enhancing quantum
computer performance via symmetrization.
173
Amazon Braket Developer Guide
Sharpening
Importantly, sharpening assumes the form of the output distribution to be sparse with few highprobability states and many zero-probability states. It may distort the probability distribution if this
assumption is not valid.
You can access the probabilities from a sharpened distribution in the additional_metadata field
on the GateModelTaskResult in the Braket Python SDK. Note that sharpening does not return the
measurement counts, but instead returns a re-normalized probability distribution. The following code
snippet shows how to access the distribution after sharpening.
print(result.additional_metadata.ionqMetadata.sharpenedProbabilities)
>>> {"00": 0.51, "11": 0.549} # sharpened probabilities
174
Amazon Braket Developer Guide
Shared responsibility for security
Security in Amazon Braket
This chapter helps you understand how to apply the shared responsibility model when using Amazon
Braket. It shows you how to configure Amazon Braket to meet your security and compliance objectives.
You also learn how to use other AWS services that help you to monitor and secure your Amazon Braket
resources.
Cloud security at AWS is the highest priority. As an AWS customer, you benefit from a data center
and network architecture that is built to meet the requirements of the most security-sensitive
organizations. You are responsible for other factors, including the sensitivity of your data, your
company’s requirements, and applicable laws and regulations.
Shared responsibility for security
Security is a shared responsibility between AWS and you. The shared responsibility model describes this
as security of the cloud and security in the cloud:
• Security of the cloud – AWS is responsible for protecting the infrastructure that runs AWS services in
the AWS Cloud. AWS also provides you with services that you can use securely. Third-party auditors
regularly test and verify the effectiveness of our security as part of the AWS Compliance Programs.
To learn about the compliance programs that apply to Amazon Braket, see AWS Services in Scope by
Compliance Program.
• Security in the cloud – You are responsible for maintaining control over your content that is hosted
on this AWS infrastructure. This content includes the security configuration and management tasks for
the AWS services that you use.
Data protection
The AWS shared responsibility model applies to data protection in Amazon Braket. As described in this
model, AWS is responsible for protecting the global infrastructure that runs all of the AWS Cloud. You
are responsible for maintaining control over your content that is hosted on this infrastructure. This
content includes the security configuration and management tasks for the AWS services that you use. For
more information about data privacy, see the Data Privacy FAQ. For information about data protection in
Europe, see the AWS Shared Responsibility Model and GDPR blog post on the AWS Security Blog.
For data protection purposes, we recommend that you protect AWS account credentials and set up
individual users with AWS IAM Identity Center or AWS Identity and Access Management (IAM). That way,
each user is given only the permissions necessary to fulfill their job duties. We also recommend that you
secure your data in the following ways:
• Use multi-factor authentication (MFA) with each account.
• Use SSL/TLS to communicate with AWS resources. We require TLS 1.2 and recommend TLS 1.3.
• Set up API and user activity logging with AWS CloudTrail.
• Use AWS encryption solutions, along with all default security controls within AWS services.
• Use advanced managed security services such as Amazon Macie, which assists in discovering and
securing sensitive data that is stored in Amazon S3.
175
Amazon Braket Developer Guide
Data retention
• If you require FIPS 140-2 validated cryptographic modules when accessing AWS through a command
line interface or an API, use a FIPS endpoint. For more information about the available FIPS endpoints,
see Federal Information Processing Standard (FIPS) 140-2.
We strongly recommend that you never put confidential or sensitive information, such as your
customers' email addresses, into tags or free-form text fields such as a Name field. This includes when
you work with Amazon Braket or other AWS services using the console, API, AWS CLI, or AWS SDKs.
Any data that you enter into tags or free-form text fields used for names may be used for billing or
diagnostic logs. If you provide a URL to an external server, we strongly recommend that you do not
include credentials information in the URL to validate your request to that server.
Data retention
After 90 days, Amazon Braket automatically removes all quantum task IDs and other metadata
associated with your quantum tasks. As a result of this data retention policy, these tasks and results are
no longer retrievable by search from the Amazon Braket console, although they remain stored in your S3
bucket.
If you need access to historical quantum tasks and results that are stored in your S3 bucket for longer
than 90 days, you must keep a separate record of your task ID and other metadata associated with that
data. Be sure to save the information prior to 90 days. You can use that saved information to retrieve the
historical data.
Managing access to Amazon Braket
This chapter describes the permissions that are required to run Amazon Braket, or to restrict the access
of specific users and roles. You can grant (or deny) the required permissions to any user or role in your
account. To do so, attach the appropriate Amazon Braket policy to that user or role in your account as
described in the following sections.
As a prerequisite, you must enable Amazon Braket. To enable Braket, be sure to sign in as a user or role
that has (1) administrator permissions or (2) is assigned the AmazonBraketFullAccess policy and has
permissions to create Amazon Simple Storage Service (Amazon S3) buckets.
In this section:
• Amazon Braket resources (p. 176)
• Notebooks and roles (p. 177)
• About the AmazonBraketFullAccess policy (p. 177)
• About the AmazonBraketJobsExecutionPolicy policy (p. 181)
• Restrict user access to certain devices (p. 183)
• Amazon Braket updates to AWS managed policies (p. 184)
• Restrict user access to certain notebook instances (p. 184)
• Restrict user access to certain S3 buckets (p. 185)
Amazon Braket resources
Braket creates one type of resource: the quantum-task resource. The Amazon Resource Name (ARN) for
this resource type is as follows:
• Resource Name: AWS::Service::Braket
176
Amazon Braket Developer Guide
Notebooks and roles
• ARN Regex: arn:${Partition}:braket:${Region}:${Account}:quantum-task/${RandomId}
Notebooks and roles
You can use the noteboook resource type in Braket. A notebook is an Amazon SageMaker resource that
Braket is able to share. To use a notebook with Braket, you must specify an IAM role with a name that
begins with AmazonBraketServiceSageMakerNotebook.
To create a notebook, you must use a role with admin permissions or that has the following inline policy
attached to it.
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Effect": "Allow",
 "Action": "iam:CreateRole",
 "Resource": "arn:aws:iam::*:role/service-role/
AmazonBraketServiceSageMakerNotebookRole-*"
 },
 {
 "Effect": "Allow",
 "Action": "iam:CreatePolicy",
 "Resource": "arn:aws:iam::*:policy/service-role/
AmazonBraketServiceSageMakerNotebookAccess-*"
 },
 {
 "Effect": "Allow",
 "Action": "iam:AttachRolePolicy",
 "Resource": "arn:aws:iam::*:role/service-role/
AmazonBraketServiceSageMakerNotebookRole-*",
 "Condition": {
 "StringLike": {
 "iam:PolicyARN": [
 "arn:aws:iam::aws:policy/AmazonBraketFullAccess",
 "arn:aws:iam::*:policy/service-role/
AmazonBraketServiceSageMakerNotebookAccess-*"
 ]
 }
 }
 }
 ]
}
To create the role, follow the steps given in the Create a notebook page or have your administrator
create it for you. Ensure that the AmazonBraketFullAccess policy is attached.
After you’ve created the role, you can reuse that role for all notebooks you launch in the future.
About the AmazonBraketFullAccess policy
The AmazonBraketFullAccess policy grants permissions for Amazon Braket operations, including
permissions for these tasks:
• Download containers from Amazon Elastic Container Registry – To read and download container
images that are used for the Amazon Braket Hybrid Jobs feature. The containers must conform to the
format "arn:aws:ecr:::repository/amazon-braket".
• Keep AWS CloudTrail logs – For all describe, get, and list actions in addition to starting and stopping
queries, testing metrics filters, and filtering log events. The AWS CloudTrail log file contains a record of
all Amazon Braket API activity that occurs in your account.
177
Amazon Braket Developer Guide
About the AmazonBraketFullAccess policy
• Utilize roles to control resources – To create a service-linked role in your account. The service-linked
role has access to AWS resources on your behalf. It can be used only by the Amazon Braket service.
Also, to pass in IAM roles to the Amazon Braket CreateJob API and to create a role and attach a
policy scoped to AmazonBraketFullAccess to the role.
• Create log groups, log events, and query log groups in order to maintain usage log files for your
account – To create, store, and view logging information about Amazon Braket usage in your account.
Query metrics on hybrid jobs log groups. Encompass the proper Braket path and allow putting log
data. Put metric data in CloudWatch.
• Create and store data in Amazon S3 buckets, and list all buckets – To create S3 buckets, list the S3
buckets in your account, and put objects into and get objects from any bucket in your account whose
name begins with amazon-braket-. These permissions are required for Braket to put files containing
results from processed quantum tasks into the bucket and to retrieve them from the bucket.
• Pass IAM roles – To pass in IAM roles to the CreateJob API.
• Amazon SageMaker Notebook – To create and manage SageMaker notebook instances scoped to the
resource from "arn:aws:sagemaker:::notebook-instance/amazon-braket-".
• Validate service quotas – To create SageMaker notebooks and Amazon Braket Hybrid jobs, your
resource counts cannot exceed quotas for your account (p. 23).
Policy contents
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Effect": "Allow",
 "Action": [
 "s3:GetObject",
 "s3:PutObject",
 "s3:ListBucket",
 "s3:CreateBucket",
 "s3:PutBucketPublicAccessBlock",
 "s3:PutBucketPolicy"
 ],
 "Resource": "arn:aws:s3:::amazon-braket-*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "s3:ListAllMyBuckets",
 "servicequotas:GetServiceQuota",
 "cloudwatch:GetMetricData"
 ],
 "Resource": "*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "ecr:GetDownloadUrlForLayer",
 "ecr:BatchGetImage",
 "ecr:BatchCheckLayerAvailability"
 ],
 "Resource": "arn:aws:ecr:*:*:repository/amazon-braket*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "ecr:GetAuthorizationToken"
 ],
 "Resource": "*"
178
Amazon Braket Developer Guide
About the AmazonBraketFullAccess policy
 },
 {
 "Effect": "Allow",
 "Action": [
 "logs:Describe*",
 "logs:Get*",
 "logs:List*",
 "logs:StartQuery",
 "logs:StopQuery",
 "logs:TestMetricFilter",
 "logs:FilterLogEvents"
 ],
 "Resource": "arn:aws:logs:*:*:log-group:/aws/braket*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "iam:ListRoles",
 "iam:ListRolePolicies",
 "iam:GetRole",
 "iam:GetRolePolicy",
 "iam:ListAttachedRolePolicies"
 ],
 "Resource": "*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "sagemaker:ListNotebookInstances"
 ],
 "Resource": "*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "sagemaker:CreatePresignedNotebookInstanceUrl",
 "sagemaker:CreateNotebookInstance",
 "sagemaker:DeleteNotebookInstance",
 "sagemaker:DescribeNotebookInstance",
 "sagemaker:StartNotebookInstance",
 "sagemaker:StopNotebookInstance",
 "sagemaker:UpdateNotebookInstance",
 "sagemaker:ListTags",
 "sagemaker:AddTags",
 "sagemaker:DeleteTags"
 ],
 "Resource": "arn:aws:sagemaker:*:*:notebook-instance/amazon-braket-*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "sagemaker:DescribeNotebookInstanceLifecycleConfig",
 "sagemaker:CreateNotebookInstanceLifecycleConfig",
 "sagemaker:DeleteNotebookInstanceLifecycleConfig",
 "sagemaker:ListNotebookInstanceLifecycleConfigs",
 "sagemaker:UpdateNotebookInstanceLifecycleConfig"
 ],
 "Resource": "arn:aws:sagemaker:*:*:notebook-instance-lifecycle-config/amazonbraket-*"
 },
 {
 "Effect": "Allow",
 "Action": "braket:*",
 "Resource": "*"
 },
 {
179
Amazon Braket Developer Guide
About the AmazonBraketFullAccess policy
 "Effect": "Allow",
 "Action": "iam:CreateServiceLinkedRole",
 "Resource": "arn:aws:iam::*:role/aws-service-role/braket.amazonaws.com/
AWSServiceRoleForAmazonBraket*",
 "Condition": {
 "StringEquals": {
 "iam:AWSServiceName": "braket.amazonaws.com"
 }
 }
 },
 {
 "Effect": "Allow",
 "Action": [
 "iam:PassRole"
 ],
 "Resource": "arn:aws:iam::*:role/service-role/
AmazonBraketServiceSageMakerNotebookRole*",
 "Condition": {
 "StringLike": {
 "iam:PassedToService": [
 "sagemaker.amazonaws.com"
 ]
 }
 }
 },
 {
 "Effect": "Allow",
 "Action": [
 "iam:PassRole"
 ],
 "Resource": "arn:aws:iam::*:role/service-role/AmazonBraketJobsExecutionRole*",
 "Condition": {
 "StringLike": {
 "iam:PassedToService": [
 "braket.amazonaws.com"
 ]
 }
 }
 },
 {
 "Effect": "Allow",
 "Action": [
 "logs:GetQueryResults"
 ],
 "Resource": [
 "arn:aws:logs:*:*:log-group:*"
 ]
 },
 {
 "Effect": "Allow",
 "Action": [
 "logs:PutLogEvents",
 "logs:CreateLogStream",
 "logs:CreateLogGroup"
 ],
 "Resource": "arn:aws:logs:*:*:log-group:/aws/braket*"
 },
 {
 "Effect": "Allow",
 "Action": "cloudwatch:PutMetricData",
 "Resource": "*",
 "Condition": {
 "StringEquals": {
 "cloudwatch:namespace": "/aws/braket"
 }
 }
180
Amazon Braket Developer Guide
About the AmazonBraketJobsExecutionPolicy policy
 }
 ]
}
About the AmazonBraketJobsExecutionPolicy policy
The AmazonBraketJobsExecutionPolicy policy grants permissions for execution roles used in Amazon
Braket Hybrid Jobs as follows:
• Download containers from Amazon Elastic Container Registry - Permissions to read and download
container images that are used for the Amazon Braket Hybrid Jobs feature. Containers must conform
to the format "arn:aws:ecr:*:*:repository/amazon-braket*".
• Create log groups and log events and query log groups in order to maintain usage log files for your
account – Create, store, and view logging information about Amazon Braket usage in your account.
Query metrics on hybrid jobs log groups. Encompass the proper Braket path and allow putting log
data. Put metric data in CloudWatch.
• Store data in Amazon S3 buckets – List the S3 buckets in your account, put objects into and
get objects from any bucket in your account that starts with amazon-braket- in its name. These
permissions are required for Braket to put files containing results from processed quantum tasks into
the bucket, and to retrieve them from the bucket.
• Pass IAM roles – Passing in IAM roles to the CreateJob API. Roles must conform to the format
arn:aws:iam::*:role/service-role/AmazonBraketJobsExecutionRole*.
 "Version": "2012-10-17",
 "Statement": [
 {
 "Effect": "Allow",
 "Action": [
 "s3:GetObject",
 "s3:PutObject",
 "s3:ListBucket",
 "s3:CreateBucket",
 "s3:PutBucketPublicAccessBlock",
 "s3:PutBucketPolicy"
 ],
 "Resource": "arn:aws:s3:::amazon-braket-*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "ecr:GetDownloadUrlForLayer",
 "ecr:BatchGetImage",
 "ecr:BatchCheckLayerAvailability"
 ],
 "Resource": "arn:aws:ecr:*:*:repository/amazon-braket*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "ecr:GetAuthorizationToken"
 ],
 "Resource": "*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "braket:CancelJob",
 "braket:CancelQuantumTask",
 "braket:CreateJob",
181
Amazon Braket Developer Guide
About the AmazonBraketJobsExecutionPolicy policy
 "braket:CreateQuantumTask",
 "braket:GetDevice",
 "braket:GetJob",
 "braket:GetQuantumTask",
 "braket:SearchDevices",
 "braket:SearchJobs",
 "braket:SearchQuantumTasks",
 "braket:ListTagsForResource",
 "braket:TagResource",
 "braket:UntagResource"
 ],
 "Resource": "*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "iam:PassRole"
 ],
 "Resource": "arn:aws:iam::*:role/service-role/AmazonBraketJobsExecutionRole*",
 "Condition": {
 "StringLike": {
 "iam:PassedToService": [
 "braket.amazonaws.com"
 ]
 }
 }
 },
 {
 "Effect": "Allow",
 "Action": [
 "iam:ListRoles"
 ],
 "Resource": "arn:aws:iam::*:role/*"
 },
 {
 "Effect": "Allow",
 "Action": [
 "logs:GetQueryResults"
 ],
 "Resource": [
 "arn:aws:logs:*:*:log-group:*"
 ]
 },
 {
 "Effect": "Allow",
 "Action": [
 "logs:PutLogEvents",
 "logs:CreateLogStream",
 "logs:CreateLogGroup",
 "logs:GetLogEvents",
 "logs:DescribeLogStreams",
 "logs:StartQuery",
 "logs:StopQuery"
 ],
 "Resource": "arn:aws:logs:*:*:log-group:/aws/braket*"
 },
 {
 "Effect": "Allow",
 "Action": "cloudwatch:PutMetricData",
 "Resource": "*",
 "Condition": {
 "StringEquals": {
 "cloudwatch:namespace": "/aws/braket"
 }
 }
 }
182
Amazon Braket Developer Guide
Restrict user access to certain devices
 ]
}
Restrict user access to certain devices
To restrict access for certain users to certain Braket devices, you can add a deny permissions policy to a
specific IAM role.
The following actions can be restricted with such permissions:
• CreateQuantumTask - to deny quantum task creation on specified devices.
• CreateJob - to deny hybrid job creation on specified devices.
• GetDevice - to deny getting details of specified devices.
The following example restricts access to all QPUs for the AWS account 123456789012.
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Effect": "Deny",
 "Action": [
 "braket:CreateQuantumTask",
 "braket:CreateJob",
 "braket:GetDevice"
 ],
 "Resource": [
 "arn:aws:braket:*:*:device/qpu/*"
 ]
 }
 ]
}
To adapt this code, substitute the Amazon Resource Number (ARN) of the restricted device for the string
shown in the previous example. This string provides the Resource value. In Braket, a device represents a
QPU or simulator that you can call to run quantum tasks. The devices available are listed on the Devices
page. There are two schemas used to specify access to these devices:
• arn:aws:braket:<region>:<account id>:device/qpu/<provider>/<device_id>
• arn:aws:braket:<region>:<account id>:device/quantum-simulator/<provider>/
<device_id>
Here are examples for various types of device access
• To select all QPUs across all regions: arn:aws:braket:*:*:device/qpu/*
• To select all QPUs in the us-west-2 region ONLY: arn:aws:braket:uswest-2:123456789012:device/qpu/*
• Equivalently, to select all QPUs in the us-west-2 region ONLY ( since devices are a service resource, not
a customer resource): arn:aws:braket:us-west-2:* :device/qpu/*
• To restrict access to all on-demand simulator devices:
arn:aws:braket:* :123456789012:device/quantum-simulator/*
• To restrict access to the IonQ Harmony device in the us-east-1 region: arn:aws:braket:useast-1:123456789012:device/ionq/Harmony
• To restrict access to devices from a certain provider (for example, to Rigetti QPU devices):
arn:aws:braket:* :123456789012:device/qpu/rigetti/*
183
Amazon Braket Developer Guide
Amazon Braket updates to AWS managed policies
• To restrict access to the TN1 device: arn:aws:braket:* :123456789012:device/quantumsimulator/amazon/tn1
Amazon Braket updates to AWS managed policies
The following table provides details about updates to AWS managed policies for Braket since this service
began tracking these changes.
Change Description Date
AmazonBraketFullAccess (p. 177) - Full
access policy for Braket
Added the
servicequotas:GetServiceQuota
and cloudwatch:GetMetricData
actions to be included in the
AmazonBraketFullAccess policy.
.
March 24, 2023
AmazonBraketFullAccess (p. 177) - Full
access policy for Braket
Braket adjusted
iam:PassRole permissions for
AmazonBraketFullAccess to include
the service-role/ path.
November 29, 2021
AmazonBraketJobsExecutionPolicy (p. 181)
- Hybrid jobs execution policy for Amazon
Braket Hybrid Jobs
Braket updated the hybrid jobs
execution role ARN to include the
service-role/ path.
November 29, 2021
Braket started tracking changes Braket started tracking changes for
its AWS managed policies.
November 29, 2021
Restrict user access to certain notebook instances
To restrict access for certain users to specific Braket notebook instances, you can add a deny permissions
policy to a specific role, user, or group.
The following example uses policy variables to efficiently restrict permissions to start, stop, and access
specific notebook instances in the AWS account 123456789012, which is named according to the user
who should have access (for example, user Alice would have access to a notebook instance named
amazon-braket-Alice).
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Effect": "Deny",
 "Action": [
 "sagemaker:CreateNotebookInstance",
 "sagemaker:DeleteNotebookInstance",
 "sagemaker:UpdateNotebookInstance",
 "sagemaker:CreateNotebookInstanceLifecycleConfig",
 "sagemaker:DeleteNotebookInstanceLifecycleConfig",
 "sagemaker:UpdateNotebookInstanceLifecycleConfig"
 ],
 "Resource": "*"
 },
 {
 "Effect": "Deny",
184
Amazon Braket Developer Guide
Restrict user access to certain S3 buckets
 "Action": [
 "sagemaker:DescribeNotebookInstance",
 "sagemaker:StartNotebookInstance",
 "sagemaker:StopNotebookInstance",
 ],
 "NotResource": [
 "arn:aws:sagemaker:*:123456789012:notebook-instance/amazon-braket-${aws:username}"
 ]
 },
 {
 "Effect": "Deny",
 "Action": [
 "sagemaker:CreatePresignedNotebookInstanceUrl"
 ],
 "NotResource": [
 "arn:aws:sagemaker:*:123456789012:notebook-instance/amazon-braket-${aws:username}*"
 ]
 }
 ]
}
Restrict user access to certain S3 buckets
To restrict access for certain users to specific Amazon S3 buckets, you can add a deny policy to a specific
role, user, or group.
The following example restricts permissions to retrieve and place objects into a specific S3 bucket
(arn:aws:s3:::amazon-braket-us-east-1-123456789012-Alice) and also restricts the listing of
those objects.
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Effect": "Deny",
 "Action": [
 "s3:ListBucket"
 ],
 "NotResource": [
 "arn:aws:s3:::amazon-braket-us-east-1-123456789012-Alice"
 ]
 },
 {
 "Effect": "Deny",
 "Action": [
 "s3:GetObject"
 ],
 "NotResource": [
 "arn:aws:s3:::amazon-braket-us-east-1-123456789012-Alice/*"
 ]
 }
 ]
}
To restrict access to the bucket for a certain notebook instance, you can add the preceding policy to the
notebook execution role.
Amazon Braket service-linked role
When you enable Amazon Braket, a service-linked role is created in your account.
185
Amazon Braket Developer Guide
Service-linked role permissions for Amazon Braket
A service-linked role is a unique type of IAM role that, in this case, is linked directly to Amazon Braket.
The Amazon Braket service-linked role is predefined to include all the permissions that Braket requires
when calling other AWS services on your behalf.
A service-linked role makes setting up Amazon Braket easier because you don’t have to add the
necessary permissions manually. Amazon Braket defines the permissions of its service-linked roles.
Unless you change these definitions, only Amazon Braket can assume its roles. The defined permissions
include the trust policy and the permissions policy. The permissions policy cannot be attached to any
other IAM entity.
The service-linked role that Amazon Braket sets up is part of the AWS Identity and Access Management
(IAM) service-linked roles capability. For information about other AWS services that support servicelinked roles, see AWS Services That Work with IAM and look for the services that have Yes in the ServiceLinked Role column. Choose a Yes with a link to view the service-linked role documentation for that
service.
Service-linked role permissions for Amazon Braket
Amazon Braket uses the AWSServiceRoleForAmazonBraket service-linked role that trusts the
braket.amazonaws.com entity to assume the role.
You must configure permissions to allow an IAM entity (such as a group or role) to create, edit, or delete
a service-linked role. For more information, see Service-Linked Role Permissions.
The service-linked role in Amazon Braket is granted the following permissions by default:
• Amazon S3 – permissions to list the buckets in your account, and put objects into and get objects from
any bucket in your account with a name that starts with amazon-braket-.
• Amazon CloudWatch Logs – permissions to list and create log groups, create the associated log
streams, and put events into the log group created for Amazon Braket.
The following policy is attached to the AWSServiceRoleForAmazonBraket service-linked role:
{"Version": "2012-10-17",
 "Statement": [
 {"Effect": "Allow",
 "Action": [
 "s3:GetObject",
 "s3:PutObject",
 "s3:ListBucket"
 ],
 "Resource": "arn:aws:s3:::amazon-braket*"
 },
 {"Effect": "Allow",
 "Action": [
 "logs:Describe*",
 "logs:Get*",
 "logs:List*",
 "logs:StartQuery",
 "logs:StopQuery",
 "logs:TestMetricFilter",
 "logs:FilterLogEvents"
 ],
 "Resource": "arn:aws:logs:*:*:log-group:/aws/braket/*"
 },
 {"Effect": "Allow",
 "Action": "braket:*",
 "Resource": "*"
 },
 {"Effect": "Allow",
186
Amazon Braket Developer Guide
Resilience
 "Action": "iam:CreateServiceLinkedRole",
 "Resource": "arn:aws:iam::*:role/aws-service-role/braket.amazonaws.com/
AWSServiceRoleForAmazonBraket*",
 "Condition": {"StringEquals": {"iam:AWSServiceName": "braket.amazonaws.com"
 }
 }
 }
 ]
}
Resilience in Amazon Braket
The AWS global infrastructure is built around AWS Regions and Availability Zones.
Each Region provides multiple availability zones that are physically separated and isolated. These
availability zones (AZs) are connected through low-latency, high-throughput, and highly redundant
networking. As a result, availability zones are more highly available, fault tolerant, and scalable than
traditional single- or multiple-datacenter infrastructures.
You can design and operate applications and databases that fail over between AZs automatically,
without interruption.
For more information about AWS Regions and availability zones, see AWS Global Infrastructure.
Compliance validation for Amazon Braket
Third-party auditors regularly assess the security and compliance of Amazon Braket and our integration
with third-party hardware providers. For an up-to-date list of compliance information for Braket, see
AWS services in scope by compliance program. For general information, see AWS compliance.
You can download third-party audit reports using AWS Artifact. For more information, see Downloading
reports in AWS Artifact.
Note
AWS compliance reports don't cover QPUs from third-party hardware providers who can choose
to go through their own independent audits.
Your compliance responsibility when using Amazon Braket is determined by the sensitivity of your data,
your company’s compliance objectives, and applicable laws and regulations. AWS provides the following
resources to help with compliance:
• Security and Compliance Quick Start Guides – These deployment guides discuss architectural
considerations and provide steps for deploying security- and compliance-focused baseline
environments on AWS.
• AWS Compliance Resources – This collection of workbooks and guides might apply to your industry
and location.
Infrastructure Security in Amazon Braket
As a managed service, Amazon Braket is protected by the AWS global network security procedures that
are described in the AWS: Overview of Security Processes whitepaper.
For access to Amazon Braket through the network, you make calls to published AWS APIs. Clients must
support Transport Layer Security (TLS) 1.2 or later. Clients also must support cipher suites with perfect
187
Amazon Braket Developer Guide
Third Party Security
forward secrecy (PFS) such as Ephemeral Diffie-Hellman (DHE) or Elliptic Curve Ephemeral DiffieHellman (ECDHE). Most modern systems such as Java 7 and later support these modes.
Additionally, requests must be signed using an access key ID and a secret access key that is associated
with an IAM principal. Or you can use the AWS Security Token Service (AWS STS) to generate temporary
security credentials to sign requests.
Security of Amazon Braket Hardware Providers
QPUs on Amazon Braket are hosted by third-party hardware providers. When you run your quantum task
on a QPU, Amazon Braket uses the DeviceARN as an identifier when sending the circuit to the specified
QPU for processing.
If you use Amazon Braket for access to quantum computing hardware operated by one of the third-party
hardware providers, your circuit and its associated data are processed by hardware providers outside of
facilities operated by AWS. Information about the physical location and AWS Region where each QPU is
available can be found in the Device Details section of the Amazon Braket console.
Your content is anonymized. Only the content necessary to process the circuit is sent to third parties.
AWS account information is not transmitted to third parties.
All data is encrypted at rest and in transit. Data is decrypted for processing only. Amazon Braket thirdparty providers are not permitted to store or use your content for purposes other than processing your
circuit. Once the circuit completes, the results are returned to Amazon Braket and stored in your S3
bucket.
The security of Amazon Braket third-party quantum hardware providers is audited periodically, to ensure
that standards of network security, access control, data protection, and physical security are met.
188
Amazon Braket Developer Guide
Access denied exception
Troubleshoot
Solve common problems you might find when working with Amazon Braket.
Topics
In this section:
• Access denied exception (p. 189)
• A quantum task is failing creation (p. 189)
• An SDK feature does not work (p. 189)
• A hybrid job fails due to an exceeded quota (p. 190)
• Something stopped working in your notebook instance (p. 190)
• Troubleshoot OpenQASM (p. 191)
Access denied exception
If you receive an AccessDeniedException, as shown in the following image, when enabling or using
Braket, then you are most likely attempting to enable or use Braket in a region where your restricted role
does not have access.
In such cases, you should contact your internal AWS administrator to understand which of the following
conditions apply:
• if there are role restrictions preventing access to a region
• if the role you are attempting to use is permitted to use Braket
If your role does not have access to a given region when using Braket, then you will be unable to use
devices in that particular region.
A quantum task is failing creation
If you receive an error along the lines of "An error occurred (ValidationException) when calling the
CreateQuantumTask operation: Caller doesn’t have access to amazon-braket-…" make sure you are
referring to an existing s3_folder since we do not auto create new Amazon S3 buckets and prefixes for
you.
If you are accessing the API directly and getting an error like "Failed to create quantum task: Caller
doesn’t have access to s3://MY_BUCKET" make sure you are not including s3:// in the Amazon S3 bucket
path.
An SDK feature does not work
Make sure your SDK (and schemas) are up-to-date. From the notebook or your python editor run
189
Amazon Braket Developer Guide
A hybrid job fails due to an exceeded quota
!pip install --upgrade amazon-braket-sdk
Make sure your SDK and schemas are up-to-date. To update the SDK from the notebook or your python
editor run the following:
pip install --upgrade amazon-braket-schemas
If you are accessing Amazon Braket from your own client make sure your AWS region is set to one
supported by Amazon Braket.
A hybrid job fails due to an exceeded quota
My hybrid job fails with ServiceQuotaExceededException
A hybrid job running quantum tasks against the Amazon Braket simulators can fail to be created if you
exceed the concurrent quantum task limit for the simulator device you are targeting. The service limits
are explained in the Quotas (p. 23) topic. If you are running multiple hybrid jobs from your account,
which run concurrent tasks against a simulator device, you could encounter this error.
To see the number of concurrent quantum tasks against a specific simulator device, use the searchquantum-tasks API, as shown in the following code example.
DEVICE_ARN=arn:aws:braket:::device/quantum-simulator/amazon/sv1
task_list=""
for status_value in "CREATED" "QUEUED" "RUNNING" "CANCELLING"; do
 tasks=$(aws braket search-quantum-tasks --filters name=status,operator=EQUAL,values=
${status_value} name=deviceArn,operator=EQUAL,values=$DEVICE_ARN --max-results 100 --query
 'quantumTasks[*].quantumTaskArn' --output text)
 task_list="$task_list $tasks"
done;
echo "$task_list" | tr -s ' \t' '[\n*]' | sort | uniq
You can also view the created quantum tasks against a device using Amazon CloudWatch metrics:
Braket > By Device.
To avoid running into these errors, you can either:
1. Request a service quota increase for the number of concurrent quantum tasks for the simulator
device. This is only applicable to the SV1 device.
2. Handle ServiceQuotaExceeded exceptions in your code and retry.
Something stopped working in your notebook
instance
If some components of your notebook stop working, try the following:
1. Download any notebooks you created or modified to a local drive.
2. Stop your notebook instance.
3. Delete your notebook instance.
4. Create new notebook instance with a different name.
190
Amazon Braket Developer Guide
Troubleshoot OpenQASM
5. Upload the notebooks to the new instance.
Troubleshoot OpenQASM
This section provides troubleshooting pointers that might be useful when encountering errors using
OpenQASM 3.0.
In this section:
• Include statement error (p. 191)
• Non-contiguous qubits error (p. 191)
• Mixing physical qubits with virtual qubits error (p. 192)
• Requesting result types and measuring qubits in the same program error (p. 192)
• Classical and qubit register limits exceeded error (p. 192)
• Box not preceded by a verbatim pragma error (p. 192)
• Verbatim boxes missing native gates error (p. 193)
• Verbatim boxes missing physical qubits error (p. 193)
• The verbatim pragma is missing "braket" error (p. 193)
• Single qubits cannot be indexed error (p. 193)
• The physical qubits in a two qubit gate are not connected error (p. 194)
• GetDevice does not return OpenQASM results error (p. 194)
• Local simulator support warning (p. 195)
Include statement error
Braket currently doesn’t have a standard gate library file to be included in OpenQASM programs. For
example, the following example raises a parser error.
OPENQASM 3;
include "standardlib.inc";
This code generates the error message: No terminal matches '"' in the current parser
context, at line 2 col 17.
Non-contiguous qubits error
Using non-contiguous qubits on devices that requiresContiguousQubitIndices be set to true in
the device capability result in an error.
When running quantum tasks on simulators and IonQ, the following program triggers the error.
OPENQASM 3;
qubit[4] q;
h q[0];
cnot q[0], q[2];
cnot q[0], q[3];
This code generates the error message: Device requires contiguous qubits. Qubit register
q has unused qubits q[1], q[4].
191
Amazon Braket Developer Guide
Mixing physical qubits with virtual qubits error
Mixing physical qubits with virtual qubits error
Mixing physical qubits with virtual qubits in the same program is not allowed and results in an error. The
following code generates the error.
OPENQASM 3;
qubit[2] q;
cnot q[0], $1;
This code generates the error message: [line 4] mixes physical qubits and qubits
registers.
Requesting result types and measuring qubits in the
same program error
Requesting result types and that qubits are explicitly measured in the same program results in an error.
The following code generates the error.
OPENQASM 3;
qubit[2] q;
h q[0];
cnot q[0], q[1];
measure q;
#pragma braket result expectation x(q[0]) @ z(q[1])
This code generates the error message: Qubits should not be explicitly measured when
result types are requested.
Classical and qubit register limits exceeded error
Only one classical register and one qubit register are allowed. The following code generates the error.
OPENQASM 3;
qubit[2] q0;
qubit[2] q1;
This code generates the error message: [line 4] cannot declare a qubit register. Only 1
qubit register is supported.
Box not preceded by a verbatim pragma error
All boxes must be preceded by a verbatim pragma. The following code generates the error.
box{
rx(0.5) $0;
}
This code generates the error message: In verbatim boxes, native gates are required. x
is not a device native gate.
192
Amazon Braket Developer Guide
Verbatim boxes missing native gates error
Verbatim boxes missing native gates error
Verbatim boxes should have native gates and physical qubits. The following code generates the native
gates error.
#pragma braket verbatim
box{
x $0;
}
This code generates the error message: In verbatim boxes, native gates are required. x
is not a device native gate.
Verbatim boxes missing physical qubits error
Verbatim boxes must have physical qubits. The following code generates the missing physical qubits
error.
qubit[2] q;
#pragma braket verbatim
box{
rx(0.1) q[0];
}
This code generates the error message: Physical qubits are required in verbatim box.
The verbatim pragma is missing "braket" error
You must include “braket” in the verbatim pragma. The following code generates the error.
#pragma braket verbatim // Correct
#pragma verbatim // wrong
This code generates the error message: You must include “braket” in the verbatim pragma
Single qubits cannot be indexed error
Single qubits cannot be indexed. The following code generates the error.
OPENQASM 3;
qubit q;
h q[0];
This code generates the error: [line 4] single qubit cannot be indexed.
However, single qubit arrays can be indexed as follows:
OPENQASM 3;
qubit[1] q;
h q[0]; // This is valid
193
Amazon Braket Developer Guide
The physical qubits in a two qubit
gate are not connected error
The physical qubits in a two qubit gate are not
connected error
To use physical qubits, first confirm that the device uses physical qubits by checking
device.properties.action[DeviceActionType.OPENQASM].supportPhysicalQubits and
then verify the connectivity graph by checking
device.properties.paradigm.connectivity.connectivityGraph or
device.properties.paradigm.connectivity.fullyConnected.
OPENQASM 3;
cnot $0, $14;
This code generates the error message: [line 3] has disconnected qubits 0 and 14
GetDevice does not return OpenQASM results error
If you do not see OpenQASM results in the GetDevice response when using a Braket SDK, you may need
to set AWS_EXECUTION_ENV environment variable to configure user-agent. See the code examples
provided below for how to do this for the Go and Java SDKs.
To set AWS_EXECUTION_ENV environment variable to configure user-agent when using the AWS CLI:
% export AWS_EXECUTION_ENV="aws-cli BraketSchemas/1.8.0"
# Or for single execution
% AWS_EXECUTION_ENV="aws-cli BraketSchemas/1.8.0" aws braket <cmd> [options]
To set AWS_EXECUTION_ENV environment variable to configure user-agent when using Boto3:
import boto3
import botocore
client = boto3.client("braket",
 config=botocore.client.Config(user_agent_extra="BraketSchemas/1.8.0"))
To set AWS_EXECUTION_ENV environment variable to configure user-agent when using the JavaScript/
TypeScript (SDK v2):
import Braket from 'aws-sdk/clients/braket';
const client = new Braket({ region: 'us-west-2', credentials: AWS_CREDENTIALS,
 customUserAgent: 'BraketSchemas/1.8.0' });
To set AWS_EXECUTION_ENV environment variable to configure user-agent when using the JavaScript/
TypeScript (SDK v3):
import { Braket } from '@aws-sdk/client-braket';
const client = new Braket({ region: 'us-west-2', credentials: AWS_CREDENTIALS,
 customUserAgent: 'BraketSchemas/1.8.0' });
To set AWS_EXECUTION_ENV environment variable to configure user-agent when using the Go SDK:
os.Setenv("AWS_EXECUTION_ENV", "BraketGo BraketSchemas/1.8.0")
mySession := session.Must(session.NewSession())
194
Amazon Braket Developer Guide
Local simulator support warning
svc := braket.New(mySession)
To set AWS_EXECUTION_ENV environment variable to configure user-agent when using the Java SDK:
ClientConfiguration config = new ClientConfiguration();
config.setUserAgentSuffix("BraketSchemas/1.8.0");
BraketClient braketClient =
 BraketClientBuilder.standard().withClientConfiguration(config).build();
Local simulator support warning
The LocalSimulator supports advanced features in OpenQASM that may not be available on
QPUs or on-demand simulators. If your program contains language features specific only to the
LocalSimulator, as seen in the following example, you will receive a warning.
qasm_string = """
qubit[2] q;
h q[0];
ctrl @ x q[0], q[1];
"""
qasm_program = Program(source=qasm_string)
This code generates the warning: `This program uses OpenQASM language features only supported in
the LocalSimulator. Some of these features may not be supported on QPUs or on-demand simulators.
For more information on supported OpenQASM features, click here (p. 69).
195
Amazon Braket Developer Guide
Considerations for Amazon Braket VPC endpoints
Amazon VPC endpoints for Amazon
Braket
You can establish a private connection between your VPC and Amazon Braket by creating an interface
VPC endpoint. Interface endpoints are powered by AWS PrivateLink, a technology that enables access
to Braket APIs without an internet gateway, NAT device, VPN connection, or AWS Direct Connect
connection. Instances in your VPC don’t need public IP addresses to communicate with Braket APIs.
Each interface endpoint is represented by one or more Elastic Network Interfaces in your subnets.
With PrivateLink, traffic between your VPC and Braket does not leave the Amazon network, which
increases the security of data that you share with cloud-based applications, because it reduces your
data’s exposure to the public internet. For more information, see Interface VPC endpoints (AWS
PrivateLink) in the Amazon VPC User Guide.
Considerations for Amazon Braket VPC endpoints
Before you set up an interface VPC endpoint for Braket, ensure that you review Interface endpoint
properties and limitations in the Amazon VPC User Guide.
Braket supports making calls to all of its API actions from your VPC.
By default, full access to Braket is allowed through the VPC endpoint. You can control access if you
specify VPC endpoint policies. For more information, see Controlling access to services with VPC
endpoints in the Amazon VPC User Guide.
Set up Braket and PrivateLink
To use AWS PrivateLink with Amazon Braket, you must create an Amazon Virtual Private Cloud (Amazon
VPC) endpoint as an interface, and then connect to the endpoint through the Amazon Braket API service.
Here are the general steps of this process, which are explained in detail in later sections.
• Configure and launch an Amazon VPC to host your AWS resources. If you already have a VPC, you can
skip this step.
• Create an Amazon VPC endpoint for Braket
• Connect and run Braket quantum tasks through your endpoint
Step 1: Launch an Amazon VPC if needed
Remember that you can skip this step if your account already has a VPC in operation.
A VPC controls your network settings, such as the IP address range, subnets, route tables, and network
gateways. Essentially, you are launching your AWS resources in a custom virtual network. For more
information about VPCs, see the Amazon VPC User Guide.
196
Amazon Braket Developer Guide
Step 2: Create an interface VPC endpoint for Braket
Open the Amazon VPC console and create a new VPC with subnets, security groups, and network
gateways.
Step 2: Create an interface VPC endpoint for Braket
You can create a VPC endpoint for the Braket service using either the Amazon VPC console or the AWS
Command Line Interface (AWS CLI). For more information, see Creating an interface endpoint in the
Amazon VPC User Guide.
To create a VPC endpoint in the console, open the Amazon VPC console, open the Endpoints page, and
proceed to create the new endpoint. Make note of the endpoint ID for later reference. It is required as
part of the —endpoint-url flag when you are making certain calls to the Braket API.
Create the VPC endpoint for Braket using the following service name:
• com.amazonaws.substitute_your_region.braket
Note: If you enable private DNS for the endpoint, you can make API requests to Braket using its default
DNS name for the Region, for example, braket.us-east-1.amazonaws.com.
For more information, see Accessing a service through an interface endpoint in the Amazon VPC User
Guide.
Step 3: Connect and run Braket quantum tasks
through your endpoint
After you have created a VPC endpoint, you can run CLI commands that include the endpoint-url
parameter to specify interface endpoints to the API or runtime, such as the following example:
aws braket search-quantum-tasks --endpoint-url
 VPC_Endpoint_ID.braket.substituteYourRegionHere.vpce.amazonaws.com
If you enable private DNS hostnames for your VPC endpoint, you don’t need to specify the endpoint as
a URL in your CLI commands. Instead, the Amazon Braket API DNS hostname, which the CLI and Braket
SDK use by default, resolves to your VPC endpoint. It has the form shown in the following example:
https://braket.substituteYourRegionHere.amazonaws.com
The blog post called Direct access to Amazon SageMaker notebooks from Amazon VPC by using an AWS
PrivateLink endpoint provides an example of how to set up an endpoint to make secure connections to
SageMaker notebooks, which are similar to Amazon Braket notebooks.
If you’re following the steps in the blog post, remember to substitute the name Amazon Braket for
Amazon SageMaker. For Service Name enter com.amazonaws.us-east-1.braket or substitute your
correct AWS Region name into that string, if your Region is not us-east-1.
More about creating an endpoint
• For information about how to create a VPC with private subnets, see Create a VPC with private subnets
• For information about creating and configuring an endpoint using the Amazon VPC console or the
AWS CLI, see Creating an Interface Endpoint in the Amazon VPC User Guide.
197
Amazon Braket Developer Guide
Control access with Amazon VPC endpoint policies
• For information about creating and configuring an endpoint using AWS CloudFormation, see the
AWS::EC2::VPCEndpoint resource in the AWS CloudFormation User Guide.
Control access with Amazon VPC endpoint policies
To control connectivity access to Amazon Braket, you can attach an AWS Identity and Access
Management (IAM) endpoint policy to your Amazon VPC endpoint. The policy specifies the following
information:
• The principal (user or role) that can perform actions.
• The actions that can be performed.
• The resources on which actions can be performed.
For more information, see Controlling access to services with VPC endpoints in the Amazon VPC User
Guide.
Example: VPC endpoint policy for Braket actions
The following example shows an endpoint policy for Braket. When attached to an endpoint, this policy
grants access to the listed Braket actions for all principals on all resources.
{
 "Statement":[
 {
 "Principal":"*",
 "Effect":"Allow",
 "Action":[
 “braket:action-1",
 “braket:action-2",
 “braket:action-3”
 ],
 "Resource":"*"
 }
 ]
}
You can create complex IAM rules by attaching multiple endpoint policies. For more information and
examples, see:
• Amazon Virtual Private Cloud Endpoint Policies for Step Functions
• Creating Granular IAM Permissions for Non-Admin Users
• Controlling Access to Services with VPC Endpoints
198
Amazon Braket Developer Guide
Using tags
Tagging Amazon Braket resources
A tag is a custom attribute label that you assign or that AWS assigns to an AWS resource. A tag is
metadata that tells more about your resource. Each tag consists of a key and a value. Together these are
known as key-value pairs. For tags that you assign, you define the key and value.
In the Amazon Braket console, you can navigate to a quantum task or a notebook and view the list of
tags associated with it. You can add a tag, remove a tag, or modify a tag. You can tag a quantum task or
notebook upon creation, and then manage associated tags through the console, AWS CLI, or API.
Using tags
Tags can organize your resources into categories that are useful to you. For example, you can assign a
"Department" tag to specify the department that owns this resource.
Each tag has two parts:
• A tag key (for example, CostCenter, Environment, or Project). Tag keys are case sensitive.
• An optional field known as a tag value (for example, 111122223333 or Production). Omitting the tag
value is the same as using an empty string. Like tag keys, tag values are case sensitive.
Tags help you do the following things:
• Identify and organize your AWS resources. Many AWS services support tagging, so you can assign the
same tag to resources from different services to indicate that the resources are related.
• Track your AWS costs. You activate these tags on the AWS Billing and Cost Management dashboard.
AWS uses the tags to categorize your costs and deliver a monthly cost allocation report to you. For
more information, see Use cost allocation tags in the AWS Billing and Cost Management User Guide.
• Control access to your AWS resources. For more information, see Controlling access using tags.
More about AWS and tags
• For general information on tagging, including naming and usage conventions, see Tagging AWS
Resources in the AWS General Reference.
• For information about restrictions on tagging, see Tag naming limits and requirements in the AWS
General Reference.
• For best practices and tagging strategies, see Tagging best practices and AWS Tagging Strategies.
• For a list of services that support using tags, see the Resource Groups Tagging API Reference.
The following sections provide more specific information about tags for Amazon Braket.
Supported resources in Amazon Braket
The following resource type in Amazon Braket supports tagging:
199
Amazon Braket Developer Guide
Tag restrictions
• quantum-task resource
• Resource Name: AWS::Service::Braket
• ARN Regex: arn:${Partition}:braket:${Region}:${Account}:quantum-task/
${RandomId}
Note: You can apply and manage tags for your Amazon Braket notebooks in the Amazon Braket
console, by using the console to navigate to the notebook resource, although the notebooks actually are
Amazon SageMaker resources. For more information, see Notebook Instance Metadata in the SageMaker
documentation.
Tag restrictions
The following basic restrictions apply to tags on Amazon Braket resources:
• Maximum number of tags that you can assign to a resource: 50
• Maximum key length: 128 Unicode characters
• Maximum value length: 256 Unicode characters
• Valid characters for key and value: a-z, A-Z, 0-9, space, and these characters: _ . : / = + -
and @
• Keys and values are case sensitive.
• Don’t use aws as a prefix for keys; it’s reserved for AWS use.
Managing tags in Amazon Braket
You set tags as properties on a resource. You can view, add, modify, list, and delete tags through the
Amazon Braket console, the Amazon Braket API, or the AWS CLI. For more information, see the Amazon
Braket API reference.
Add tags
You can add tags to taggable resources at the following times:
• When you create the resource: Use the console, or include the Tags parameter with the Create
operation in the AWS API.
• After you create the resource: Use the console to navigate to the quantum task or notebook resource,
or call the TagResource operation in the AWS API.
To add tags to a resource when you create it, you also need permission to create a resource of the
specified type.
View tags
You can view the tags on any of the taggable resources in Amazon Braket by using the console to
navigate to the task or notebook resource, or by calling the AWS ListTagsForResource API operation.
You can use the following AWS API command to view tags on a resource:
• AWS API: ListTagsForResource
200
Amazon Braket Developer Guide
Edit tags
Edit tags
You can edit tags by using the console to navigate to the quantum task or notebook resource or you can
use the following command to modify the value for a tag attached to a taggable resource. When you
specify a tag key that already exists, the value for that key is overwritten:
• AWS API: TagResource
Remove tags
You can remove tags from a resource by specifying the keys to remove, by using the console to navigate
to the quantum task or notebook resource, or when calling the UntagResource operation.
• AWS API: UntagResource
Example of CLI tagging in Amazon Braket
If you’re working with the AWS CLI, here is an example command showing how to create a tag that
applies to a quantum task you create for SV1 with parameter settings of the Rigetti QPU. Notice that the
tag is specified at the end of the example command. In this case, Key is given the value state and Value
is given the value Washington.
aws braket create-quantum-task --action /
"{\"braketSchemaHeader\": {\"name\": \"braket.ir.jaqcd.program\", /
 \"version\": \"1\"}, /
 \"instructions\": [{\"angle\": 0.15, \"target\": 0, \"type\": \"rz\"}], /
 \"results\": null, /
 \"basis_rotation_instructions\": null}" /
 --device-arn "arn:aws:braket:::device/quantum-simulator/amazon/sv1" /
 --output-s3-bucket "my-example-braket-bucket-name" /
 --output-s3-key-prefix "my-example-username" /
 --shots 100 /
 --device-parameters /
 "{\"braketSchemaHeader\": /
 {\"name\": \"braket.device_schema.rigetti.rigetti_device_parameters\", /
 \"version\": \"1\"}, \"paradigmParameters\": /
 {\"braketSchemaHeader\": /
 {\"name\": \"braket.device_schema.gate_model_parameters\", /
 \"version\": \"1\"}, /
 \"qubitCount\": 2}}" /
 --tags {\"state\":\”Washington\"}
Tagging with the Amazon Braket API
• If you’re using the Amazon Braket API to set up tags on a resource, call the TagResourceAPI.
aws braket tag-resource --resource-arn $YOUR_TASK_ARN --tags {\"city\":
\"Seattle\"}
• To remove tags from a resource, call the UntagResourceAPI.
aws braket list-tags-for-resource --resource-arn $YOUR_TASK_ARN
201
Amazon Braket Developer Guide
Tagging with the Amazon Braket API
• To list all tags that are attached to a particular resource, call the ListTagsForResourceAPI.
aws braket tag-resource --resource-arn $YOUR_TASK_ARN --tag-keys "[\"city\",
\"state\"]"
202
Amazon Braket Developer Guide
Amazon Braket Metrics and Dimensions
Monitoring Amazon Braket with
Amazon CloudWatch
You can monitor Amazon Braket using Amazon CloudWatch, which collects raw data and processes it
into readable, near real-time metrics. You view historical information generated up to 15 months ago or
search metrics that have been updated in the last 2 weeks in the Amazon CloudWatch console to gain a
better perspective on how Amazon Braket is performing. To learn more, see Using CloudWatch metrics.
Amazon Braket Metrics and Dimensions
Metrics are the fundamental concept in CloudWatch. A metric represents a time-ordered set of data
points that are published to CloudWatch. Every metric is characterized by a set of dimensions. To learn
more about metrics dimensions in CloudWatch, see CloudWatch dimensions.
Amazon Braket sends the following metric data, specific to Amazon Braket, into the Amazon CloudWatch
metrics:
Quantum Task Metrics
Metrics are available if quantum tasks exist. They are displayed under AWS/Braket/By Device in the
CloudWatch console.
Metric Description
Count Number of quantum tasks.
Latency This metric is emitted when a quantum task has
completed. It represents the total time from
quantum task initialization to completion.
Dimensions for Quantum Task Metrics
The quantum task metrics are published with a dimension based on the deviceArn parameter, which
has the form arn:aws:braket:::device/xxx.
Supported Devices
For a list of supported devices and device ARNs, see Braket devices.
Note
You can view the CloudWatch log streams for Amazon Braket notebooks by navigating to the
Notebook detail page on the Amazon SageMaker console. Additional Amazon Braket notebook
settings are available through the SageMaker console.
203
Amazon Braket Developer Guide
Monitor quantum task status with EventBridge
Events and automated actions
for Amazon Braket with Amazon
EventBridge
Amazon EventBridge monitors status change events in Amazon Braket quantum tasks. Events from
Amazon Braket are delivered to EventBridge, almost in real time. You can write simple rules that indicate
which events interest you, including automated actions to take when an event matches a rule. Automatic
actions that can be triggered include these:
• Invoking an AWS Lambda function
• Activating an AWS Step Functions state machine
• Notifying an Amazon SNS topic
EventBridge monitors these Amazon Braket status change events:
• The state of qauntum task changes
Amazon Braket guarantees delivery of quantum task status change events. These events are delivered at
least once, but possibly out of order.
For more information, see the Events and Event Patterns in EventBridge.
In this section:
• Monitor quantum task status with EventBridge (p. 204)
• Example Amazon Braket EventBridge event (p. 205)
Monitor quantum task status with EventBridge
With EventBridge, you can create rules that define actions to take when Amazon Braket sends
notification of a status change regarding a Braket quantum task. For example, you can create a rule that
sends you an email message each time the status of a quantum task changes.
1. Log in to AWS using an account that has permissions to use EventBridge and Amazon Braket.
2. Open the Amazon EventBridge console at https://console.aws.amazon.com/events/.
3. Using the following values, create an EventBridge rule:
• For Rule type, choose Rule with an event pattern.
• For Event source, choose Other.
• In the Event pattern section, choose Custom patterns (JSON editor), and then paste the following
event pattern into the text area:
{
 "source": [
 "aws.braket"
 ],
 "detail-type": [
204
Amazon Braket Developer Guide
Example Amazon Braket EventBridge event
 "Braket Task State Change"
 ]
}
To capture all events from Amazon Braket, exclude the detail-type section as shown in the
following code:
{
 "source": [
 "aws.braket"
 ]
}
• For Target types, choose AWS service, and for Select a target, choose a target such as an Amazon
SNS topic or AWS Lambda function. The target is triggered when a quantum task state change
event is received from Amazon Braket.
For example, use an Amazon Simple Notification Service (SNS) topic to send an email or text
message when an event occurs. To do that, first create an Amazon SNS topic using the Amazon SNS
console. To learn more, see Using Amazon SNS for user notifications.
For details about creating rules, see Creating Amazon EventBridge rules that react to events.
Example Amazon Braket EventBridge event
For information on the fields for an Amazon Braket Quantum Task Status Change event, see Events and
Event Patterns in EventBridge.
The following attributes appear in the JSON "detail" field.
• quantumTaskArn (str): The quantum task for which this event was generated.
• status (Optional[str]): The status to which the quantum task transitioned.
• deviceArn (str): The device specified by the user for which this quantum task was created.
• shots (int): The number of shots requested by the user.
• outputS3Bucket (str): The output bucket specified by the user.
• outputS3Directory (str): The output key prefix specified by the user.
• createdAt (str): The quantum task creation time as an ISO-8601 string.
• endedAt (Optional[str]): The time at which the quantum task reached a terminal state. This field is
present only when the quantum task has transitioned to a terminal state.
The following JSON code shows an example of an Amazon Braket Quantum Task Status Change event.
{
 "version":"0",
 "id":"6101452d-8caf-062b-6dbc-ceb5421334c5",
 "detail-type":"Braket Task State Change",
 "source":"aws.braket",
 "account":"012345678901",
 "time":"2021-10-28T01:17:45Z",
 "region":"us-east-1",
 "resources":[
 "arn:aws:braket:us-east-1:012345678901:quantum-task/834b21ed-77a7-4b36-a90cc776afc9a71e"
 ],
205
Amazon Braket Developer Guide
Example Amazon Braket EventBridge event
 "detail":{
 "quantumTaskArn":"arn:aws:braket:us-east-1:012345678901:quantumtask/834b21ed-77a7-4b36-a90c-c776afc9a71e",
 "status":"COMPLETED",
 "deviceArn":"arn:aws:braket:::device/quantum-simulator/amazon/sv1",
 "shots":"100",
 "outputS3Bucket":"amazon-braket-0260a8bc871e",
 "outputS3Directory":"sns-testing/834b21ed-77a7-4b36-a90c-c776afc9a71e",
 "createdAt":"2021-10-28T01:17:42.898Z",
 "eventName":"MODIFY",
 "endedAt":"2021-10-28T01:17:44.735Z"
 }
}
206
Amazon Braket Developer Guide
Amazon Braket Information in CloudTrail
Amazon Braket API logging with
CloudTrail
Amazon Braket is integrated with AWS CloudTrail, a service that provides a record of actions taken by
a user, role, or an AWS service in Amazon Braket. CloudTrail captures all API calls for Amazon Braket as
events. The calls captured include calls from the Amazon Braket console and code calls to the Amazon
Braket Braket operations. If you create a trail, you can enable continuous delivery of CloudTrail events to
an Amazon S3 bucket, including events for Amazon Braket. If you do not configure a trail, you can still
view the most recent events in the CloudTrail console in Event history. Using the information collected
by CloudTrail, you can determine the request that was made to Amazon Braket, the IP address from
which the request was made, who made the request, when it was made, and additional details.
To learn more about CloudTrail, see the AWS CloudTrail User Guide.
Amazon Braket Information in CloudTrail
CloudTrail is enabled on your AWS account when you create the account. When activity occurs in Amazon
Braket, that activity is recorded in a CloudTrail event along with other AWS service events in Event
history. You can view, search, and download recent events in your AWS account. For more information,
see Viewing Events with CloudTrail Event History.
For an ongoing record of events in your AWS account, including events for Amazon Braket, create a
trail. A trail enables CloudTrail to deliver log files to an Amazon S3 bucket. By default, when you create
a trail in the console, the trail applies to all AWS Regions. The trail logs events from all Regions in the
AWS partition and delivers the log files to the Amazon S3 bucket that you specify. Additionally, you can
configure other AWS services to further analyze and act upon the event data collected in CloudTrail logs.
For more information, see the following:
• Overview for Creating a Trail
• CloudTrail Supported Services and Integrations
• Configuring Amazon SNS Notifications for CloudTrail
• Receiving CloudTrail Log Files from Multiple Regions and Receiving CloudTrail Log Files from Multiple
Accounts
All Amazon Braket actions are logged by CloudTrail. For example, calls to the GetQuantumTask or
GetDevice actions generate entries in the CloudTrail log files.
Every event or log entry contains information about who generated the request. The identity
information helps you determine the following:
• Whether the request was made with temporary security credentials for a role or federated user.
• Whether the request was made by another AWS service.
For more information, see the CloudTrail userIdentity Element.
207
Amazon Braket Developer Guide
Understanding Amazon Braket Log File Entries
Understanding Amazon Braket Log File Entries
A trail is a configuration that enables delivery of events as log files to an Amazon S3 bucket that you
specify. CloudTrail log files contain one or more log entries. An event represents a single request from
any source and includes information about the requested action, the date and time of the action, request
parameters, and so on. CloudTrail log files are not an ordered stack trace of the public API calls, so they
don’t appear in any specific order.
The following example is a log entry for the GetQuantumTask action, which gets the details of a
quantum task.
{
 "eventVersion": "1.05",
 "userIdentity": {
 "type": "AssumedRole",
 "principalId": "foobar",
 "arn": "foobar",
 "accountId": "foobar",
 "accessKeyId": "foobar",
 "sessionContext": {
 "sessionIssuer": {
 "type": "Role",
 "principalId": "foobar",
 "arn": "foobar",
 "accountId": "foobar",
 "userName": "foobar"
 },
 "webIdFederationData": {},
 "attributes": {
 "mfaAuthenticated": "false",
 "creationDate": "2020-08-07T00:56:57Z"
 }
 }
 },
 "eventTime": "2020-08-07T01:00:08Z",
 "eventSource": "braket.amazonaws.com",
 "eventName": "GetQuantumTask",
 "awsRegion": "us-east-1",
 "sourceIPAddress": "foobar",
 "userAgent": "aws-cli/1.18.110 Python/3.6.10
 Linux/4.9.184-0.1.ac.235.83.329.metal1.x86_64 botocore/1.17.33",
 "requestParameters": {
 "quantumTaskArn": "foobar"
 },
 "responseElements": null,
 "requestID": "20e8000c-29b8-4137-9cbc-af77d1dd12f7",
 "eventID": "4a2fdb22-a73d-414a-b30f-c0797c088f7c",
 "readOnly": true,
 "eventType": "AwsApiCall",
 "recipientAccountId": "foobar"
}
The following shows a log entry for the GetDevice action, which returns the details of a device event.
{
 "eventVersion": "1.05",
 "userIdentity": {
 "type": "AssumedRole",
 "principalId": "foobar",
 "arn": "foobar",
 "accountId": "foobar",
 "accessKeyId": "foobar",
208
Amazon Braket Developer Guide
Understanding Amazon Braket Log File Entries
 "sessionContext": {
 "sessionIssuer": {
 "type": "Role",
 "principalId": "foobar",
 "arn": "foobar",
 "accountId": "foobar",
 "userName": "foobar"
 },
 "webIdFederationData": {},
 "attributes": {
 "mfaAuthenticated": "false",
 "creationDate": "2020-08-07T00:46:29Z"
 }
 }
 },
 "eventTime": "2020-08-07T00:46:32Z",
 "eventSource": "braket.amazonaws.com",
 "eventName": "GetDevice",
 "awsRegion": "us-east-1",
 "sourceIPAddress": "foobar",
 "userAgent": "Boto3/1.14.33 Python/3.7.6 Linux/4.14.158-129.185.amzn2.x86_64 exec-env/
AWS_ECS_FARGATE Botocore/1.17.33",
 "errorCode": "404",
 "requestParameters": {
 "deviceArn": "foobar"
 },
 "responseElements": null,
 "requestID": "c614858b-4dcf-43bd-83c9-bcf9f17f522e",
 "eventID": "9642512a-478b-4e7b-9f34-75ba5a3408eb",
 "readOnly": true,
 "eventType": "AwsApiCall",
 "recipientAccountId": "foobar"
}
209
Amazon Braket Developer Guide
Step 1: Create an Amazon SageMaker
lifecycle configuration script
Create an Amazon Braket notebook
instance using AWS CloudFormation
You can use AWS CloudFormation to manage your Amazon Braket notebook instances. Braket notebook
instances are built on Amazon SageMaker. With CloudFormation, you can provision a notebook instance
with a template file that describes the intended configuration. The template file is written in JSON or
YAML format. You can create, update, and delete instances in an orderly and repeatable fashion. You may
find this useful when you manage multiple Braket notebook instances in you AWS account.
After you create a CloudFormation template for a Braket notebook, you use AWS CloudFormation to
deploy the resource. For more information, see Creating a stack on the AWS CloudFormation console in
the AWS CloudFormation user guide.
To create a Braket notebook instance using CloudFormation, you perform these three steps:
1. Create an Amazon SageMaker lifecycle configuration script.
2. Create an AWS Identity and Access Management (IAM) role to be assumed by SageMaker.
3. Create a SageMaker notebook instance with the prefix amazon-braketYou can reuse the lifecycle configuration for all of the Braket notebooks that you create. You can also
reuse the IAM role for the Braket notebooks that you assign the same execution permissions.
Step 1: Create an Amazon SageMaker lifecycle
configuration script
Use the following template to create a SageMaker lifecycle configuration script. The script customizes
an SageMaker notebook instance for Braket. For configuration options for the lifecycle CloudFormation
resource, see AWS::SageMaker::NotebookInstanceLifecycleConfig in the AWS CloudFormation user guide.
BraketNotebookInstanceLifecycleConfig:
 Type: "AWS::SageMaker::NotebookInstanceLifecycleConfig"
 Properties:
 NotebookInstanceLifecycleConfigName: BraketLifecycleConfig-${AWS::StackName}
 OnStart:
 - Content:
 Fn::Base64: |
 #!/usr/bin/env bash
 sudo -u ec2-user -i #EOS
 aws s3 cp s3://braketnotebookcdk-prod-i-notebooklccs3bucketb3089-1cysh30vzj2ju/
notebook/braket-notebook-lcc.zip braket-notebook-lcc.zip
 unzip braket-notebook-lcc.zip
 ./install.sh
 EOS
 exit 0
210
Amazon Braket Developer Guide
Step 2: Create the IAM role assumed by Amazon SageMaker
Step 2: Create the IAM role assumed by Amazon
SageMaker
When you use a Braket notebook instance, SageMaker performs operations on your behalf. For example,
suppose you run a Braket notebook using a circuit on a supported device. Within the notebook instance,
SageMaker runs the operation on Braket for you. The notebook execution role defines the exact
operations that SageMaker is permitted to execute on your behalf. For more information, see SageMaker
roles in the Amazon SageMaker developer guide.
Use the following example to create a Braket notebook execution role with the required permissions. You
can modify the policies according to your needs.
Note
Make sure that the role has permission for the s3:ListBucket and s3:GetObjectoperations
on Amazon S3 buckets prefixed with braketnotebookcdk-". The lifecycle configuration script
requires these permissions to copy the Braket notebook installation script.
ExecutionRole:
 Type: "AWS::IAM::Role"
 Properties:
 RoleName: !Sub AmazonBraketNotebookRole-${AWS::StackName}
 AssumeRolePolicyDocument:
 Version: "2012-10-17"
 Statement:
 -
 Effect: "Allow"
 Principal:
 Service:
 - "sagemaker.amazonaws.com"
 Action:
 - "sts:AssumeRole"
 Path: "/service-role/"
 ManagedPolicyArns:
 - arn:aws:iam::aws:policy/AmazonBraketFullAccess
 Policies:
 -
 PolicyName: "AmazonBraketNotebookPolicy"
 PolicyDocument:
 Version: "2012-10-17"
 Statement:
 - Effect: Allow
 Action:
 - s3:GetObject
 - s3:PutObject
 - s3:ListBucket
 Resource:
 - arn:aws:s3:::amazon-braket-*
 - arn:aws:s3:::braketnotebookcdk-*
 - Effect: "Allow"
 Action:
 - "logs:CreateLogStream"
 - "logs:PutLogEvents"
 - "logs:CreateLogGroup"
 - "logs:DescribeLogStreams"
 Resource:
 - !Sub "arn:aws:logs:*:${AWS::AccountId}:log-group:/aws/sagemaker/*"
 - Effect: "Allow"
 Action:
 - braket:*
 Resource: "*"
211
Amazon Braket Developer Guide
Step 3: Create an Amazon SageMaker notebook
instance with the prefix amazon-braketStep 3: Create an Amazon SageMaker notebook
instance with the prefix amazon-braketUse the SageMaker lifecycle script and the IAM role created in step 1 and step 2 to create a SageMaker
notebook instance. The notebook instance is customized for Braket and can be accessed with the
Amazon Braket console. For more information about configuration options for this CloudFormation
resource, see AWS::SageMaker::NotebookInstance in the AWS CloudFormation user guide.
BraketNotebook:
 Type: AWS::SageMaker::NotebookInstance
 Properties:
 InstanceType: ml.t3.medium
 NotebookInstanceName: !Sub amazon-braket-notebook-${AWS::StackName}
 RoleArn: !GetAtt ExecutionRole.Arn
 VolumeSizeInGB: 30
 LifecycleConfigName: !GetAtt
 BraketNotebookInstanceLifecycleConfig.NotebookInstanceLifecycleConfigName
212
Amazon Braket Developer Guide
API & SDK Reference Guide for
Amazon Braket
Amazon Braket provides APIs, SDKs, and a command line interface that you can use to create and
manage notebook instances and train and deploy models.
• Amazon Braket Python SDK (Recommended)
• Amazon Braket API Reference
• AWS Command Line Interface
• AWS SDK for .NET
• AWS SDK for C++
• AWS SDK for Go
• AWS SDK for Java
• AWS SDK for JavaScript
• AWS SDK for PHP
• AWS SDK for Python (Boto)
• AWS SDK for Ruby
You can also get code examples from the Amazon Braket Tutorials GitHub repository.
• Braket Tutorials GitHub
213
