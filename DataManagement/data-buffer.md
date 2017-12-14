**Data Buffer**

DataBuffer is a dynamically allocated region of memory that holds multiple events in order to facilitate correlation analysis. The size is configured with a time window. In each execution, an event acts as the anchor of the time window and its adjacent events in the time window are cached in the DataBuffer simultaneously. During the event loops, the anchor event moves forward one by one, and events in the time window are accordingly updated.

