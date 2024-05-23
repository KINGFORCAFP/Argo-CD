Notas:

--> En la ruta cd /home/usuario/.kube se almacenan los config de los cluster que queremos visualizar en el cliente kubectl.

--> Plugins para kubectl se encuentran en esta dirección:
https://krew.sigs.k8s.io/docs/user-guide/setup/install/

--> Para abreviar el comando de mostrar los clusters
instalar kubectl krew install ctx

--> Para abreviar el comando de mostrar los namespace:
instalar namespaces kubectl krew install ns

--> En el archivo ~/.bashrc se debe agregar los siguientes exporta para el funcionamiento del autocompletado en consola:

source /etc/profile.d/bash_completion.sh
export KUBECONFIG=~/.kube/config:~/.kube/config-test.yaml:~/.kube/config-uat.yaml
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
alias kns='kubectl ns'
alias kctx='kubectl ctx'
alias k=kubectl
source <(kubectl completion bash)
complete -o default -F __start_kubectl k

--> Para ver clusters que se tienen con el cliente kubectl se utiliza el comando:
kctx

--> Para obtener los namespaces de un cluster se utiliza el comando:
k get ns

--> Para traer los recursos que tiene un namespaces:
k get all -n nombre_del_namespace

--> Para crear un nuevo contexto de cluster en minikube se utiliza el siguiente comando:
minikube start --kubernetes-version='v1.28.3' \
    --cpus=4 \
    --memory=4096 \
    --addons="metrics-server,default-storageclass,storage-provisioner,ingress,ingress-dns" \
    -p c-pruebas-cafp

--> Para ver los helm de un cluster se usa el comando:
helm repo list

--> El flag w es para ver el log de lo que hace un proceso:
k get pods -n argocd -w

--> Para crear el servicio local de argo cd se utiliza el comando:
kubectl -n argocd port-forward service/argocd-server 8085:443

--> Comando para generar contraseña de argo CD y poder ingresar por la url con el usuario admin:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d