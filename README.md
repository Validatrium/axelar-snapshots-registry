# Axelar Snapshots Registry

This repository contains a list of public snapshots for axelar-mainnet (axelar-dojo-1) provided by different validators.

## How to Add Your Snapshot

1. Create a **fork** of this repository.
2. Copy the file `validators/template.json` into a new file `validators/<your-validator-name>.json`
3. Fill in the following fields:
   - `validator`
   - `network name` (mainnet or testnet)
   - `snapshot.block`
   - `snapshot.url`
   - `snapshot.checksum_url`
   - `snapshot.size`
   - `snapshot.compression`
   - `snapshot.updated_at` (UTC, ISO8601 format)

4. Commit your changes `git commit` and `push` them to your fork.
5. Open a **Pull Request** to this repository.

## How to Update Your Snapshot

1. Update the fields in your file `validators/<your-validator-name>.json`:
   - `snapshot.block`
   - `snapshot.url`
   - `snapshot.checksum_url`
   - `snapshot.size`
   - `snapshot.updated_at`
2. Create a new Pull Request with the updated file.

## Snapshot Format

Archives are `tar.zst` containing the **contents** of the axelard `data` directory
(blockstore.db, state.db, application.db, tx_index.db, evidence.db, wasm/, ...).
Extract into your `$AXELAR_HOME/data`:

```bash
aria2c -x 8 -s 8 <snapshot.url>
aria2c -x 8 -s 8 <snapshot.checksum_url>
sha256sum -c <archive>.sha256
tar --use-compress-program="zstd -d -T0" -xf <archive> -C ~/.axelar/data
```
