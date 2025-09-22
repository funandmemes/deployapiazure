Deploy de APIs no Azure com Azure Functions

Este guia mostra como criar, configurar e publicar uma API no Azure usando Azure Functions.

Pré-requisitos

Conta no Azure

Azure CLI

Python 3.9+

Azure Functions Core Tools

Passo 1: Criar um Function App local

Abra o terminal.

Crie uma pasta para o projeto e acesse-a:

mkdir minha_api && cd minha_api


Inicialize o projeto Azure Functions com Python:

func init . --python


Crie uma nova função HTTP Trigger:

func new --name minha_funcao --template "HTTP trigger"

Passo 2: Adicionar código da API

Substitua o conteúdo de __init__.py dentro da função pelo código da sua API.

Adicione dependências no requirements.txt se necessário.

Passo 3: Testar localmente
func start


A função será executada em http://localhost:7071/api/minha_funcao.

Teste enviando requisições GET ou POST usando curl ou Postman.

Passo 4: Criar Function App no Azure

Logue na Azure CLI:

az login


Crie um Resource Group:

az group create --name meu_rg --location eastus


Crie o Function App:

az functionapp create \
    --resource-group meu_rg \
    --consumption-plan-location eastus \
    --runtime python \
    --runtime-version 3.9 \
    --functions-version 4 \
    --name nome_unico_da_funcao \
    --storage-account nomeunicoazure

Passo 5: Publicar a função no Azure

No diretório do projeto:

func azure functionapp publish nome_unico_da_funcao


Após o deploy, sua API estará disponível em:

https://nome_unico_da_funcao.azurewebsites.net/api/minha_funcao

Passo 6: Testar a API no Azure

Use curl, Postman ou qualquer cliente HTTP para acessar a URL publicada.

Envie requisições GET ou POST conforme definido na sua função.

Passo 7: Atualizações

Modifique o código localmente.

Publique novamente com:

func azure functionapp publish nome_unico_da_funcao