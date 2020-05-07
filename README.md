# Dicas para Copiar / Mover um Repositorio Github

## Importanto AzureDevops(Git) para o Github

Para importar de um repositorio git do Azure Devops basta seguir os passos abaixo:

* No AzureDevops Habilite a "alternate authentication credentials" e especifique um nome de usuário e senha
* No AzureDevops vá para o repositório do seu projeto (Que deseja importar) clique em Clonar para obter a URL HTTPS.
* No repositorio novo criado no Github => Importar repositório
* Digite o URL do repositório (etapa 2)
* Digite as credenciais que você criou (etapa 1) quando solicitar credencial


<img src="https://github.com/nesshub/gitMove/blob/master/Resources/ImportarGithub.png?raw=true" alt="azureDevops" >

É possivel fazer via linha de comando, basta verificar a documentação [clicando aqui](https://help.github.com/en/github/importing-your-projects-to-github/importing-a-git-repository-using-the-command-line)

## Movendo um Repositorio Git para Outro preservando o Historico

