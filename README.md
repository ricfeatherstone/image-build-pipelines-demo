# Image Build Pipelines Demo

Demonstrating using BuildConfigs and ImageStreams in OpenShift to create chained Image Build Pipelines

Create a project

`oc new-project image-build-pipelines-demo`

Create the base image BuildConfig and ImageStream

```
oc new-build https://github.com/ricfeatherstone/image-build-pipelines-demo \
    --name=base-image \
    --context-dir=base-image \
    --to=base-image
```

Create the framework image BuildConfig and ImageStream

```
oc new-build https://github.com/ricfeatherstone/image-build-pipelines-demo \
    --name=framework-image \
    --context-dir=framework-image \
    --to=framework-image
```

Create the application image BuildConfig and ImageStream

```
oc new-build https://github.com/ricfeatherstone/image-build-pipelines-demo \
    --name=application-image \
    --context-dir=application-image \
    --to=application-image
```

Start the base build and watch the image change triggers invoke the downstream builds

```
oc start-build base-image
watch oc get builds
``` 