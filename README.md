# desafio-eks

Dentro do repositorio, execute:

    terraform init

    terraform plan

    terraform apply

Em seguida,configure o kubectl para interagir com o cluster:

    aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)

Verifique o status dos componentes:

    kubectl get cs

Verifique que o usuario desafio_aquarela foi adicionado ao configmap aws-auth:

    kubectl get configmaps aws-auth -n kube-system -o yaml   

Realize o deployment da aplicação:

    kubectl apply -f complete-demo.yaml
    

Obs. O serviço frontend foi alterado para o tipo LoadBalancer.

Aguarde todos os recursos do namespace sock-shop ficarem prontos
    
    kubectl get all -n sock-shop 

Após ficarem prontos, execute o comando para verificar endereço externo.

    kubectl -n sock-shop get svc front-end -o json | jq -r .status.loadBalancer.ingress[].hostname

Copie o endereço e insira em um navegador para acesso à aplicação.
