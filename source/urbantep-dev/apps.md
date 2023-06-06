# Installed applications and tools

The Urban TEP processor development VM comes with a few pre-installed processor development tools. In the first version these are:

- Sentinel Toolbox SNAP
- Matlab runtime environment
- Urban-TEP processor packaging and upload support tools
- Docker build and run tools

The applications are located in directory /urbantep/software/\<package> in the virtual machine:

```
urbanuser@urbandev:~ $ tree -L 2 /urbantep/software
/urbantep/software
├── snap-3.0.1
│   ├── bin
│   ├── snap
│   ├── s1tbx
│   ├── s2tbx
│   ├── s3tbx
│   ├── ...
│   └── LICENSE.txt
├── mcr_root-v81
│   ├── bin
│   ├── etc
│   ├── mcr_root
│   ├── ...
│   ├── license.txt
│   └── MCR_license.txt
└── urbantep-dev
    ├── bin
    ├── etc
    └── example
```

Additional tools can be installed in standard places (e.g. /usr/local or /opt). If they are required at runtime by the processor the runtime parts of them must be packaged and maybe mounted into the docker container like the processor software itself, as explained later in this chapter.
