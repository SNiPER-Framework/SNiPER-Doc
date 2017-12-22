# General Concept

In previous chapters, we have introduced the primary components of SNiPER, including Task, Algorithm and Service, and how the event processing procedure \(event loop\) is achieved based on them. Now the vital issue is that how the DM functionalities are achieved in the event loop. This includes the layout of the event data in memory, the interfaces for users to access data, as well as the I/O of the event data.Based on our experience, it's beneficial to encapsulate the DM functionalities in a set of modules with standard interfaces, so that the user-level code does not have to care about the details of DM.

### Overall Design

The figure below shows how the DM modules interact with the event loop process in an typical application developed  on top of SNiPER. In a SNiPER task, multiple Service and Algorithm instances can be defined sharing DM modules including the data store \(i. e. DataBuffer\) and Data I/O services. During event processing, Service and Algorithm instances access event data in form of EDM objects via the common interfaces of the memory manager. Meanwhile, the data store is associated with the Data I/O services which performance the data I/O before/after each event is processed \(conversion of transient EDM objects and data files\).

![](/assets/DM.png)

### DataMemSvc

In order to simplify the kernel and decouple from the experiment-specific functionalities, SNiPER does not provide concrete DM implementation, except the DataMemSvc as the mechanism of memory management based on which developers can custom their own data store modules.

The following figure shows the design of DataMemSvc. DataMemSvc is a SNiPER service that is internally created by SNiPER kernel for each task. By calling the regist\(\) interface, an IDataBlock instance can be registered into the DataMemSvc, identified by a string parameter. IDataBlock is an abstract class that must be implemented to provide the data store functionalities. We have provided a concrete implementation of IDataBlock, the DataBuffer, as a double-ended queue to hold multiple events, which will be introduced in the following sub-chapter. After an IDataBlock instance has been registered, users can retrieve it with its string identifier, and then access data managed by them via a tool named SniperDataPtr. SniperDataPtr will be introduced in the following sub-chapter as well.

![](/assets/DataMemSvc.png)

