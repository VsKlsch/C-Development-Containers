 # Fedora + GRPC Development Container
Container contains standart C++ compiler and installed vcpkg for future development.

## Using
1. Install docker or Podman
2. Build container
3. Run container  
`docker run -d fedoravcpkg /bin/bash -c "sleep infinity" ` 
4. Connect to container with exec /bin/bash command or trough VSCode DevContainer

## Environment variables
| Name | Description | Standart Value |
|------|-------------|----------------|
| WORK_USERNAME | Non root user name for regular container using | developer |
| WORK_USERPASS | Non root password | developer |