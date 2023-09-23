# Config Defaults

The following values are used for all `KSVC` CRs, which are created by `Capp` CRs. The values are also specified in the `config-default` ConfigMap in the `knative-serving` namespace:

| Parameter                                 | Value              | Explanation                                                                                                                                                                                                                                                                                                                                                         |
| ---------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `revision-timeout-seconds`               | "300" (5 minutes)  | Sets the default number of seconds to use for the revision's per-request timeout if none is specified.                                                                                                                                                                                                                                                                                                                             |
| `max-revision-timeout-seconds`           | "600" (10 minutes) | Specifies the maximum number of seconds that can be used for `revision-timeout-seconds`. This value must be greater than or equal to `revision-timeout-seconds`. If omitted, the system default (600 seconds) is used. Note that if this value is increased, the `activator`'s `terminationGraceTimeSeconds` should also be increased to prevent in-flight requests from being disrupted. |
| `revision-response-start-timeout-seconds`| "300" (5 minutes)  | Defines the default number of seconds a request will be allowed to stay open while waiting to receive any bytes from the user's application if none is specified. By default, this value is set to match `revision-timeout-seconds`.                                                       |
| `revision-idle-timeout-seconds`          | "0" (infinite)     | Specifies the default number of seconds a request will be allowed to stay open while not receiving any bytes from the user's application if none is specified. By setting this to "0," it means there is no idle timeout, and requests can remain open indefinitely.                               |
| `revision-cpu-request`                   | "400m" (400 milli-CPU) | Sets the CPU allocation to assign to revisions by default. If omitted, no value is specified, and the system default is used. The example provided allocates 0.4 of a CPU (400 milli-CPU) to each revision.                                                                                       |
| `revision-memory-request`                | "100M" (100 megabytes) | Defines the memory allocation to assign to revisions by default. If omitted, no value is specified, and the system default is used. The example allocates 100 megabytes of memory to each revision.                                                                                              |
| `revision-ephemeral-storage-request`     | "500M" (500 megabytes) | Specifies the ephemeral storage allocation to assign to revisions by default. If omitted, no value is specified, and the system default is used. The example allocates 500 megabytes of storage to each revision.                                                                                  |
| `revision-cpu-limit`                     | "1000m" (1 CPU)  | Sets the CPU allocation limit for revisions by default. If omitted, no value is specified, and the system default is used. The example limits each revision to 1 CPU (1000 milli-CPU).                                                                                                             |
| `revision-memory-limit`                  | "200M" (200 megabytes) | Defines the memory allocation limit for revisions by default. If omitted, no value is specified, and the system default is used. The example limits each revision to 200 megabytes of memory.                                                                                                    |
| `revision-ephemeral-storage-limit`       | "750M" (750 megabytes) | Specifies the ephemeral storage allocation limit for revisions by default. If omitted, no value is specified, and the system default is used. The example limits each revision to 750 megabytes of storage.                                                                                        |
| `container-name-template`                | "user-container" | Contains a template for the default container name if none is specified. This field supports Go templating and is supplied with the `ObjectMeta` of the enclosing Service or Configuration, allowing values such as `{{.Name}}` to be used.                                                    |
| `init-container-name-template`           | "init-container" | Contains a template for the default init container name if none is specified. This field also supports Go templating and is supplied with the `ObjectMeta` of the enclosing Service or Configuration.                                                                                                  |
| `container-concurrency`                  | "0" | Specifies the maximum number of requests the Container can handle at once, and requests above this threshold are queued. Setting a value of zero disables this throttling and lets through as many requests as the pod receives.                                                                              |
| `container-concurrency-max-limit`        | "1000" | Sets the maximum limit for individual revision concurrency values or autoscaling targets. The `container-concurrency` default setting must be at or below this value. This is an operator setting and must be greater than 1. Even with this set, a user can choose a `containerConcurrency` of 0 (unbounded) unless `allow-container-concurrency-zero` is set to "false."                   |
| `allow-container-concurrency-zero`       | "true" | Controls whether users can specify 0 (unbounded) for `containerConcurrency`. If set to "true," it allows users to specify unbounded concurrency (0).                                                                                                                                     |
| `enable-service-links`                  | "false" | Specifies the default value used for the `enableServiceLinks` field of the `PodSpec` when it is omitted by the user. This field has three possible values: "true," "false," and "default." Setting this value to "false" is recommended in environments with a large number of services.                                                                                                                     |