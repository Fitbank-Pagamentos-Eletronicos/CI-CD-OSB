# **Explicação passo a passo do pipeline**
***1. Primeiro passo do Pipline.*** 
 
    pipeline {
    agent any
    environment {
        SERVER  = 'nome do servidor'
    }
   Esse primeiro passo será reponsável por determinar qual o servidor que será utilizado.
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
   
   Esse seundo passo será reponsável por  selecionar e clonar o seu repositório, coloque o link do seu git e credentialsId entre aspas simples.
   
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
Esse quarto passo será reponsável por fazer o build da aplicação.

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
 Esse quinto passo será reponsável por pegar os arquivos gerados no build do passo anterior, comprimir eles e mandar para uma pasta .zip dentro do servidor de Jenkins.
 
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
 Esse sexto passo será reponsável por enviar os arquivios que está na sua pasta zipada do Jenkins, e enviar para o seu servidor.
 
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
                        if(-Not (Test-Path -Path "C:\\zips para extracao\\SUA PASTA")){
                            mkdir "C:\\zips para extracao\\SUA PASTA" -Force
                        }

                        Remove-Item C:\\SEU DIRETÓRIO\\static\\* -Recurse -Force -Verbose

                        Expand-Archive -Path "C:\\zips para extracao\\SUA PASTA.zip" -DestinationPath "C:\\zips para extracao\\SUA PASTA" -Force
                        Copy-Item -Path "C:\\zips para extracao\\SUA PASTA\\*" -Destination C:\\SEU DIRETÓRIO\\SUA PASTA  -Recurse -Force -Verbose

                        Remove-Item "C:\\zips para extracao\\SUA PASTA" -Recurse -Force
                    }
                """
                }
            }
        }
  ``` 
  Esse sétimo passo será reponsável por descompactar os arquivos que estão zipados dentro do seu servidor, e mandar para a pasta destino final que será usada pela aplicação.
   
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
Esse oitavo e último passo será reponsável por finalizar o pipeline, fazendo a limpeza do jenkins, e relatando se o deploy ocorreu com sucesso ou falha.
 
 
 
 
 
