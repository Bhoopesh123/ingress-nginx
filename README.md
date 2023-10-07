
# 1. Create K3d Minikube Cluster  

If minikube cluster is not present then create it by below commands.

    curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | TAG=v5.3.0 bash
    k3d cluster create mykeptn -p "8082:80@loadbalancer" --k3s-arg "--no-deploy=traefik@server:*"

# 2. Install NGINX Ingress Controller using the below Helm Chart  

  helm upgrade --install ingress-nginx ingress-nginx \
    --repo https://kubernetes.github.io/ingress-nginx \
    --namespace ingress-nginx --create-namespace

# 3. Install and configure First Demo Application

    kubectl apply -f deployment1.yml

# 4. Create Ingress rule for Traffic Routing

    kubectl apply -f ingress1.yml

# 5. Install and configure Second Demo Application

    kubectl apply -f deployment2.yml
    kubectl apply -f deployment3.yml
    kubectl apply -f ingress2.yml

# 6. Install and configure Third Demo Application

    kubectl apply -f deployment4.yml
    kubectl apply -f ingress3.yml