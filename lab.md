⚙️ 1. Pré-requisitos

Instale:

# Docker
sudo apt install docker.io -y

# kubectl
curl -LO https://dl.k8s.io/release/v1.29.0/bin/linux/amd64/kubectl
chmod +x kubectl && sudo mv kubectl /usr/local/bin/

# kind
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-amd64
chmod +x kind && sudo mv kind /usr/local/bin/

# istioctl
curl -L https://istio.io/downloadIstio | sh -
cd istio-*/bin
sudo mv istioctl /usr/local/bin/
🧩 2. Criar cluster KIND (multi-node)

Crie o arquivo:

# kind-cluster.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4

nodes:
- role: control-plane
- role: worker
- role: worker

Suba:

kind create cluster --name lab-istio --config kind-cluster.yaml
🔌 3. Instalar Istio (modo produção simplificado)
istioctl install --set profile=demo -y

Verifique:

kubectl get pods -n istio-system
🔐 4. Ativar mTLS (importante)
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1
kind: PeerAuthentication
metadata:
  name: default
  namespace: default
spec:
  mtls:
    mode: STRICT
EOF
🚀 5. Deploy app de teste (com sidecar Envoy)
kubectl create namespace app
kubectl label namespace app istio-injection=enabled
httpbin
kubectl apply -n app -f https://raw.githubusercontent.com/istio/istio/release-1.20/samples/httpbin/httpbin.yaml
curl (cliente)
kubectl apply -n app -f https://raw.githubusercontent.com/istio/istio/release-1.20/samples/curl/curl.yaml
🔍 6. Testar comunicação via Envoy
kubectl exec -n app deploy/curl -c curl -- \
  curl http://httpbin:8000/get

👉 Isso já passa pelo Envoy sidecar + mTLS automático

🔎 7. Ver tráfego no Istio
istioctl proxy-status
kubectl logs -n app deploy/httpbin -c istio-proxy
🌐 8. (Opcional) Expor via Gateway

Se quiser simular algo parecido com AKS ingress:

kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.20/samples/httpbin/httpbin-gateway.yaml

Port-forward:

kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80

Teste:

curl http://localhost:8080/get
