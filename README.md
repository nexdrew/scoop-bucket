# scoop-bucket

[Scoop](https://scoop.sh) bucket for [nexdrew](https://github.com/nexdrew) tools.

```powershell
scoop bucket add nexdrew https://github.com/nexdrew/scoop-bucket
scoop install nexdrew/blitzy-cli   # standalone `blitzy` binary, no Node required
```

Manifests here are machine-generated: `bucket/blitzy-cli.json` is rendered from each
release's asset digests by the [blitzy-cli release workflow](https://github.com/nexdrew/blitzy-cli/blob/main/.github/workflows/release.yml)
(`scripts/scoop-manifest.mjs` is the source of truth). Don't edit manifests by hand —
changes belong in the generator.

Every exe the manifests install carries a GitHub build-provenance attestation. Scoop
keeps the downloaded file byte-identical — the `blitzy` command is a shim — so you can
verify the installed binary directly:

```powershell
gh attestation verify "$(scoop prefix blitzy-cli)\blitzy-windows-x64.exe" --repo nexdrew/blitzy-cli
```

(On arm64 Windows, verify `blitzy-windows-arm64.exe` instead.)

The exes are not Authenticode-signed, so SmartScreen may warn on first run; the
attestation above is how to establish trust in what you downloaded.
