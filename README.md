Experimenting with signing of docker images and pushing them to GHCR with github actions.

Verifying the signature locally:

```
cosign verify ghcr.io/doben/signing-docker-images@sha256:93972dded0f839027b13b7e11ec91b1144acd8d7dfb3925326d8896131d83ac1 --certificate-identity=https://github.com/DOBEN/signing-docker-images/.github/workflows/release.yaml@refs/tags/1.0.0 --certificate-oidc-issuer=https://token.actions.githubusercontent.com
```

docker pull ghcr.io/doben/signing-docker-images:sha256-93972dded0f839027b13b7e11ec91b1144acd8d7dfb3925326d8896131d83ac1.sig

The output should be:
```
Verification for ghcr.io/doben/signing-docker-images@sha256:8254aa7ef22836f131f6d6419b913e349dad6d4281a3f552243197f7121acc04 --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - The code-signing certificate was verified using trusted certificate authority certificates

[{"critical":{"identity":{"docker-reference":"ghcr.io/doben/signing-docker-images"},"image":{"docker-manifest-digest":"sha256:8254aa7ef22836f131f6d6419b913e349dad6d4281a3f552243197f7121acc04"},"type":"cosign container image signature"},"optional":{"1.3.6.1.4.1.57264.1.1":"https://token.actions.githubusercontent.com","1.3.6.1.4.1.57264.1.2":"push","1.3.6.1.4.1.57264.1.3":"7439fa44fca47d
...
```