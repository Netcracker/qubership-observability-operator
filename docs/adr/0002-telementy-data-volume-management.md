# Telemetry Data Volume Management for Qubership

## Status
Accepted  
#### Date  
2025-03-11 
#### Owner  
[Denis Filatov](https://github.com/denifilatoff)
#### Participants and approvers  
- [IldarMinaev](https://github.com/IldarMinaev)
- [Vladimir Sitnikov](https://github.com/vlsi)
- [Alexey Karasev](https://github.com/asatt)
#### Related ADRs  
None

## Context
Qubership platform needs to reduce and manage the volume of observability data generated by different telemetry sources. By default, a large amount of data is generated, and not all of it is valuable. The goal is to understand and manage the data volumes effectively.

The following user journey for telemetry was discussed:
1. Analyze metrics for telemetry generation from each source and aggregated.
2. Identify issues (useless or redundant data) through drill-down into actual data samples.
3. Propose a solution for improvement.
4. Analyze the effectiveness of the solution.
5. Apply changes to real environments.
6. Create a template from the new configuration and apply it across similar data sources.

We reviewed how telemetry management is implemented at [BindPlane](https://bindplane.com/).

## Decision
We will not implement the full UI-based e2e telemetry management journey within Qubership due to the high cost of developing a separate UI for this. Open-source solutions were also not found for this purpose. Instead, the following functions will be implemented:
1. Monitoring data volumes for each data source with visualization in a dashboard.
2. Configuration control based on the concept of a Monitoring Pack.

We will also monitor the development of the Open Agent Management Protocol (OpAMP) protocol and its server and client-side implementations. Currently, it is in development and cannot be used in production.

- [OpAMP Protocol in Go](https://github.com/open-telemetry/opamp-go)
- [OpAMP Specification](https://github.com/open-telemetry/opamp-spec)

### Justification
- The full e2e user journey for telemetry data management would be expensive to develop, particularly the need for a custom UI, which does not justify the costs at this stage.
- Monitoring data volumes and controlling configuration are key requirements for Qubership's observability management.
- OpAMP protocol offers promising features for telemetry management, and we will keep track of its progress as it matures, though it is currently not ready for production.

## Consequences
- Without the full user journey implementation in UI, manual processes may be required for deep drill-downs and specific data improvements. 
- Heavy leraning curve will be required for manage observability data
- We will need to invest in developing a custom dashboard for monitoring and visualizing data volumes.
- A simplified approach with telemetry data volumes dashboard and Monitoring Pack will be adopted for manage cost of observability.
- Future updates may integrate OpAMP if it matures and meets production standards, enabling more efficient telemetry management.
