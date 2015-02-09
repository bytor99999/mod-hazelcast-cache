# mod-hazelcast-cache
A Vert.x 2.x module for using Hazelcast as an in-memory cache, while keeping it separate from Vert.x's Hazelcast cluster

The goal is to provide a mod-cluster.xml file that is a Hazelcast cluster xml file that is different han the one in  Vert.x install directory so that this will
create and use a different Hazelcast cluster than the one Vert.x uses for determining nodes in the Vert.x cluster.

Also a the developer using this module needs to provide a configuration stating what Hazelcast objects to create in the Hazelcast cluster as well as object types that will be put
in these Hazelcast objects. (Hazelcast objects means things like iMap or iAtomicLong)

Messages sent to this module should include things like name of the Hazelcast object to retrieve, 

used in calls
like hazelcastInstance.get("mapName")

It should also include things like Key, for key to use to lookup in Map. The Key value should be convertable to the object type of the Key used in the configuration.


This first take on the module is to be as simple as possible. So we will only support iMaps with Strings as the key, and Maps for the values that will and can be converted to other types.
So those other types will need to have a constructor that takes the Map and takes the values in the Map to populate the object's values. This will allow the data to be inserted into or out of the 
Maps to be using Json that is passed in the Vert.x eventbus to this module. And since this module is written with Groovy language Maps and Json are very easy to work with and to convert to object types.