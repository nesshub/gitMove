# Dicas para Copiar / Mover um Repositorio Git/Github

## Importanto AzureDevops(Git) para o Github

Para importar de um repositorio git do Azure Devops basta seguir os passos abaixo:

* No AzureDevops Habilite a "alternate authentication credentials" e especifique um nome de usuário e senha
* No AzureDevops vá para o repositório do seu projeto (Que deseja importar) clique em Clonar para obter a URL HTTPS.
* No repositorio novo criado no Github => Importar repositório
* Digite o URL do repositório (etapa 2)
* Digite as credenciais que você criou (etapa 1) quando solicitar credencial


<img src="https://github.com/nesshub/gitMove/blob/master/Resources/ImportarGithub.png?raw=true" alt="azureDevops" >

É possivel fazer via linha de comando, basta verificar a documentação [clicando aqui](https://help.github.com/en/github/importing-your-projects-to-github/importing-a-git-repository-using-the-command-line)

## Movendo um Repositorio Git para Outro preservando o Historico (Via linha de Comando)

### Preparando os Arquivos para mover

* Por segurança é bom fazer uma copia do seu repositorio Original (vamos chamar o mesmo de repositorio A). As proximas etapas fazem muitas alterações e não seria bom faazer um push errado.

```bash
mkdir cloneA
cd cloneA
git clone --branch <branch> --origin origin --progress \
  -v <git repository A url>
# eg. git clone --branch master --origin origin --progress \
#   -v https://github.com/username/meuprojeto.git
# (assumindo que meuprojeto é o repositório que você deseja copiar)
```

* Acesse o repositorio criado na sua maquina e evite acidentalmente fazer alterações remotas (por exemplo, enviando um push), exclua o link para o repositório original.

```bash
cd <git repository A directory>
#  eg. cd meuprojeto
# O caminho da pasta seria ~/cloneA/meuprojeto

git remote rm origin
# Após estar na pasta rode o comando acima

```

* Percorra seu histórico e arquivos, removendo qualquer coisa que não esteja em FOLDER_TO_KEEP. 

```bash
git filter-branch --subdirectory-filter <directory> -- --all
# eg. git filter-branch --subdirectory-filter subfolder1/subfolder2/FOLDER_TO_KEEP -- --all

```

* Limpe os dados indesejados

```bash

git reset --hard
git gc --aggressive 
git prune
git clean -fd

```

* Mova todos os arquivos e diretórios para uma nova pasta que você deseja enviar por push para o repositório B.

```bash

mkdir <base directory>
#eg mkdir NovaPasta
mv * <base directory>
#eg mv * NovaPasta

```

Ë possivel fazer via interface caso prefira.

* Para finalizar vamos adicionar as alterações

```bash

git add .
git commit

```

### Fazendo Merge com o Repositorio B

* Caso você não tenha um "Repositorio B" faça.

```bash

mkdir cloneB
cd cloneB
git clone <git repository B url>
# eg. git clone 
https://github.com/username/novoprojeto.git

```

* Acesse o Diretorio e faça uma conexão remota com o Repositorio A

```bash

cd <git repository B directory>
#  eg. cd novoprojeto
# Folder Path is ~/cloneB/novoprojeto

git remote add repo-A <git repository A directory>
# (repo-A pode ser qualquer nome)

# eg. git remote add repo-A ~/cloneA/meuProjeto

```

* De um Push nas branchs que deseja copiar / Mover para o Repositorio B e em seguida remova a conexão com o Repositorio A

```bash

git pull repo-A master --allow-unrelated-histories
# Isto fara o merge do repositorio A para o repositorio B

git remote rm repo-A
# isto remove a conexão com o repositorio A

```

* Para Finalizar Envie um Push

git push

```

Se quiser pode apagar as pastas após o termino. Os Arquivos estrão disponiveis no repositorio B