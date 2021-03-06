# Plugin Application
Create V2O application and automatically serve it.

## Install

Generate gRPC python code
```shell script
python -m grpc_tools.protoc -I . --python_out=. --grpc_python_out=. proto/infer.proto
# copy to runner
cp protos/*.py runner/protos
```

Build auto serving docker image
```shell script
cd runner
docker build -t auto-serve:latest-gpu . -f serve-gpu.Dockerfile
```

## Deploy a self-defined service
```shell script
python container_starter.py <path to service.yml>
```

For example, deploy a simple hello world service.
```shell script
python container_service.py example/hello-world/service.yml
```

## Test

Test gRPC service
```shell script
cd test
python test_grpc.py -p 8000  # gRPC service port, find at service.yml.grpc_port
```

Test HTTP service  
:warning: Currently this does not work
```shell script
cd test
python test_http.py -p 8001 # HTTP service port, find at service.yml.grpc_port
```
