# Configuação de servidor para instalação do orquestrador (Jenkins)

## Pré-requisitos

Requisitos mínimos de hardware:

256MB de RAM

1 GB de espaço em disco (embora 10 GB seja o mínimo recomendado se estiver executando o Jenkins como um contêiner do Docker)

Configuração de hardware recomendada para uma equipe pequena:

4 GB+ de RAM

50 GB+ de espaço em disco


Primeiro, você precisa instalar o Jenkins. Normalmente, isso é feito usando um programa de gerenciamento de pacotes como o apt-get ou yum, dependendo do sistema operacional da sua empresa. Em seguida, você precisará configurar o servidor Jenkins para acessar os seus repositórios de código. Por fim, você precisará configurar o Jenkins para que seja executado automaticamente toda vez que o servidor for reiniciado.


A documentação oficial para configuração está no site do jenkins para instalação no sistema operacional Windons, Linux, Mac OS.

https://www.jenkins.io/doc/book/installing/windows/



###########################################################################################################



>## Para ter acesso ao portal do jenkins já instalado. 

![image](https://user-images.githubusercontent.com/84463038/224710651-fee1d4a5-8ae9-494b-8d2d-b4ebd7d3edd3.png)


Ao instalar um serviço para ser executado em uma conta de usuário de domínio, a conta deve ter o direito de fazer login como um serviço. Essa permissão de login se aplica estritamente ao computador local e deve ser concedida na Diretiva de Segurança Local.

Execute as seguintes etapas abaixo para editar a política de segurança local do computador no qual deseja definir a permissão 'logon as a service':


1. Faça logon no computador com privilégios administrativos.

2. Abra as Ferramentas Administrativas e abra a Política de Segurança Local

3. Se a Política de segurança local estiver ausente em seu sistema, consulte a resposta em Onde baixar o GPEdit.msc para Windows 10 Home? pergunta no Microsoft Community para solucionar problemas

4. Expanda Política local e clique em Atribuição de direitos do usuário

5. No painel direito, clique com o botão direito do mouse em Fazer logon como um serviço e selecione Propriedades.

6. Clique no botão Adicionar usuário ou grupo… para adicionar o novo usuário.

7. Na caixa de diálogo Selecionar usuários ou grupos , localize o usuário que deseja inserir e clique em OK

8.Clique em OK nas Propriedades de logon como um serviço para salvar as alterações.

> Depois de concluir as etapas acima, tente fazer login novamente com o usuário adicionado.

Outro ponto a ser levado em conta seria a transformação do  seu projeto em um site, você precisará criar um servidor web e publicar seu conteúdo nele. Existem vários serviços que você pode usar para hospedar seu conteúdo, incluindo serviços de hospedagem compartilhada e VPSs. Após configurar o servidor web adequadamente, você também precisará escolher um sistema de gerenciamento de conteúdo (CMS) para exibir seu conteúdo. Você também precisará configurar o DNS corretamente para apontar o domínio para seu site.

##########################################################################################################

# Configuração Jenkins com o Github. 

- Para configurar o Jenkins com o GitHub, você precisa primeiro criar um projeto Jenkins e adicionar uma fonte de código do GitHub. Para isso, faça login no servidor Jenkins e vá para a página de configuração do projeto. Em seguida, clique em "Adicionar Fonte de Código" e selecione o repositório do GitHub que deseja usar. Depois disso, você pode configurar as etapas necessárias para executar a compilação, testes e implantação do código.
# Configuração das credenciais 


- Umas das tarefas mais importantes da configuração de um pipeline funcional, será essa etapa de ajustes das credenciais, pois será de suma importancia para a execução do mesmo. 

    > As credenciais armazenadas no Jenkins podem ser usadas:

- Em qualquer lugar aplicável em Jenkins (ou seja, credenciais globais),
- Por um projeto/item específico do Pipeline (leia mais sobre isso na seção Manipulando credenciais de Usando um Jenkinsfile ),
- Por um usuário Jenkins específico (como é o caso de projetos Pipeline criados em Blue Ocean ).

    > Jenkins pode armazenar os seguintes tipos de credenciais:

- Texto secreto - um token como um token de API (por exemplo, um token de acesso pessoal do GitHub),
- Nome de usuário e senha - que podem ser tratados como componentes separados ou como uma string separada por dois pontos no formato username:password(leia mais sobre isso em Manuseio de credenciais ),
- Arquivo secreto - que é essencialmente conteúdo secreto em um arquivo,
- Nome de usuário SSH com chave privada - um par de chaves públicas/privadas SSH ,
- Certificado - um arquivo de certificado PKCS#12 e senha opcional, ou
- Credenciais de autenticação de certificado de host do Docker .


# Segurança de credenciais

- Para maximizar a segurança, as credenciais configuradas no Jenkins são armazenadas de forma criptografada na instância do Jenkins do controlador (criptografadas pelo ID da instância do Jenkins) e são tratadas apenas nos projetos do Pipeline por meio de seus IDs de credencial.
Isso minimiza as chances de expor as próprias credenciais reais aos usuários do Jenkins e dificulta a capacidade de copiar as credenciais funcionais de uma instância do Jenkins para outra.

### Configurando credenciais

Esta seção descreve os procedimentos para configurar credenciais no Jenkins.

As credenciais podem ser adicionadas ao Jenkins por qualquer usuário do Jenkins que tenha a permissão Credentials > Create (definida por meio de Matrix-based security ). Essas permissões podem ser configuradas por um usuário Jenkins com a permissão Administrar . Leia mais sobre isso na seção Autorização de Gerenciando a segurança .

Caso contrário, qualquer usuário do Jenkins pode adicionar e configurar credenciais se as configurações de autorização da página Configurar configurações de segurança global da sua instância do Jenkins estiverem definidas como a configuração padrão Usuários conectados podem fazer qualquer coisa ou Qualquer pessoa pode fazer qualquer coisa .

### Adicionando novas credenciais globais

Para adicionar novas credenciais globais à sua instância do Jenkins:

1. Se necessário, verifique se você está conectado ao Jenkins (como um usuário com a permissão Credenciais > Criar ).

2. Na página inicial do Jenkins (ou seja, o Painel da IU clássica do Jenkins), clique em Gerenciar Jenkins > Gerenciar credenciais .

![image](https://user-images.githubusercontent.com/84463038/224713972-069eb303-539f-4dca-ad66-3ed0ffc96956.png)

3. Em Stores com escopo para Jenkins à direita, clique em Jenkins. 


![image](https://user-images.githubusercontent.com/84463038/224714227-5379c260-a36c-495e-aae6-cfb1ac949f01.png)

4. Em Sistema , clique no link Credenciais globais (sem restrições) para acessar esse domínio padrão.

![image](https://user-images.githubusercontent.com/84463038/224714396-355362b5-e093-4bba-876f-5b33f07bc3b2.png)

5. Clique em Adicionar credenciais à esquerda.
Observação: se não houver credenciais nesse domínio padrão, você também pode clicar no link adicionar algumas credenciais (que é o mesmo que clicar no link Adicionar credenciais ).

6. No campo Tipo , escolha o tipo de credencial a ser adicionado.

https://www.jenkins.io/doc/book/using/using-credentials/#types-of-credentials

7.No campo Escopo , escolha:

- Global - se a(s) credencial(is) a ser(em) adicionada(s) for(em) para um projeto/item Pipeline. Escolher esta opção aplica o escopo da(s) credencial(is) ao "objeto" do projeto/item Pipeline e a todos os seus objetos descendentes.

- Sistema - se a(s) credencial(is) a ser(em) adicionada(s) é(são) para a própria instância do Jenkins interagir com as funções de administração do sistema, como autenticação de e-mail, conexão do agente, etc. Escolher esta opção aplica o escopo da(s) credencial(is) a um único objeto apenas.

8. Adicione as próprias credenciais nos campos apropriados para o tipo de credencial escolhido:

- Texto secreto - copie o texto secreto e cole-o no campo Segredo .

- Nome de usuário e senha - especifique o nome de usuário e a senha da credencial em seus respectivos campos.

- Arquivo secreto - clique no botão Escolher arquivo ao lado do campo Arquivo para selecionar o arquivo secreto a ser carregado no Jenkins.

- Nome de usuário SSH com chave privada - especifique as credenciais Nome de usuário , Chave privada e Senha opcional em seus respectivos campos.
Observação: Escolher Enter diretamente permite copiar o texto da chave privada e colá-lo na caixa de texto Chave resultante .

- Certificado —especifique o Certificado e a Senha opcional . Escolher Carregar certificado PKCS#12 permite carregar o certificado como um arquivo por meio do botão Carregar certificado resultante .

- Docker Host Certificate Authentication - copie e cole os detalhes apropriados nos campos Client Key , Client Certificate e Server CA Certificate .

9. No campo ID , especifique um valor de ID de credencial significativo - por exemplo, jenkins-user-for-xyz-artifact-repository. O provedor de credenciais embutido (padrão) pode usar letras maiúsculas ou minúsculas para o ID da credencial, bem como qualquer caractere separador válido; outros provedores de credenciais podem aplicar outras restrições aos caracteres ou comprimentos permitidos. No entanto, para o benefício de todos os usuários em sua instância do Jenkins, é melhor usar uma convenção única e consistente para especificar IDs de credenciais.
Nota: Este campo é opcional. Se você não especificar seu valor, Jenkins atribuirá um valor de ID globalmente exclusivo (GUID) para o ID de credencial. Lembre-se de que, uma vez definido um ID de credencial, ele não poderá mais ser alterado.

10. Especifique uma Descrição opcional para a(s) credencial(is).

11. Clique em OK para salvar as credenciais.


##########################################################################################################

# Conceito básico de pipeline:

Jenkins é, fundamentalmente, um mecanismo de automação que suporta vários padrões de automação. O Pipeline adiciona um poderoso conjunto de ferramentas de automação ao Jenkins, suportando casos de uso que vão desde integração contínua simples até pipelines de CD abrangentes. Ao modelar uma série de tarefas relacionadas, os usuários podem aproveitar os diversos recursos do Pipeline:

> Código : os pipelines são implementados em código e normalmente verificados no controle de origem, dando às equipes a capacidade de editar, revisar e iterar em seu pipeline de entrega.

> urável : os pipelines podem sobreviver a reinicializações planejadas e não planejadas do controlador Jenkins.

> Pausável : os pipelines podem, opcionalmente, parar e aguardar entrada ou aprovação humana antes de continuar a execução do pipeline.

> Versátil : os pipelines suportam requisitos complexos de CD do mundo real, incluindo a capacidade de bifurcar/juntar, fazer loop e realizar trabalho em paralelo.

> Extensível : O plugin Pipeline suporta extensões customizadas para seu DSL [ 1 ] e múltiplas opções de integração com outros plugins.

Embora Jenkins sempre tenha permitido formas rudimentares de encadear trabalhos Freestyle para executar tarefas sequenciais, [ 4 ] Pipeline torna esse conceito um cidadão de primeira classe em Jenkins.


## Fundamentos do pipeline na forma declarativa

- Na sintaxe declarativa do Pipeline, o pipelinebloco define todo o trabalho feito em todo o seu Pipeline utilizando o JenkinsFile.

pipeline {
    agent any - 1
    stages {
        stage('Build') { - 2
            steps {
                // 3
            }
        }
        stage('Test') { 4
            steps {
                // 5
            }
        }
        stage('Deploy') { 6
            steps {
                // 7
            }
        }
    }
}

1.Execute este Pipeline ou qualquer uma de suas etapas, em qualquer agente disponível.
2.Define a etapa "Build".
3.Execute algumas etapas relacionadas ao estágio "Build".
4.Define a etapa "Teste".
5.Execute algumas etapas relacionadas ao estágio "Teste".
6.Define o estágio "Deploy".
7.Execute algumas etapas relacionadas ao estágio "Deploy".

## Fundamentos do pipeline com Scrit:

Na sintaxe do pipeline com script, um ou mais nodeblocos fazem o trabalho principal em todo o pipeline. Embora esse não seja um requisito obrigatório da sintaxe do Pipeline com script, confinar o trabalho do seu Pipeline dentro de um node bloco resulta em duas coisas:

1. Agenda as etapas contidas no bloco para serem executadas adicionando um item à fila do Jenkins. Assim que um executor estiver livre em um nó, as etapas serão executadas.

2.Cria um espaço de trabalho (um diretório específico para esse Pipeline específico) onde o trabalho pode ser feito em arquivos com check-out do controle de origem.
Cuidado: Dependendo da configuração do Jenkins, alguns espaços de trabalho podem não ser limpos automaticamente após um período de inatividade. Veja os tickets e a discussão no link de JENKINS-2111 para mais informações.

## Exemplo de pipeline

1. Pipelineé a sintaxe específica do Pipeline Declarativo que define um "bloco" contendo todo o conteúdo e instruções para executar todo o Pipeline.

2. Agent é a sintaxe específica do pipeline declarativo que instrui o Jenkins a alocar um executor (em um nó) e espaço de trabalho para todo o pipeline.

3. Stage é um bloco de sintaxe que descreve um estágio deste Pipeline. Leia mais sobre stageblocos na sintaxe de pipeline declarativa na página de sintaxe de pipeline  Conforme mencionado acima , stageos blocos são opcionais na sintaxe do Scripted Pipeline.

4. Steps é a sintaxe específica do pipeline declarativo que descreve as etapas a serem executadas neste stage.
 
5.Sh é uma etapa do Pipeline (fornecida pelo plugin Pipeline: Nodes and Processes ) que executa o comando shell fornecido.



####################################################################################################





####################################################################################################

## Configuração do Pipeline

- Primeiro passo será a configuração da configuração do Github com o Jenkins utilizando o "List Git branches 99 (and more)"

- Configurado o paramentro de comunicação do github, agora utilizaremos o paramentro de verificação de acesso, caso o jenkins seja configurado com usuario defaut, esse passo não será utilizado. Caso tenha necessite de acesso, será utilizado o paramentro User e Senha.

- Pipeline 
Será feito no modo de script na forma pipeline declarativo.
O arquivo de configuração do pipeline e todos os seus passos, estará disponivel no repositorio do CI/CD para melhor organização. 

# **Explicação passo a passo do pipeline**

***1. Primeiro passo do Pipline.*** 
 
    pipeline {
    agent any
    environment {
        SERVER  = 'nome do servidor'
    }
   Esse primeiro Step será reponsável por determinar qual o servidor que será utilizado.
   Basta colocar o nome do servidor que irá ser utilizado  na variavel **SERVER** entre aspas simples.
  
  ***2. Segundo passo do Pipline.***
  ```
  stages {
        stage('Clone Repository') {
            steps {
                git url: 'Link do seu repositorio no git',
                    credentialsId: "seu credentialsID",
                    branch: ("${env.BRANCH}".split("/").length > 3 ? "${env.BRANCH}".split("/")[2] + "/" + "${env.BRANCH}".split("/")[3] : "${env.BRANCH}".split("/")[2])
            }
        }
   ```
   
   Esse seundo passo será reponsável por  selecionar e clonar o seu repositorio, coloque o link do seu git e credentialsId entre aspas simples.
   
   ***3. Terceiro passo do Pipline.***
```
   stage ("Install Packages with Yarn") {
            steps {
                powershell script: """
                    \$ErrorActionPreference = 'Stop'
                    yarn
                """
            }
        } 
 ```    
  Esse Terceiro passo será reponsável por baixar os pacotes do Yarn e instalar o mesmo.
  
  ***4. Quarto passo do Pipline.***
```
stage ("Build Application with Yarn") {
            steps {
                powershell script: """
                    \$ErrorActionPreference = 'Stop'
                    yarn build
                """
            }
        }
``` 
Esse Quarto passo será reponsável por fazer o build da aplicação.

 ***5. Quinto passo do Pipline.***
 ```
 stage ("Compress files") {
            steps {
                powershell script: """
                    \$ErrorActionPreference = 'Stop'
                    Compress-Archive -Path "$WORKSPACE\\build\\*" -DestinationPath "$WORKSPACE\\Nomedasuapasta.zip" -Force
                """
            }
        }
 ```
 Esse Quinto passo será reponsável por pegar os arquivos gerados no build do passo anterior, comprimir eles e mandar para uma pasta .zip dentro do servidor de Jenkins.
 
 ***6. Sexto passo do Pipline.***
```
stage ("Send files into server") {
            steps {
                powershell script: """
                    \$ErrorActionPreference = 'Stop'
                    Copy-Item -Path "$WORKSPACE\\Nomedasuapasta.zip" `
                        -Destination "\\\\$SERVER\\c\$\\zips para extracao" -Force
                """
            }
        }
 ```     
 Esse Sexto passo será reponsável por enviar os arquivios que está na sua pasta zipada do Jenkins, e enviar para o seu servidor.
 
 ***7. Sétimo passo do Pipline.***
```
stage('Uncompress Files Into Server'){
            steps{
                powershell script: """
                    \$ErrorActionPreference = 'Stop'
                    \$USER = '$env.USER'
                    \$PASS = '$env.PASS'
                    \$SERVER = '${SERVER}'
                    \$PASSWORD = \$PASS | ConvertTo-SecureString -AsPlainText -Force
                    \$CRED = New-Object System.Management.Automation.PSCredential -ArgumentList \$USER, \$PASSWORD

                    Invoke-Command -ComputerName \$SERVER -Credential \$CRED -ScriptBlock {
                        if(-Not (Test-Path -Path "C:\\zips para extracao\\OSBMobile")){
                            mkdir "C:\\zips para extracao\\OSBMobile" -Force
                        }

                        Remove-Item C:\\FitBank\\Deploy\\Sites\\OSBMobile\\static\\* -Recurse -Force -Verbose

                        Expand-Archive -Path "C:\\zips para extracao\\OSBMobile.zip" -DestinationPath "C:\\zips para extracao\\OSBMobile" -Force
                        Copy-Item -Path "C:\\zips para extracao\\OSBMobile\\*" -Destination C:\\FitBank\\Deploy\\Sites\\OSBMobile  -Recurse -Force -Verbose

                        Remove-Item "C:\\zips para extracao\\OSBMobile" -Recurse -Force
                    }
                """
                }
            }
        }
  ``` 
  Esse Sétimo passo será reponsável por descompactar os arquivos que estão zipados dentro do seu servidor, e mandar para a pasta destino final que será usada pela aplicação.
   
   ***8. Oitavo passo do Pipline.***
 ```
  post {
        always {
            echo 'Realizando a limpeza do Workspace!'
        }
        success {
            echo 'Deploy com sucesso!'
        }
        failure {
            echo "Falha no deploy."
        }
    }
}
```
Esse Oitavo e último passo será reponsável por finalizar o pipeline, fazendo a limpeza do jenkins, e relatando se o deploy ocorreu com sucesso ou falha.
 

