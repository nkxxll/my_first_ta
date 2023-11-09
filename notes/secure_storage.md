# Secure Storage

There are two types of secure storage:

- first is the storage relying on the normal world
- second is the storage relying on the replay protected memory block [see](https://optee.readthedocs.io/en/latest/architecture/secure_storage.html#rpmb)

```
                                            |
                 Normal World               |          Secure World
                                            |
User                                        |          +--+
Space                                       |          |TA|
                                            |          +--+
               +------------------+         |   +-------------------+
           +----   TEE Supplicant ----+     |   |TEE Trusted Storage|
           |   +------------------+   |     |   |Svc. Call          |
           |                          |     |   +-------------------+
          -|--------------------------|-------------------------------------------------
Kernel     |                          |     |   +------------------+
Space      |-------------+  +---------|--+  |   |TEE File Operation|
           | Linux       |  | TEE Driver |  |   |Interface         |
           | File System |  |            |  |   +------------------+
           +-------------+  +------|-----+  |   +------------------------------+
                                   |        |   |TEE File System   +---------+ |
                                   |        |   |                  | Key     | |
                                   |        |   |                  | Manager | |
                                   |        |   |                  +---------+ |
                                   |        |   +------------------------------+
                                   |        |   +----------------------------+
                                   +-------------REE File Operation Interface|
                                            |   +----------------------------+
```

- secure storage is typically stored in /dev/tee/<file number>
