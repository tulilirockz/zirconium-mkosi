# ParticleOS-based bootc image

THIS IS A WIP - The target is to have [Zirconium](https://github.com/zirconium-dev/zirconium) mostly built off of this (as a POC)

### Building

- `mkosi -f -B` to generate the OCI blobs under `mkosi.output`
- `podman load -i` so you can load that directory as an OCI image
- Edit Containerfile with the hash that you got off of `podman load`
- `podman build --squash-all` with whatever name you'd like your image to have
- `IMAGE_FULL=(image-name) just rootful` then `IMAGE_FULL=(img) just disk-image` to get a bootable disk image off of this

run `mkosi -f -B` to build an oci-dir directory, then `podman load -i mkosi.output/_(numbers)` to load into podman storage

### Known issues

- No rechunker support, this is due to a certain ostree attribute not being there, the rpm-ostree rechunker currently does not read the rpm database off of /usr/lib/sysimage/rpm/ for whatever reason.
- Missing writeable `/var` directories and tmpfiles, these are included in fedora-bootc but not on the upstream bootc packaging on Fedora, we need to port them + add symlinks on `/` for common directories following what roughly Silverblue does
