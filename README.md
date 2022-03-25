# bazel-alpine-package

This is the Bazel 2.2.0 as a Alpine Linux package.

## Installing

The current installation method for these packages is to pull them in using `wget` or `curl` and install the local file with `apk`:

    apk --no-cache add ca-certificates wget
    wget -q -O /etc/apk/keys/maskndafi@tesla.com-623a4a11.rsa.pub https://github.com/MikeDafi/bazel-alpine-package/blob/master/maskndafi%40tesla.com-623a4a11.rsa.pub
    wget https://github.com/MikeDafi/bazel-alpine-package/releases/download/2.2.0/bazel-2.2.0-r0.apk
    apk add bazel-2.2.0-r0.apk

## Usage inside a Dockerfile

    ADD https://github.com/MikeDafi/bazel-alpine-package/blob/master/maskndafi%40tesla.com-623a4a11.rsa.pub \
        /etc/apk/keys/maskndafi@tesla.com-623a4a11.rsa.pub
    ADD https://github.com/MikeDafi/bazel-alpine-package/releases/download/2.2.0/bazel-2.2.0-r0.apk \
        /tmp/bazel-2.2.0-r0.apk
    RUN apk add /tmp/bazel-2.2.0-r0.apk
