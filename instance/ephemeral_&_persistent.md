# Ephemeral & Persistent

Due to the sub-second boot performance, Hyper instance could be considered as ephemeral entities, though it certainly clould be also used as long-running and durable.

- Ephemeral


    In a microservice architecture, apps are scheduled to (physical) hosts, where a new Hyper instance is created, the app is loaded into the instance and remains there until termination or deletion. When an app dies (or the instance), the app will be scheduled to another host with new instance. If a host dies, either all apps on the host can be rescheduled, or all instances on the host can be restarted on other hosts (if shared storage available).

- Persistent


    For big data application (Hadoop, Spark), new jobs are consistently dispatched to hosts. Instead of creating ephemeral instances for each task, the application could use persistent Hyper instance and "submit" jobs by calling Hyper's REST API to replace the binary in the instance.



