FROM quay-proxy.ci.openshift.org/openshift/ci:ocp_builder_rhel-9-golang-1.24-openshift-4.20
WORKDIR /go/src/k8s.io/cloud-provider-openstack
COPY . .
RUN go build -o manila-csi-plugin ./cmd/manila-csi-plugin

FROM quay-proxy.ci.openshift.org/openshift/ci:ocp_4.20_base-rhel9

COPY --from=0 /go/src/k8s.io/cloud-provider-openstack/manila-csi-plugin /usr/bin/

ENTRYPOINT ["/usr/bin/manila-csi-plugin"]
