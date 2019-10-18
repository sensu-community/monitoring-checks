# Sensu Monitoring Checks

Hello world.

## Rules

1. Every Sensu user must be able to safely create all resources as
defined in this project (from the project root). 

2. All Assets used must be registered and hosted on
[Bonsai](https://bonsai.sensu.io).

3. Asset resources must include a version reference in their name.

4. Check definitions must specify the appropriate handler from the
[handler list](#handler-list) for its collected data.

### Handler List

- alert
- incident-management
- metric-storage
- event-storage
- deregistration
- remediation
