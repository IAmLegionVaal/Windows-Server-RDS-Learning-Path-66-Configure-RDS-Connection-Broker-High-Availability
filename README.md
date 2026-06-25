# Windows Server RDS Learning Path 66 — Configure RDS Connection Broker High Availability

**Level:** Expert · **Module:** 66/70

## Goal
Design and deploy Connection Broker high availability using a supported SQL backend and shared client-access name.

## Prerequisites
- Second Broker server
- Supported SQL database
- HA DNS name and certificate
- Database backup and rollback plan

## Setup
1. Prepare SQL connectivity, permissions and backups.
2. Add the second Broker server to the deployment.
3. Configure Broker HA with the approved database connection strings and client-access name.
4. Create DNS for the shared Broker name.
5. Assign certificates matching that name.
6. Validate both Broker services and database connectivity.
7. Test one Broker node unavailable, then restore it.

Set the values for the lab before running validation:

```powershell
$ConnectionBroker = 'rdcb01.corp.lab'
$BrokerHaName = 'rdsbroker.corp.lab'

Get-RDConnectionBrokerHighAvailability -ConnectionBroker $ConnectionBroker
Get-RDServer -ConnectionBroker $ConnectionBroker
Resolve-DnsName -Name $BrokerHaName
Get-Service -Name Tssdis,RDMS
```

Confirm the shared name resolves only to the approved Broker endpoints and that the certificate presented to clients includes `$BrokerHaName`.

## Evidence
Store HA design, SQL/DNS configuration, certificate names, Broker membership, single-node outage, recovery and event logs under `evidence/`. Redact database secrets.

## Troubleshooting
HA failures commonly involve SQL permissions/connectivity, DNS, certificate names or mismatched connection strings. Validate each layer separately.

## Security
Protect database access, connection details, certificates and Broker administration. Use supported SQL availability and backup methods.

## Rollback
Restore the documented single-Broker configuration only through the supported RDS HA workflow.

## Next
`Windows-Server-RDS-Learning-Path-67-Patch-an-RDS-Host-without-User-Disruption`
