# 1. Create K3d Minikube Cluster  

If minikube cluster is not present then create it by below commands.

    curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | TAG=v5.3.0 bash
    k3d cluster create mykeptn -p "8082:80@loadbalancer" --k3s-arg "--no-deploy=traefik@server:*"

# 2. Install NGINX Ingress Controller using the below Helm Chart  

  helm upgrade --install ingress-nginx ingress-nginx \
    --repo https://kubernetes.github.io/ingress-nginx \
    --namespace ingress-nginx --create-namespace


# 3. Install Cert Manager Helm Chart  

    helm repo add jetstack https://charts.jetstack.io
    helm repo update

    helm upgrade --install cert-manager jetstack/cert-manager --version v1.13.1 --namespace cert-manager --set installCRDs=true

# 4. Configure the ClusterIssuer manifest  

  kubectl apply -f cluster-issuer.yaml

# 5. Install and configure Grafana with Domain and CertManager Config  

    helm upgrade --install grafana prometheus-community/kube-prometheus-stack -n metrics --values grafana-public.yaml
