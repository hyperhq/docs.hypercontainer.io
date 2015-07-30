# Ephemeral & Persistent

Although a HyperVM instance is considered as an ephemeral entity due to its nature of sub-second boot, it certainly could be also used as long-running and durable.

- Ephemeral


    In a microservice architecture, apps are scheduled to (physical) hosts. Where a new Hyper instance is created, the app is loaded into the instance and remains there until termination or deletion. When an app died (or the instance), the app will be scheduled to another host, with a new instance. If a host died, either all apps on the host can be rescheduled, or all instances on the host can be restarted on other hosts (if shared storage available).

- Persistent


    For big data application (Hadoop, Spark), new jobs are consistently dispatched to hosts. Instead of creating ephemeral instances for each task, the application could use persistent Hyper instance and "submit" jobs by calling Hyper's REST API to replace the binary in the instance.
