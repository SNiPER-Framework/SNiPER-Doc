**Example: JUNO Data Management**

The JUNO offline software is designed to fulfill many requirements including Monte Carlo \(MC\) data produc- tion, raw data calibration, and event reconstruction as well as to provide tools for the physics analysis.The JUNO offline software is based on the general SNiPER framework with the main components implemented as SNiPER plugins.

The DM modules are the core parts of the JUNO offline software, including the event data model \(EDM\), memory management modules and ROOT I/O systems. The figure below illustrates the JUNO offline software workflow, where the DM module play a vital part.

![](/assets/offlineworkflow.png)

Take the simulated data production as an example, the Generator stage applies physics generators to produce GenEvent objects. These GenEvent objects are used as the input to the Simulation stage which models the detector and electronics response. Similarly the Calibration and Reconstruction stages read data from the previous step and produce CalibEvent and RecEvent objects, respectively. All event data objects, such as GenEvent, SimEvent, RawEvent, CalibEvent and RecEvent, are defined and implemented by the JUNO EDM. During data processing, The EDM objects are held in a dynamically allocated region of memory named DataBuffer managed by the memory manager module. The event data at all stages can be persisted to files in the form of ROOT TTrees or read back into memory by the ROOT I/O system.

This sub-chapter introduces the design of JUNO DM modules based on the SNiPER scheme, aimed at inspiring the software developers of other experiments.



