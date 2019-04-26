# Zulu OpenJDK on Alpine with Payara Micro

Custom Docker images that combine Zulu OpenJDK on Alpine with Payara Micro. The images are published on Docker Hub here: https://hub.docker.com/r/qaware/zulu-alpine-payara-micro/

All the images are tuned for Docker usage, especially concerning the CPU, RAM and thus JVM heap usage.
```
docker run -it --rm --cpus 1 --memory 640m qaware/zulu-alpine-payara-micro:8u212-5.191
```

# Maintainer

M.-Leander Reimer (@lreimer), <mario-leander.reimer@qaware.de>

# License

This software is provided under the MIT open source license, read the `LICENSE` file for details.
