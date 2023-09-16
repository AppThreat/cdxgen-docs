# Getting Started <!-- {docsify-ignore-all} -->

cdxgen is available as an npm package, container image, and single application executables. Begin your journey by selecting your use case.

<!-- tabs:start -->

#### **Generate SBoM for git repos**

## Installation

```shell
sudo npm install -g @cyclonedx/cdxgen

# For CycloneDX 1.4 compatibility use version 8.6.0 or pass the argument `--spec-version 1.4`
sudo npm install -g @cyclonedx/cdxgen@8.6.0
```

If you are a [Homebrew](https://brew.sh/) user, you can also install [cdxgen](https://formulae.brew.sh/formula/cdxgen) via:

```bash
brew install cdxgen
```

## Usage

Minimal example.

```shell
cd <Path to source code>
cdxgen -o bom.json
```

For a java project. This would automatically detect maven, gradle or sbt and build bom accordingly

```shell
cdxgen -t java -o bom.json
```

To print the SBoM as a table pass `-p` argument.

```shell
cdxgen -t java -o bom.json -p
```

To recursively generate a single BoM for all languages pass `-r` argument.

```shell
cdxgen -r -o bom.json
```

To generate SBoM for an older specification version such as 1.4, pass the version using the `--spec-version` argument.

```shell
cdxgen -r -o bom.json --spec-version 1.4
```

To generate SBoM for C or Python, ensure Java >= 17 is installed.

```shell
# Install java >= 17
cdxgen -t c -o bom.json
```

#### **Generate SBoM for container images**

## Installation

```shell
sudo npm install -g @cyclonedx/cdxgen

# For CycloneDX 1.4 compatibility use version 8.6.0 or pass the argument `--spec-version 1.4`
sudo npm install -g @cyclonedx/cdxgen@8.6.0
```

## Usage

`docker` type is automatically detected based on the presence of values such as `sha256` or `docker.io` prefix etc in the path.

```shell
cdxgen odoo@sha256:4e1e147f0e6714e8f8c5806d2b484075b4076ca50490577cdf9162566086d15e -o bom.json
```

You can also pass `-t docker` for simple labels. Only the `latest` tag would be pulled if none was specified.

```shell
cdxgen ghcr.io/owasp-dep-scan/depscan:nightly -o bom.json -t docker
```

You can also pass the .tar file of a container image.

```shell
docker pull ghcr.io/owasp-dep-scan/depscan
docker save -o /tmp/slim.tar ghcr.io/owasp-dep-scan/depscan
podman save -q --format oci-archive -o /tmp/slim.tar ghcr.io/owasp-dep-scan/depscan
cdxgen /tmp/slim.tar -o /tmp/bom.json -t docker
```

### Podman in rootless mode

Setup podman in either [rootless](https://github.com/containers/podman/blob/master/docs/tutorials/rootless_tutorial.md) or [remote](https://github.com/containers/podman/blob/master/docs/tutorials/mac_win_client.md) mode

On Linux, do not forget to start the podman socket which is required for API access.

```bash
systemctl --user enable --now podman.socket
systemctl --user start podman.socket
podman system service -t 0 &
```

#### **Generate OBoM**

<!-- tabs:end -->
