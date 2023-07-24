# Implantação do Aplicativo Node.js no OpenShift

1. Criar um novo aplicativo Node.js a partir do registro de imagens do OpenShift:
   ```bash
   oc new-app --search node
   ```

2. Criar uma nova construção (build) para o aplicativo usando a estratégia Docker e um arquivo binário. Neste caso, a imagem usada será a `node:18-alpine`, e o nome da construção será `nodejs`:
   ```bash
   oc new-build --strategy docker --binary --image node:18-alpine --name nodejs
   ```

3. Iniciar a construção do aplicativo Node.js a partir do diretório atual (onde o código-fonte está localizado) e acompanhar o progresso da construção:
   ```bash
   oc start-build nodejs --from-dir . --follow
   ```

4. Criar um novo aplicativo OpenShift para o aplicativo Node.js recém-construído:
   ```bash
   oc new-app nodejs
   ```

5. Expor o serviço do aplicativo Node.js recém-criado para acesso externo:
   ```bash
   oc expose service/nodejs
   ```

6. Caso seja necessário remover a implantação do aplicativo, o serviço e a rota, você pode executar os seguintes comandos:
   ```bash
   oc delete deployment.apps/nodejs service/nodejs route.route.openshift.io/nodejs
   ```

7. Se desejar limpar também a construção (build) do aplicativo Node.js, utilize o seguinte comando:
   ```bash
   oc delete bc nodejs
   ```
