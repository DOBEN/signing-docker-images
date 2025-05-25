### Building, signing and pushing a docker image to GHCR

The repo is set-up with a release pipeline using [github actions](https://github.blog/security/supply-chain-security/safeguard-container-signing-capability-actions/) to build, sign and push a docker image to GHCR.

To trigger the release pipeline, tag the `main` branch with the release version and push the tag:

```
git tag 1.0.0
git push origin 1.0.0
```

This will build, sign and push the docker image to GHCR.

### Verifiying the signature

Run locally:

```
cosign verify ghcr.io/doben/signing-docker-images:1.0.0 --certificate-identity=https://github.com/DOBEN/signing-docker-images/.github/workflows/release.yaml@refs/tags/1.0.0 --certificate-oidc-issuer=https://token.actions.githubusercontent.com
```

The output should be:
```
Verification for ghcr.io/doben/signing-docker-images:1.0.0 --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - The code-signing certificate was verified using trusted certificate authority certificates

[{"critical":{"identity":{"docker-reference":"ghcr.io/doben/signing-docker-images"},"image":{"docker-manifest-digest":"sha256:50c20b6c7b677a066338f3a376d444811b990edfb125212aef1d6d0c6a5e7d8b"},"type":"cosign container image signature"},"optional":
...
```