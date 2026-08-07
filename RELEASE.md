# Release Process

This document describes how to cut a release of `cluster-api-provider-nico`.

## Versioning

This project uses [Semantic Versioning](https://semver.org/):

- **MAJOR** — incompatible API or CRD changes that require migration (e.g. removing a field from `NicoCluster.spec`)
- **MINOR** — new backward-compatible features (e.g. new optional spec fields, new CRDs)
- **PATCH** — backward-compatible bug fixes

A **breaking change** is any change that requires users to update their YAML manifests,
credentials Secrets, or `clusterctl` configuration before upgrading.

## Release cadence

Releases are cut on demand. There is no fixed schedule.

## Steps to release

1. **Update `CHANGELOG.md`** — move all `[Unreleased]` entries to a new versioned
   section (e.g. `[0.2.0] - 2026-08-07`) and add a comparison link at the bottom.

2. **Update `metadata.yaml`** if the major or minor version is new, or if the
   Cluster API contract version supported by this release differs from the previous one.

3. **Commit and open a PR** against `main`:
   ```bash
   git commit -s -m "chore: prepare release v<VERSION>"
   ```
   Merge after review.

4. **Tag the release** on the merge commit:
   ```bash
   git tag -s v<VERSION> -m "Release v<VERSION>"
   git push upstream v<VERSION>
   ```

5. **The release workflow fires automatically** on the tag push.
   It creates a GitHub Release with changelog notes extracted from `CHANGELOG.md`.

6. **Verify** at `https://github.com/NVIDIA/cluster-api-provider-nico/releases`.

## Backport policy

Only critical security fixes are backported. All other fixes target `main`.

## Who can release

Any [maintainer](MAINTAINERS.md) may cut a release.
