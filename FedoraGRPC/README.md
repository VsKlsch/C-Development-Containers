 # Fedora + GRPC Development Container
Container contains standart C++ compiler, full grpc with third-party dependencies.

## Using
1. Install docker or Podman
2. Build container
3. Run container
4. Connect to container with exec /bin/bash command or trough VSCode DevContainer

## Environment variables
| Name | Description | Standart Value |
|------|-------------|----------------|
| WORK_USERNAME | Non root user name for regular container using | Developer |
| WORK_USERPASS | Non root password | DeveloperPassword |
| GRPC_RELEASE_TAG | Release tag of used GRPC Version | v1.65.0 |
| GRPC_INSTALL_DIR | Path for installing GRPC Library | /var/local/git/grpc/InstalledGRPC |
| GRPC_INCLUDE_DIR | Path with GRPC and third-party deps includes | $GRPC_INSTALL_DIR/include |