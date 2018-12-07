# Honeybadger CircleCI Orb

The Honeybadger CircleCI Orb is used to notify the [Honeybadger API][1]
from your CircleCI workflows.

To use this orb in your project, you need to enable two settings:

- __Settings -> Security -> Allow uncertified orbs__
- __Settings -> Advanced Settings -> Enable build processing (preview)__

## Usage

### Deployment Notifications

Sending deployment notifications to Honeybadger allows your team to associate
spikes in errors to changes that were deployed.

You can add a job definition to `circle.yml` that invokes the
`notify_deploy` command from this orb:

```yaml
jobs:
  test:
    ...

  deploy:
    docker:
       - image: circleci/ruby:2.5.3-node-browsers
    steps:
      - run:
          ...
      - honeybadger/notify_deploy:
          api_key: YOUR_HONEYBADGER_API_KEY
```

Then include that job in your workflow:

```yaml
workflows:
  test:
    jobs:
      - test
      - deploy:
          requires:
            - test
```

This will invoke the deploy job after the test job is completed.

## More Info

See https://circleci.com/orbs/registry/orb/honeybadger-io/deploy for
more info on the parameters you can use.

[1]: https://docs.honeybadger.io/guides/api/
