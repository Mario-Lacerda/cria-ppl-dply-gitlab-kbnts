## Desafio Dio -  Criando um Pipeline de Deploy com GitLab e Kubernetes



**Criando um arquivo de configuração do GitLab CI/CD para o projeto Criando um Pipeline de Deploy com GitLab e Kubernetes:**

yaml

```yaml
image: docker:latest

stages:
  - build
  - deploy

build:
  stage: build
  script:
    - docker build -t my-app .

deploy:
  stage: deploy
  script:
    - kubectl apply -f deployment.yaml
```



### **Observações 1:**

- A imagem `docker:latest` é usada para executar os estágios de build e deploy.
- O estágio `build` cria uma imagem Docker para o aplicativo.
- O estágio `deploy` implanta a imagem Docker no Kubernetes usando o arquivo de configuração `deployment.yaml`.



#### **Para juntar os programas e códigos em um único projeto:**

1. Crie um novo projeto no GitLab.
2. Crie um arquivo Dockerfile para o seu aplicativo.
3. Crie um arquivo de configuração do GitLab CI/CD.
4. Adicione seus programas e códigos ao repositório do projeto.
5. Execute o pipeline do GitLab CI/CD para construir e implantar seu aplicativo.



### **Observações 2:**

- O arquivo Dockerfile deve estar localizado no diretório raiz do seu projeto.
- O arquivo de configuração do GitLab CI/CD deve ser nomeado `.gitlab-ci.yml` e deve estar localizado no diretório raiz do seu projeto.
- Você pode usar o comando `git push` para enviar seu projeto para o GitLab.
- Você pode usar o comando `gitlab-ci-runner register` para registrar um runner do GitLab CI/CD.
- Você pode usar o comando `gitlab-ci-runner run` para executar o pipeline do GitLab CI/CD.





Para criar um pipeline de deploy de uma aplicação utilizando Docker e Kubernetes no Google Cloud Platform (GCP), podemos seguir estes passos gerais:

1. #### **Prepare a Aplicação**:

   - Certifique-se de que sua aplicação está pronta para ser containerizada com Docker.

   - Crie um `Dockerfile` que define como a imagem do Docker da sua aplicação será construída.

     

2. #### **Construa a Imagem Docker**:

   - Utilize o comando `docker build` para construir a imagem da sua aplicação.

   - Após a construção, envie a imagem para um registro de container, como o Google Container Registry (GCR).

     

3. #### **Configure o Kubernetes**:

   - Instale e configure o `kubectl`, a ferramenta de linha de comando do Kubernetes.

   - Crie os arquivos de configuração do Kubernetes, como `deployments`, `services`, e `ingress`, que definirão como sua aplicação será executada no cluster.

     

4. #### **Crie o Pipeline de CI/CD**:

   - Configure um sistema de integração e entrega contínua (CI/CD) para automatizar o processo de deploy.

   - Ferramentas como GitHub Actions, GitLab CI ou Jenkins podem ser usadas para criar pipelines que automatizam testes, construção de imagens Docker e deployment no Kubernetes.

     

5. #### **Deploy no GCP**:

   - Utilize o GCP para provisionar um cluster Kubernetes.

   - Configure o pipeline para realizar o deploy da imagem Docker no cluster Kubernetes do GCP.

     

6. #### **Monitore e Atualize**:

   - Após o deploy, monitore o desempenho e a saúde da sua aplicação.

   - Configure o pipeline para atualizações automáticas ou promova atualizações manualmente quando necessário.

     

Lembre-se de configurar adequadamente as permissões e variáveis de ambiente sensíveis, utilizando recursos como Secrets do Kubernetes e do provedor de CI/CD escolhido.

Para um guia mais detalhado, você pode consultar recursos e tutoriais específicos para o GCP e Kubernetes, ou até mesmo explorar repositórios no GitHub que demonstram pipelines de deploy configurados para esse ambiente³⁴. Esses recursos podem oferecer exemplos práticos e configurações que você pode adaptar para o seu projeto.



Aqui está um exemplo prático de como criar um pipeline de deploy para uma aplicação utilizando Docker e Kubernetes no Google Cloud Platform (GCP):



```
# Exemplo de Dockerfile para a aplicação
FROM node:14
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 8080
CMD ["node", "server.js"]

# Comandos para construir e enviar a imagem Docker
docker build -t gcr.io/SEU_PROJETO/minha-aplicacao:v1 .
docker push gcr.io/SEU_PROJETO/minha-aplicacao:v1

# Exemplo de arquivo deployment.yaml para Kubernetes
apiVersion: apps/v1
kind: Deployment
metadata:
  name: minha-aplicacao
spec:
  replicas: 3
  selector:
    matchLabels:
      app: minha-aplicacao
  template:
    metadata:
      labels:
        app: minha-aplicacao
    spec:
      containers:
      - name: minha-aplicacao
        image: gcr.io/SEU_PROJETO/minha-aplicacao:v1
        ports:
        - containerPort: 8080

# Comandos para criar o cluster e fazer o deploy
gcloud container clusters create meu-cluster
kubectl apply -f deployment.yaml
```



Este é um exemplo simplificado. No seu pipeline de CI/CD, você terá etapas adicionais para testar a aplicação, construir a imagem Docker apenas se os testes passarem, e atualizar o deployment no Kubernetes automaticamente com a nova imagem.

Para um guia passo a passo, você pode consultar o tutorial do Google Cloud que mostra como empacotar uma aplicação web em uma imagem de container Docker e executá-la em um cluster do Google Kubernetes Engine (GKE), gerenciar o autoescalonamento para o deployment e expor a aplicação na internet¹.

Além disso, há um artigo no Medium que detalha a construção e o deploy de uma imagem Docker para um cluster Kubernetes do GCP com um pipeline Jenkins². Este artigo pode ser útil para entender como integrar ferramentas de CI/CD como Jenkins no processo de deploy.
