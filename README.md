# nginx-nr-agent-patches

Some patches for nginx-nr-agent.

## Usage

1. Install `nginx-nr-agent` first.
2. Apply the latest patch.

    ```bash
    $ patch /usr/bin/nginx-nr-agent.py < patch_0.1.diff
    ```

3. Follow the configuration to edit your agent config file.
4. Restart the agent daemon.
    

## Changelog

- 2017.1.25 - Fix agent stuck with bad network connection.

    With this patch, you can specify collectors' timeout and NewRelic push client's timeout. The origin version from NGINX may be will stuck forever with bad network connection.

    You can add field `newrelic_push_timeout` in `[global]` scope. And `collector_timeout` in `[source$n]` scope.

    ```ini
    [global]
    newrelic_license_key=YOUR_LICENSE_KEY_HERE
    poll_interval=60
    newrelic_push_timeout=10

    ...

    [source1]
    name=exampleorg
    url=http://example.org/status
    collector_timeout=5
    ```

