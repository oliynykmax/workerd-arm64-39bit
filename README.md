# workerd for arm64 kernels with a 39-bit address space

Upstream workerd links tcmalloc on Linux. tcmalloc assumes a 48-bit virtual address space and aborts on arm64 kernels built with `CONFIG_ARM64_VA_BITS_39`, which includes most Android phones:

```
MmapAligned() failed - unable to allocate with tag ... TCMalloc assumes a 48-bit virtual address space
```

This repository builds the unmodified upstream release tag for linux arm64 with `--@workerd//src/workerd/server:use_tcmalloc=False`, so workerd uses glibc malloc instead. Binaries are published as GitHub releases named after the workerd version.

Use one with wrangler or Miniflare by setting `MINIFLARE_WORKERD_PATH` to the unpacked binary. Its version must match the `workerd` package that your wrangler version installs.

To build another version, run the `build` workflow with that version as input.
