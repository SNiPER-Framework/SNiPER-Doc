The offline software system is developed for the offline data processing, including Monte Carlo \(MC\) data production as well as experimental data processing and physics analysis. Usually the offline software system consists of framework, generator, detector simulation, electronics simulation, calibration, reconstruction and physics analysis tools. The framework takes very important roles for the performance, functionality, flexibility, extensibility as well as portability of the whole offline software system in many current high energy physics \(HEP\) experiments.

The framework provides most of the common functionalities according to the offline data processing in HEP experiments, such as: data management, data processing controlling, data storage, common services and tools, friendly user interface. The framework builds the unified software environments and platform to develop application software such as Event generators, Detector simulation, Electronics Simulation, Calibration, Reconstruction and Physics analysis tools. It defines the standard interfaces between different applications, therefore many people can synchronously develop their applications. All applications developed by following the standard interfaces can be smoothly plugged into the framework and run very well.

For collider physics experiments, there is a very popular and powerful framework, Gaudi, developed by the LHCb experiment. Originally Gaudi was designed for processing independent events \(or collider experiments\) such as ATLAS, BESIII although it currently also is used by other non-collider experiments such as, FERMi, MINERvA, Daya Bay and LBNE with some extensions on their data management system.

SNiPER \(abbreviation of Software for Non-collider Physics ExpeRiment\) is designed and developed for non-collider physics Experiments from scratch with Object-Oriented technology and bi-language, C++ and Python. It evolved from the LAF \(light weighted Analysis Framework\) of Daya Bay experiment and also learned some technologies from Gaudi. SNiPER does have many innovations on the management of dependent events by introducing event buffer mechanism, multi-task processing controlling, less dependences on the third-party software and tools. SNiPER also reserved the interfaces to implementation of multi-threading computing. More details can be found at the following chapters.
