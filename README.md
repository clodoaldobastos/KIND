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
