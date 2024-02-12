# Software Detailed Design - `DiagId provider`

## Introduction

### Document overview

This document describes the `<Diagnostic Id provider>` detailed design.

### Definitions, Acronyms and Abbreviations

Local acronyms, abbreviations and definitions:

|Acronym         | Definition|
|---             |---                       |
|DID |Data identifier                |
|RID |Routine identifier                          |
|ECU | Electronic control unit |

### Standard and regulatory references

`<Diag Id provider>` standards and references can be found [here](<add link>).

## Detailed Design

### Overview

*The Diagnostic ID Provider (diag_id_provider) is a library that can be used to develop application services aimed to provide DID/RID. It has functionality to notify on session change and on security level change.*

***Label declaration***

A software label used to define a diagnostic entity shall follow the naming pattern: [Node]_[SWC]_[Entity_name].

* Node: a name of the ECU which the entity belongs to;
* SWC: software component which instantiated the entity;
* Entity_name: a name of the particular entity.*

***Adding Providers:*** 

Application developers might want to provide Read/Write Data functionality, Routine Control functionality, be notified on session change functionality, security level or all of the above. 

In order to do that the developer needs to inherit from DidProvider and/or RidProvider, implement the necessary methods and add itself by calling DiagIdCommunicator::AddDidProvider() or DiagIdCommunicator::AddRidProvider() from the DiagIdCommunicator class that should be initialized with the instance ID of your Application. Under the hood the instance ID will be used in order to establish communication with the HP UDS Server using Service Framework.*

***Starting the communication***

In order to signal that the Application is ready, the developer should call the DiagIdCommunicator::Start() method passing csp::afw::core::ContextualObject of the Application. 

ContextualObject should be valid both when calling DiagIdCommunicator::Start() as well as later, as it will be used during IPC communication (if you inherit from csp::afw::core::Executable, the best moment to call Start() is from OnWillStart()).*

### Implementation view

DidProvider | RidProvider | 
---------|----------|
  sw_label | sw_label | 
 value | option record | 
 control_status| status |
   ReadDid | StartRoutine | 
 WriteDid | StopRoutine | 
 ReturnControl| GetRoutineResults |  
 ResetToDefault| idOnSessionChange|
 FreezeState |RidOnSecurityLevelChange |
 ShortTermAdjustment ||*

## Public interfaces TBD

*Describe the component's public interfaces, i.e. what other SWAD components can access.
This is a high level description of the component's public interface. The intention
is to understand the outer boundary of the component, which is used for interaction
with other SWAD components. This is used as input to the implementation, so do not expect
details such as the same method names or input parameters as in the source code.*

| Interface method | Data flow direction | Short description|
----------- | ----------- | -------------- |
| Set Something | Input   | Set ... |
| Get Something | Output  | Get ... |

### Process view TBD

*Provide sequence and (if applicable) state diagrams showing the
dynamic behavior of the SWDD units.*

*Include startup and shutdown sequences in this section.*

## Requirements

*List all requirements allocated to the SWAD component, using the table format
below. Do not modify the format, it is consumed by tooling.*

*Requirement breakdown and allocation to SWDD units.*

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-001`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_common_types_line23
**Description:**             | The software shall ensure that the enumeration values of uds::Nrc::kPositiveResponse and Nrc::kPositiveResponse are identical

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-002`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_common_types_line24
**Description:**             | The software shall ensure that the enumeration values of uds::Nrc::kSubFunctionNotSupported and Nrc::kSubFunctionNotSupported are identical

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-003`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_common_types_line25
**Description:**             | The software shall ensure that the enumeration values of uds::Nrc::kConditionsNotCorrect and Nrc::kConditionsNotCorrect are identical.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-004`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_common_types_line26
**Description:**             | The software shall ensure that the enumeration values of uds::Nrc::kPositiveResponse and Nrc::kPositiveResponse are identical

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-005`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_impl_lines23-55
**Description:**             | The software shall define a class template DiagIdCommunicatorImpl with two template parameters UdsDidCommunicationStub and UdsRidCommunicationStub.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-006`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_impl_lines27-28
**Description:**             | The software shall ensure that the enumeration values of uds::Nrc::kSubFunctionNotSupported and Nrc::kSubFunctionNotSupported are identical

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-007`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_impl_lines30-41
**Description:**             | The software shall ensure that the enumeration values of uds::Nrc::kConditionsNotCorrect and Nrc::kConditionsNotCorrect are identical.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-008`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_impl_lines43-55
**Description:**             | The software shall ensure that the enumeration values of uds::Nrc::kPositiveResponse and Nrc::kPositiveResponse are identical

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-009`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_lines18-55
**Description:**             | The software shall define a class template DiagIdCommunicatorImpl with two template parameters UdsDidCommunicationStub and UdsRidCommunicationStub

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-010`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_line21
**Description:**             | The software shall define a constructor for the DiagIdCommunicatorImpl class that takes a string_view parameter instance_id

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-011`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_line24
**Description:**             | The software shall define a method AddDidProvider in the DiagIdCommunicatorImpl class that takes a DidConfigCollection and a DidProvider as parameters

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-012`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_line26
**Description:**             | The software shall define a method AddRidProvider in the DiagIdCommunicatorImpl class that takes a RidConfigCollection and a RidProvider as parameters

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-013`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | diag_id_communicator_impl_line28
**Description:**             | The software shall define a method Start in the DiagIdCommunicatorImpl class that takes a ContextualObject as a parameter

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-014`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_config_lines13-30
**Description:**             |  The software shall include the header file "communicator/did_config.hpp", define a namespace did_config, and define three operator < overloads for the DidConfig class. The first overload compares two DidConfig instances based on their sw_lbl members. The second overload compares a DidConfig instance and a csp::string_view based on the DidConfig instance's sw_lbl member. The third overload compares a csp::string_view and a DidConfig instance based on the DidConfig instance's sw_lbl member.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-015`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_provider
**Description:**             | The software define methods for the DidProvider class.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-016`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_provider
**Description:**             | ReadDid method: This method is expected to read a Diagnostic Identifier (DID) based on a given software label (sw_label). The result should be stored in the provided value parameter. Returns NRC

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-017`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_provider
**Description:**             | WriteDid method: This method is expected to write a value to a Diagnostic Identifier (DID) based on a given software label (sw_label). The result should be stored in the provided value parameter.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-018
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_provider
**Description:**             | ReturnControlToEcu method: This method is expected to return control of a DID to the ECU (Electronic Control Unit) based on a given software label (sw_label). 

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-019`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_provider
**Description:**             | ResetToDefault method: This method is expected to reset a DID to its default state based on a given software label (sw_label). The control status record should be stored in the provided parameter.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-020`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_provider
**Description:**             | FreezeCurrentState method: This method is expected to freeze the current state of a DID based on a given software label (sw_label). The control status record should be stored in the provided parameter. 

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-021
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_provider
**Description:**             | ShortTermAdjustment method: This method is expected to make a short-term adjustment to a DID based on a given software label (sw_label). The control state and control status record should be stored in the provided parameters.  

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-022`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | did_provider
**Description:**             | Each method shall contain the parameters (/*sw_label*/, /*value*/, /*control_status_record*/, /*control_state*/)

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-023`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | rid_config_lines13-30
**Description:**             |  The software shall include the header file "communicator/rid_config.hpp", define a namespace did_config, and define three operator < overloads for the RidConfig class. The first overload compares two RidConfig instances based on their sw_lbl members. The second overload compares a RidConfig instance and a csp::string_view based on the RidConfig instance's sw_lbl member. The third overload compares a csp::string_view and a RidConfig instance based on the RidConfig instance's sw_lbl member.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-024`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | rid_provider
**Description:**             | The software define methods for the RidProvider class.


Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-025`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | rid_provider
**Description:**             | StartRoutine method: This method is expected to start a routine based on a given software label (sw_label). The option_record parameter is expected to provide additional options for starting the routine, and the status parameter is expected to hold the status of the operation.

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-026`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | rid_provider
**Description:**             | StopRoutine method: This method is expected to stop a routine based on a given software label (sw_label). The option_record parameter is expected to provide additional options for stopping the routine, and the status parameter is expected to hold the status of the operation

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-027`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | rid_provider
**Description:**             | GetRoutineResults method: This method is expected to get the results of a routine based on a given software label (sw_label). The option_record parameter is expected to provide additional options for getting the routine results, and the status parameter is expected to hold the status of the operation. . 

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-028`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | rid_provider
**Description:**             | RidOnSessionChange method: This method is expected to handle a change in the diagnostic session (new_session).

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-029`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | rid_provider
**Description:**             | RidOnSecurityLevelChange method: This method is expected to handle a change in the security level (level).  

Requirement:                 ||
-----------------------------|------------------------
**Requirement ID:**          | `DiagIDprovider-REQ-030`
**Parent Requirement ID:**   | Versioned CW requirement ID
**ASIL:**                    | `ASIL-B`
**Affected file:**     | rid_provider
**Description:**             | Each method shall contain the parameters (/*sw_label*/, /*option_record*/, /*status*/, /*new_session*/, /*level*/),