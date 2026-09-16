FROM quay-proxy.ci.openshift.org/openshift/ci:ocp_builder_rhel-9-golang-1.24-openshift-4.20
WORKDIR /go/src/k8s.io/cloud-provider-openstack
COPY . .
RUN go build -o cinder-csi-plugin ./cmd/cinder-csi-plugin

FROM quay-proxy.ci.openshift.org/openshift/ci:ocp_4.20_base-rhel9

# Get mkfs & blkid
RUN yum update -y && \
    yum install --setopt=tsflags=nodocs -y e2fsprogs xfsprogs util-linux systemd-udev && \
    yum clean all && rm -rf /var/cache/yum/*

COPY --from=0 /go/src/k8s.io/cloud-provider-openstack/cinder-csi-plugin /usr/bin/

ENTRYPOINT ["/usr/bin/cinder-csi-plugin"]
