# Dify-Sandbox
## Requirements

```bash
sudo apt-get install pkg-config libseccomp-dev
```

## Introduction
Dify-Sandbox offers a simple way to run untrusted code in a secure environment. It is designed to be used in a multi-tenant environment, where multiple users can submit code to be executed. The code is executed in a sandboxed environment, which restricts the resources and system calls that the code can access.

## Stack
- **Service**: Gin
- **Library**: Go
- **Sandbox**: Seccomp

## Principle

1. Run `./build/build.sh` to build a Linux native binary file which contains the seccomp filter
2. A temp directory is created for each code execution
3. Launch the code execution in a new process and set a chroot jail to restrict the access to the file system
4. Set the seccomp filter using native library to restrict the system calls that the code can access
5. Drop the privileges of the process to a non-root user which could not access any resource
6. Execute the code and capture the output
