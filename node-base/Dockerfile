FROM scratch

COPY node.nabla /node.nabla

ENV LKL_BOOT_CMDLINE="mem=255M virtio-pci.force_legacy=1"
ENTRYPOINT ["/node.nabla"]
