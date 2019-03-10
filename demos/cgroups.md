# Memory cgroups demo

1. Navigate the `/sys/fs/cgroup` directory
     ```bash
        cd /sys/fs/cgroup
    ```
1. Make a `memory` directory (if it doesn't exist)
    ```bash
        mkdir -p memory
    ```
1. Mount the memory cgroup onto this directory (if it isn't done already)
    ```bash
        mount -t cgroup -o memory cgroup /sys/fs/cgroup/memory
    ```
1. Navigate into this directory and create a new subdirectory call it `M1` and navigate into that
    ```bash
        cd memory
        mkdir M1
        cd M1
    ```
1. Attach any running process to this newly created memory cgroup `M1`. Preferably a process that increases memory consumption over time. Try to locate your browser's PID using ps aux command. And enter that PID below
    ```bash
        echo {{PID}} > cgroups.procs
    ```
1. Print the memory stats
    ```bash
        cat memory.stat
    ```
1. Set memory limits
    ```bash
        echo 10M > memory.limit_in_bytes
    ```
1. Print the memory usage
    ```bash
        cat memory.usage_in_bytes
    ```
1. You will observe that memory usage for this cgroup will never go beyond the limit set
