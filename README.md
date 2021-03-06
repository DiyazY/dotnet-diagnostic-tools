# dotnet-diagnostic-tools
Artifacts for diagnostic dotnet applications.


# how to run test!
Visit [page](https://github.com/DiyazY/dotnet-diagnostic-tools/packages) and pull the image.  

Create a volume  
```
# from local terminal
> docker volume create --name tmp

> docker container  run --rm -d -p 8002:80 -v tmp:/tmp --name [test-app]  [image]

option 1:  
> docker container  run --rm -ti -v tmp:/tmp --name [sidecar-container]  docker.pkg.github.com/diyazy/dotnet-diagnostic-tools/tools:[version]

option 2:
> docker container  run --rm -ti --volumes-from [test-app] --name [sidecar-container]  docker.pkg.github.com/diyazy/dotnet-diagnostic-tools/tools:[version]

# from sidecar-container
> dotnet-trace ps  
         1 bash       /bin/bash
```

# Run dotnet-trace

```
# from sidecar-container
> dotnet-trace collect -p [1] --format [Chromium] -o [trace.json]

#stop tracing: press ctrl+c

# from local terminal
> docker cp [containerId]:tools/trace.chromium.json [.]
```
# Run dotnet-counters
// TODO: adjust parameters later  
```
# from sidecar-container
> dotnet-counters collect --process-id [1] --refresh-interval 10 --output counters --format json

#stop counting: press ctrl+c

# from local terminal
> docker cp [containerId]:tools/counters.json [.]
```
# Run dotnet-dump
// TODO: needs some fixes. it fails on mac  
```
# from sidecar-container
> dotnet-dump collect -p [1]

```

# Run dotnet-gcdump
```
# from sidecar-container
> dotnet-gcdump report -p [1]

# from local terminal
> docker cp [containerId]:tools/counters.json [.]
```


