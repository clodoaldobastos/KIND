# KIND
https://kind.sigs.k8s.io/

📌 O que é o KIND?

KIND = Kubernetes IN Docker

É uma ferramenta que permite rodar clusters Kubernetes localmente usando containers Docker como se fossem nós (nodes).

🧠 Explicando de forma direta
Ele cria um cluster Kubernetes completo na sua máquina
Cada “node” do cluster é um container Docker
Usa kubeadm por baixo para inicializar o cluster

👉 Ou seja:
Você simula um ambiente Kubernetes real sem precisar de VM, cloud ou infraestrutura pesada.

🏗️ Como funciona na prática
4
Docker roda containers
Cada container = um node (control-plane ou worker)
Dentro deles roda Kubernetes completo
🚀 Para que serve (casos reais)

Use KIND quando você precisa de:

🔧 Desenvolvimento local
🧪 Testes de aplicações Kubernetes
🔄 CI/CD (pipeline automatizado)
🧱 Simular clusters multi-node

Ele foi criado principalmente para testar o próprio Kubernetes, mas é muito usado por devs e DevOps.

On Linux:
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

On macOS:
# For Intel Macs
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-darwin-amd64
# For M1 / ARM Macs
[ $(uname -m) = arm64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.31.0/kind-darwin-arm64
chmod +x ./kind
mv ./kind /some-dir-in-your-PATH/kind

On Windows in PowerShell:
curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.31.0/kind-windows-amd64
Move-Item .\kind-windows-amd64.exe c:\some-dir-in-your-PATH\kind.exe
