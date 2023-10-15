
# 1. Install Cert Manager Helm Chart  

    helm repo add jetstack https://charts.jetstack.io
    helm repo update

    kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml

    helm upgrade --install cert-manager jetstack/cert-manager --version v1.13.1 --namespace cert-manager --set installCRDs=true

# 2. Configure the ClusterIssuer manifest  

  kubectl apply -f CluserIssuer.yaml

# 3. Install and configure Grafana with Domain and CertManager Config  

    helm upgrade --install grafana prometheus-community/kube-prometheus-stack -n metrics --values grafana-public.yaml