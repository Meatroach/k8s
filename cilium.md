## install cilium

# install crds

kubectl get crd \
  gateways.gateway.networking.k8s.io \
  httproutes.gateway.networking.k8s.io

  # install cilium (helm alternative via cilium cli)
  quelle: https://docs.siderolabs.com/kubernetes-guides/cni/deploying-cilium#without-kube-proxy-7

  

cilium install \
    --set ipam.mode=kubernetes \
    --set kubeProxyReplacement=true \
    --set securityContext.capabilities.ciliumAgent="{CHOWN,KILL,NET_ADMIN,NET_RAW,IPC_LOCK,SYS_ADMIN,SYS_RESOURCE,DAC_OVERRIDE,FOWNER,SETGID,SETUID}" \
    --set securityContext.capabilities.cleanCiliumState="{NET_ADMIN,SYS_ADMIN,SYS_RESOURCE}" \
    --set cgroup.autoMount.enabled=false \
    --set cgroup.hostRoot=/sys/fs/cgroup \
    --set k8sServiceHost=localhost \
    --set k8sServicePort=7445

  # install cilium with helm // datt mit der version hat aber nicht geklappt, die musste ich raus nehmen

  helm install cilium oci://quay.io/cilium/charts/cilium \
  1.20.1 \
  --namespace kube-system



# Troubleshoot


CoreDNS not working with forwardKubeDNSToHost and bpf.masquerade: When using Talos forwardKubeDNSToHost=true (enabled by default) together with Cilium bpf.masquerade=true, CoreDNS may not work correctly. Setting forwardKubeDNSToHost=false resolves the issue. See the discussion here for more context.