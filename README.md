# Test-app bundle example

Example: image bundle contains `test-app` charts from `0.1.0` to `0.1.6` versions.
[gcr.io/mapr-252711/ezua/apps/test-app:bundle][gcr-test-app]

```Yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: image-pull-job-testapp-example
  namespace: ezapp-system
spec:
  backoffLimit: 0
  template:
    spec:
      containers:
        - name: chart
          image: gcr.io/mapr-252711/ezua/apps/test-app:bundle
          imagePullPolicy: Always
      restartPolicy: Never
      imagePullSecrets:
        - name: ezapp-hpe-imagepull-secrets
```
UI will generate job like in example above, and apply it with k8s API.
After the job become succeeded, upgrade actions will be available for correspond installed applications. 

Job will produce an output: 
```sh
> kubectl logs -n ezapp-system  -l job-name=image-pull-job-testapp-example
 
NAME                               APP_VERSION         VERSION               STATUS
test-app                                1.16.0           0.1.0        ALREADY EXIST
test-app                                1.16.0           0.1.1        ALREADY EXIST
test-app                                1.16.0           0.1.2        ALREADY EXIST
test-app                                1.16.0           0.1.3        ALREADY EXIST
test-app                                1.16.0           0.1.4        ALREADY EXIST
test-app                                1.16.0           0.1.5        ALREADY EXIST
test-app                                1.16.1           0.1.6               PUSHED
```


[//]: # (Referenses)

   [gcr-test-app]: <https://console.cloud.google.com/gcr/images/mapr-252711/global/ezua/apps/test-app>
