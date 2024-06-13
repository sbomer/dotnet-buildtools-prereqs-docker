FROM mcr.microsoft.com/dotnet-buildtools/prereqs:azurelinux-3.0-crossdeps-builder-net9.0-local as builder
ARG ROOTFS_DIR=/crossrootfs/riscv64

# debootstrap from Azure Linux sources doesn't yet support Ubuntu 24.04,
# so get latest debootstrap from Ubuntu sources
RUN git clone --depth 1 https://git.launchpad.net/ubuntu/+source/debootstrap /debootstrap && \
    chmod a+x /debootstrap/debootstrap && \
    ln -s /debootstrap/debootstrap -t /usr/local/bin

RUN /scripts/eng/common/cross/build-rootfs.sh riscv64 noble --skipunmount

FROM mcr.microsoft.com/dotnet-buildtools/prereqs:azurelinux-3.0-crossdeps-llvm-net9.0-local
ARG ROOTFS_DIR=/crossrootfs/riscv64

COPY --from=builder $ROOTFS_DIR $ROOTFS_DIR
