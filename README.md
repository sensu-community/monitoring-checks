# Sensu Monitoring Checks

This project contains a number of Sensu monitoring check
configurations to bootstrap effective monitoring with [Sensu
Go](https://sensu.io). These checks are intended to be a starting
point for Sensu Go users, some per-deployment modifications are to be
expected.

## Rules

1. Every Sensu user must be able to safely create all resources as
defined in this project (from the project root).

2. All resource definitions must be written in YAML for consistency
and comment support.

3. All Assets used must be registered and hosted on
[Bonsai](https://bonsai.sensu.io).

4. Asset resources must include a version reference in their name.

5. Check definitions must specify the appropriate Handler from the
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

TODO: Write me.
