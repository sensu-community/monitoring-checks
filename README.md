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

4. Asset resources must include a version reference in their name.  For
   example `sensu-plugins/sensu-plugins-disk-checks:5.0.1`.

5. Check definitions should recommend one or more named subscriptions. At a
   minimum this should include the corresponding sub-directory as the default
   naming convention. For example, all Postgres configs should include the
   ["postgres"](tree/master/postgres) subscription, though they may optionally
   include additional/alternate subscriptions (e.g. "pg" or "postgresql").

6. Check definitions must NOT include a namespace.

7. Check definitions must be set to "publish: false".

8. Check definitions should use the "interval" scheduler, with a minimum of
   30 seconds.

9. Check timeout should be set to a non-zero value and should not be greater
   than 50% of the interval.

10. Check definitions must include the following required fields, even if they
    are blank or are the defaults:

    * `command`
    * `interval`
    * `timeout`
    * `ttl`
    * `publish`
    * `subscriptions`
    * `runtime_assets`
    * `handlers`
    * `stdin`
    * `proxy_entity_name: ""`

11. Long check commands should be wrapped using the YAML `>-` multiline
    "block scalar" syntax.

    ```yaml
    spec:
      command: >-
        check-disk-usage.rb
        -w {{ .annotations.disk_usage_warning | default 85 }}
        -c {{ .annotations.disk_usage_critical | default 95 }}
    ```

12. As seen in the example above, check commands should include tunables
    using Sensu tokens from annotations and explicitly set the defaults.

13. Resources should be defined in the following order by type:

    * CheckConfig
    * HookConfig
    * Secret
    * Asset

14. Check definitions must specify the appropriate Handler from the
    [handler list](#handler-list) for its collected data.

15. All PRs submitted are ran through [super-linter](https://github.com/github/super-linter/).
    You are encouraged to [run it locally](https://github.com/github/super-linter/blob/master/docs/run-linter-locally.md)
    to reduce the churn of having to fix issues after submission.

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
