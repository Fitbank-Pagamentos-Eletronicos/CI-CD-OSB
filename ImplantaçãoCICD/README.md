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

Ao instalar um serviço para ser executado em uma conta de usuário de domínio, a conta deve ter o direito de fazer login como um serviço. Essa permissão de login se aplica estritamente ao computador local e deve ser concedida na Diretiva de Segurança Local.

Execute as seguintes etapas abaixo para editar a política de segurança local do computador no qual deseja definir a permissão 'logon as a service':


> Faça logon no computador com privilégios administrativos.

Abra as Ferramentas Administrativas e abra a Política de Segurança Local

Se a Política de segurança local estiver ausente em seu sistema, consulte a resposta em Onde baixar o GPEdit.msc para Windows 10 Home? pergunta no Microsoft Community para solucionar problemas

Expanda Política local e clique em Atribuição de direitos do usuário

No painel direito, clique com o botão direito do mouse em Fazer logon como um serviço e selecione Propriedades.

Clique no botão Adicionar usuário ou grupo… para adicionar o novo usuário.

Na caixa de diálogo Selecionar usuários ou grupos , localize o usuário que deseja inserir e clique em OK

Clique em OK nas Propriedades de logon como um serviço para salvar as alterações.

Depois de concluir as etapas acima, tente fazer login novamente com o usuário adicionado.

Outro ponto a ser levado em conta seria a transformação do  seu projeto em um site, você precisará criar um servidor web e publicar seu conteúdo nele. Existem vários serviços que você pode usar para hospedar seu conteúdo, incluindo serviços de hospedagem compartilhada e VPSs. Após configurar o servidor web adequadamente, você também precisará escolher um sistema de gerenciamento de conteúdo (CMS) para exibir seu conteúdo. Você também precisará configurar o DNS corretamente para apontar o domínio para seu site.

##################################################################################################################################



##################################################################################################################################
Para configurar o Jenkins com o GitHub, você precisa primeiro criar um projeto Jenkins e adicionar uma fonte de código do GitHub. Para isso, faça login no servidor Jenkins e vá para a página de configuração do projeto. Em seguida, clique em "Adicionar Fonte de Código" e selecione o repositório do GitHub que deseja usar. Depois disso, você pode configurar as etapas necessárias para executar a compilação, testes e implantação do código.






Fundamentos do pipeline na forma declarativa 
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


####################################################################################################
Configuração das credenciais 
- Umas das tarefas mais importantes da configuração de um pipeline funcional, será essa etapa de ajustes das credenciais, pois será de suma importancia para a execução do mesmo. 

    As credenciais armazenadas no Jenkins podem ser usadas:

- Em qualquer lugar aplicável em Jenkins (ou seja, credenciais globais),
- Por um projeto/item específico do Pipeline (leia mais sobre isso na seção Manipulando credenciais de Usando um Jenkinsfile ),
- Por um usuário Jenkins específico (como é o caso de projetos Pipeline criados em Blue Ocean ).

#Jenkins pode armazenar os seguintes tipos de credenciais:

- Texto secreto - um token como um token de API (por exemplo, um token de acesso pessoal do GitHub),
- Nome de usuário e senha - que podem ser tratados como componentes separados ou como uma string separada por dois pontos no formato username:password(leia mais sobre isso em Manuseio de credenciais ),
- Arquivo secreto - que é essencialmente conteúdo secreto em um arquivo,
- Nome de usuário SSH com chave privada - um par de chaves públicas/privadas SSH ,
- Certificado - um arquivo de certificado PKCS#12 e senha opcional, ou
- Credenciais de autenticação de certificado de host do Docker .


#Segurança de credenciais

Para maximizar a segurança, as credenciais configuradas no Jenkins são armazenadas de forma criptografada na instância do Jenkins do controlador (criptografadas pelo ID da instância do Jenkins) e são tratadas apenas nos projetos do Pipeline por meio de seus IDs de credencial.
Isso minimiza as chances de expor as próprias credenciais reais aos usuários do Jenkins e dificulta a capacidade de copiar as credenciais funcionais de uma instância do Jenkins para outra.

#Configurando credenciais
Esta seção descreve os procedimentos para configurar credenciais no Jenkins.

As credenciais podem ser adicionadas ao Jenkins por qualquer usuário do Jenkins que tenha a permissão Credentials > Create (definida por meio de Matrix-based security ). Essas permissões podem ser configuradas por um usuário Jenkins com a permissão Administrar . Leia mais sobre isso na seção Autorização de Gerenciando a segurança .

Caso contrário, qualquer usuário do Jenkins pode adicionar e configurar credenciais se as configurações de autorização da página Configurar configurações de segurança global da sua instância do Jenkins estiverem definidas como a configuração padrão Usuários conectados podem fazer qualquer coisa ou Qualquer pessoa pode fazer qualquer coisa .

#Adicionando novas credenciais globais
Para adicionar novas credenciais globais à sua instância do Jenkins:

1. Se necessário, verifique se você está conectado ao Jenkins (como um usuário com a permissão Credenciais > Criar ).

2. Na página inicial do Jenkins (ou seja, o Painel da IU clássica do Jenkins), clique em Gerenciar Jenkins > Gerenciar credenciais .

####################################################################################################

Configuração do Pipeline

- Primeiro passo será a configuração da configuração do Github com o Jenkins utilizando o "List Git branches 99 (and more)"
- Configurado o paramentro de comunicação do github, agora utilizaremos o paramentro de verificação de acesso, caso o jenkins seja configurado com usuario defaut, esse passo não será utilizado. Caso tenha necessite de acesso, será utilizado o paramentro User e Senha.
- Pipeline 
Será feito no modo de script na forma pipeline declarativo.
O arquivo de configuração do pipeline e todos os seus passos, estará disponivel no repositorio do CI/CD para melhor organização. 

