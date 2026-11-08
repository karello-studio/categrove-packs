# categrove-packs

Release assets for the Categrove app: encrypted word packs and a signed
manifest. The app downloads them; nothing here is meant for people to use
directly.

This repository is not a data source. The packs are encrypted, and hosting them
here grants no license to them or to the data inside. No license file is
included on purpose: all rights reserved, Karello Studio.

## Stable URLs

The latest release always serves:

- https://github.com/karello-studio/categrove-packs/releases/latest/download/manifest.json
- https://github.com/karello-studio/categrove-packs/releases/latest/download/manifest.sig
- https://github.com/karello-studio/categrove-packs/releases/latest/download/en.fst.gz

Each release is named by a CalVer string (`YYYY.MM.N`), which is also the
manifest's `version`.

## manifest.json

```json
{
  "schema": 1,
  "version": "2026.11.0",
  "packs": [
    { "id": "en", "lang": "en", "file": "en.fst.gz",
      "sha256": "<hex SHA-256 of the encrypted file>", "size": 597806,
      "plain_size": 946418, "cipher": "aes-256-gcm-stream",
      "format": 1, "normalizer": 1, "paid": false }
  ]
}
```

- `sha256`, `size`: of the file as downloaded (encrypted).
- `plain_size`: bytes of the installed store after decrypting and unzipping.
- `cipher`: AES-256-GCM in the STREAM construction, 1 MiB segments.
- `format`, `normalizer`: the store format and normalizer versions; an app
  installs only packs it can read.

## manifest.sig

One line per signature over the exact bytes of `manifest.json`:

```
ed25519 <hex signature>
```

Apps check the `ed25519` line and skip algorithms they do not know, so another
signature can be added beside it later. The Ed25519 public key:

```
6db898b191bb26960197b9fc72d51692febf413e6e28aaaa1f4e45c27dcaf128
```
