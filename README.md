# Sensu Monitoring Checks

This project contains a number of Sensu monitoring check
configurations to bootstrap effective monitoring with [Sensu
Go](https://sensu.io). These checks are intended to be a starting
point for Sensu Go users, some per-deployment modifications are to be
expected.

## Getting Started 

1. Download and install all of the monitoring checks. 

   ```
   $ git clone https://github.com/sensu-community/monitoring-checks.git
   $ cd monitoring-checks
   $ find . -name *.yaml -print0 | xargs -0 -n1 sensuctl create -f**
   ```
   
   _NOTE: instructions for Windows users are a work-in-progress; if you 
   are a Windows powershell expert, PRs are welcome! For everyone else, 
   please let us know if you need help using this project on a Windows 
   workstation by creating an issue (or commenting on existing issues)._
   
2. To enable checks, browse to the "Checks" view in the Sensu dashboard, select 
   a check you'd like to enable, and "Publish". 
   
   _NOTE: you may need to update existing agent subscriptions to match the 
   template project subscription names._
   
3. Familiarize yourself with the example configuration templates! There are 
   dozens (soon-to-be **hundreds**) of examples that should help you learn!


## Contributoring 

### Rules

1. Every Sensu user must be able to safely create all resources as
   defined in this project (from the project root).

2. All resource definitions must be written in YAML for consistency
   and comment support.

3. All Assets used must be registered and hosted on
   [Bonsai](https://bonsai.sensu.io).

4. Asset resources must include a version reference in their name.

5. Check definitions should recommend one or more named subscriptions. At a
   minimum this should include the corresponding sub-directory as the default
   naming convention. For example, all Postgres configs should include the
   ["postgres"](tree/master/postgres) subscription, though they may optionally
   include additional/alternate subscriptions (e.g. "pg" or "postgresql").

6. Check definitions must specify the appropriate Handler from the
   [handler list](#handler-list) for its collected data.

### Handler List

Sensu Check definitions in this project specify one or more of the
following handlers. These Handlers do not exist by default, however,
they act as references for future [Handler
sets](https://docs.sensu.io/sensu-go/5.14/reference/handlers/#handler-sets).
Handler set definitions allow groups of handlers (individual
collections of actions to take on event data) to be referenced via a
single named handler set. At any time, a user may create or modify a
Handler set with one of the following names (e.g. alert -> slack,
pagerduty).

- alert
- incident-management
- metric-storage
- event-storage
- deregistration
- remediation

## Contributing

For guidelines on how to contribute to this project and information
about what we require from project contributors, please see
[CONTRIBUTING.md](CONTRIBUTING.md).
