# SFC Support for Openstack4j: code changes.

Service Function Chaining REST Api for the openstack has been available since mitaka release. It deals with four kinds of objects:
flow classifiers, port pairs, port pair groups and port chains. We have submitted the [pull request](https://github.com/ContainX/openstack4j/pull/1141) to the [openstack4j project](https://github.com/ContainX/openstack4j) which deals with flow classifiers only. These changes are summarized here.

The remaining three objects will be submitted later, following the same pattern.

## Design Changes
We add ```SFCService``` under ```api/networking/ext```. This service will be on the same level of service objects as the existing [```NetworkingService```](https://github.com/ContainX/openstack4j/blob/master/core/src/main/java/org/openstack4j/api/networking/NetworkingService.java). 

- The ```SFCService``` will return ```FlowClassifierService``` from ```flowclassifiers()``` call.
- Similar calls will later be added for  ```PortGroupService```, ```PortPairService```, ```PortGroupChainService```.
- These four services will be lower-level CRUD services, much like  [```NetworkService```](https://github.com/ContainX/openstack4j/blob/master/core/src/main/java/org/openstack4j/api/networking/NetworkService.java).
- All four lower-level services will implement [```Buildable```](https://github.com/ContainX/openstack4j/blob/master/core/src/main/java/org/openstack4j/common/Buildable.java) and the builders will be provided in the Impl.
-  ```OS.sfc()``` call shall return an implementation of  ```SFCService```

### Code changes.

The following files were added or modified. The new files are underlined red.

![Code changes](./images/FileChanges.png "Code changes")

### FlowClassifier class diagram.
Flow classifiers follow the existing pattern:

![Class diagram](./images/classdiag.png "FlowClassifiers follow the existing pattern")

## Assignees
Dmitry Gerenrot ([dmitryintel](https://github.com/dmitryintel)).

## References
[SFC REST Api for openstack](https://github.com/ContainX/openstack4j/blob/master/core/src/main/java/org/openstack4j/api/networking/NetworkingService.java)

[ContainX/openstack4j project](https://github.com/ContainX/openstack4j)
