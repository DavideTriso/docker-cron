# Docker CRON

## Overview

The image is designed to facilitate the scheduling and execution of cron jobs within a containerized environment.

## How to Use
The image provide a convenient folder structure in the `/etc/periodic` path, which includes the following subfolders:

* 1min
* 5min
* 10min
* 15min
* 20min
* 30min
* hourly
* daily
* weekly
* monthly

To schedule a task, simply place the script in one of the folders corresponding to the desired execution interval:

1. Create a script that contains the task you want to schedule. For example, you can create a file named `my-cronjob` with the following content:

```ash
#!/bin/bash
echo "Executing my cron job"
# Add your cron job task here ...
```
> NOTE: Please ensure that the script has no file extension.

2.  Place the script in one of the folders corresponding to the desired execution interval.

```yaml
cron:
    image: davidetriso/cron:alpine-3.18
    # ... other settings here ...
    volumes:
        # ... other volumes and mounts here ...
        - ./my-cronjob:/etc/periodic/5min/my-cronjob:rw
```

> NOTE: When the container starts up, all scripts located in the subfolders of `/etc/periodic/` are made executable using the chmod command. Hence, it is important to ensure that these files are writable by the container.
