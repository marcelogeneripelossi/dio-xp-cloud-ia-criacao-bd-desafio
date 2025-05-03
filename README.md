# 📋 Desafio: Criação e Configuração de uma Instância de Banco de Dados SQL no Microsoft Azure

Este documento detalha o processo de criação e configuração de um Servidor de Banco de Dados Windows e uma Instância de Banco de Dados SQL no Microsoft Azure, utilizando a conta gratuita do Azure e opções básicas para fins educacionais. 

O objetivo é fornecer um guia claro e estruturado para praticar conceitos de Bancos de Dados na nuvem, com anotações, resumos e dicas úteis para estudos e futuras implementações.

As etapas são destinadas exclusivamente a fins educacionais e não para ambientes de produção.

> _Este material é voltado para estudantes, iniciantes e profissionais em formação na área de computação em nuvem._

---

## 🎯 Objetivos do Desafio

Ao concluir este Passo a Passo, você aplicará conceitos de computação em nuvem em um ambiente prático no Azure.
- Documentar processos técnicos de forma clara, estruturada e reproduzível.
- Criar um servidor de Banco de Dados Windows no Azure;
- Criar e configurar uma Instância de Banco de Dados SQL;
- Aplicar conceitos práticos em um ambiente seguro e gratuito.

---

## 🚀 Pré-requisitos

Antes de começar, certifique-se de ter:
- Uma *conta gratuita do Azure*. Caso não tenha, crie uma em [azure.microsoft.com/free](https://azure.microsoft.com/free/) com:
  - Um número de telefone válido.
  - Um cartão de crédito ou débito para verificação (não será cobrado na conta gratuita).
    - Dica: utilize um Cartão de Crédito Virtual e Temporário para não ter nenhuma cobrança surpresa se esquecer de excluir os serviços após os estudos.
    - Lembre-se: **Fique atento** aos serviços utilizados para que não haja cobranças imprevistas.
  - Uma conta Microsoft ou GitHub.
- Acesso ao [Portal do Azure](https://portal.azure.com).
- Conhecimento básico sobre bancos de dados relacionais e o Azure.

*Dicas:* 
- A conta gratuita oferece 100.000 segundos de vCore de computação sem servidor e 32 GB de armazenamento mensal para o Azure SQL Database, além de um crédito de USD$200 por 30 dias.
- Use a [Calculadora de Preços do Azure](https://azure.microsoft.com/pricing/calculator/) para estimar custos e garantir que você permaneça dentro dos limites gratuitos.

---

## 🛠️ Criando um Servidor de Banco de Dados Windows no Azure

Nesta seção, criaremos uma máquina virtual (VM) Windows no Azure que será configurada como um servidor de banco de dados. Usaremos o SQL Server em uma VM Windows, uma opção compatível com a conta gratuita para aprendizado.

### Passo a Passo

1. *Acesse o Portal do Azure*:
   - Faça login em [portal.azure.com](https://portal.azure.com) com sua conta gratuita.

2. *Criar uma Máquina Virtual (VM)*:
   - No menu lateral, clique em *Criar um recurso* ou pesquise por *Máquinas Virtuais* no campo de busca.
   - Clique em *Criar* > *Máquina Virtual*.

3. *Configurar as Informações Básicas*:
   - *Assinatura*: Selecione sua assinatura gratuita (ex.: "Avaliação Gratuita").
   - *Grupo de Recursos: Crie um novo grupo (ex.: myResourceGroup) clicando em **Criar novo* e inserindo o nome.
   - *Nome da Máquina Virtual*: Insira um nome, como WinSQLServer.
   - *Região: Escolha uma região padrão, como **East US* (disponível na conta gratuita).
   - *Opções de Disponibilidade*: Deixe como padrão (sem configuração adicional para aprendizado).
   - *Imagem: Selecione **Windows Server 2019 Datacenter* com SQL Server pré-instalado (ex.: "SQL Server 2019 on Windows Server 2019"). Verifique se a opção está no nível gratuito.
   - *Tamanho: Escolha um tamanho básico, como **B1s* (1 vCore, 1 GB RAM), que é elegível para o nível gratuito.

4. *Configurar Credenciais*:
   - *Nome de Usuário*: Insira um nome de administrador (ex.: azureadmin).
   - *Senha*: Crie uma senha forte (anote-a, pois será necessária para acessar a VM).
   - Confirme a senha e clique em *Avançar: Discos*.

5. *Configurar Discos*:
   - Mantenha as configurações padrão (disco SSD padrão de 128 GB é suficiente para aprendizado).
   - Clique em *Avançar: Rede*.

6. *Configurar Rede*:
   - *Rede Virtual*: Crie uma nova rede virtual (ex.: myVNet) ou use a padrão.
   - *Sub-rede*: Use a sub-rede padrão.
   - *IP Público*: Mantenha o IP público padrão para acesso remoto.
   - *Portas de Entrada: Habilite a porta **RDP (3389)* para conectar à VM e a porta *1433* para o SQL Server.
   - Clique em *Avançar: Gerenciamento*.

7. *Configurar Gerenciamento*:
   - Mantenha as configurações padrão para monitoramento e atualizações.
   - Clique em *Avançar: Configurações do SQL Server*.

8. *Configurações do SQL Server*:
   - *Autenticação: Escolha **Autenticação do SQL Server* (mais simples para aprendizado).
   - *Nome de Usuário do SQL*: Insira um usuário (ex.: sqladmin).
   - *Senha do SQL*: Crie uma senha forte e anote-a.
   - Clique em *Revisar + Criar*.

9. *Revisar e Criar*:
   - Revise as configurações e clique em *Criar*.
   - Aguarde a implantação (pode levar alguns minutos).

10. *Conectar à VM*:
    - Após a criação, vá para *Máquinas Virtuais* > WinSQLServer > *Conectar* > *RDP*.
    - Baixe o arquivo RDP, abra-o e insira as credenciais (azureadmin e a senha).
    - Conecte-se à VM Windows.

11. *Verificar o SQL Server*:
    - Na VM, abra o *SQL Server Management Studio (SSMS)* (pré-instalado).
    - Conecte-se usando o servidor local (localhost) e as credenciais do SQL (sqladmin e senha).
    - Crie um banco de dados de teste (ex.: TestDB) para validar a configuração.

### Resumo
- Criamos uma VM Windows com SQL Server 2019 usando o nível gratuito do Azure.
- Configuramos uma máquina básica (B1s) com autenticação SQL para facilitar o aprendizado.
- A VM está acessível via RDP, e o SQL Server está pronto para uso.

### Dicas
- *Gerenciamento de Custos: Monitore o uso no painel **Custo* do Azure para evitar exceder os limites gratuitos.
- *Segurança*: Para aprendizado, habilitamos a porta 1433, mas em produção, use uma VPN ou ponto de extremidade privado.
- *Limpeza*: Quando não precisar mais, exclua o grupo de recursos (myResourceGroup) para liberar recursos.

---

## 🖥️ Criando e Configurando uma Instância de Banco de Dados SQL no Azure

Nesta seção, criaremos uma instância do Azure SQL Database, um serviço de banco de dados gerenciado que não requer gerenciamento de servidor físico, ideal para aprendizado.

### Passo a Passo

1. *Acesse o Portal do Azure*:
   - Faça login em [portal.azure.com](https://portal.azure.com).

2. *Criar um Banco de Dados SQL*:
   - No menu lateral, clique em *Criar um recurso* ou pesquise por *Banco de Dados SQL*.
   - Clique em *Criar* na seção *Banco de Dados SQL*.

3. *Configurar Informações Básicas*:
   - *Assinatura*: Selecione a assinatura gratuita.
   - *Grupo de Recursos*: Use o mesmo grupo criado anteriormente (myResourceGroup) ou crie um novo.
   - *Nome do Banco de Dados*: Insira um nome, como mySampleDatabase.
   - *Servidor*:
     - Clique em *Criar novo*.
     - *Nome do Servidor*: Insira um nome exclusivo (ex.: mysqlserver123). O Azure adicionará o sufixo .database.windows.net.
     - *Localização: Escolha **East US* (compatível com a conta gratuita).
     - *Autenticação: Use **Autenticação do SQL*.
     - *Nome de Usuário do Administrador*: Insira sqladmin.
     - *Senha*: Crie uma senha forte e anote-a.
     - Clique em *OK*.
   - *Quer usar um pool elástico?: Selecione **Não* (opção mais simples para aprendizado).

4. *Configurar Computação e Armazenamento*:
   - Clique em *Configurar banco de dados*.
   - Escolha o plano *Básico* (modelo baseado em DTU, 5 DTUs, 2 GB de armazenamento), ideal para cargas de trabalho leves e gratuito.
   - Clique em *Aplicar*.

5. *Configurar Rede*:
   - Na guia *Rede, selecione **Ponto de extremidade público*.
   - *Permitir serviços e recursos do Azure acessarem este servidor: Selecione **Sim* (permite acesso de serviços como backup).
   - *Adicionar endereço IP do cliente atual: Selecione **Sim* (adiciona seu IP ao firewall para acesso remoto).
   - Mantenha as outras configurações padrão (ex.: TLS 1.2, política de conexão padrão).
   - Clique em *Avançar: Segurança*.

6. *Configurar Segurança*:
   - *Microsoft Defender para SQL*: Desative (não necessário para aprendizado).
   - *Transparent Data Encryption*: Mantenha ativado (padrão).
   - Clique em *Avançar: Configurações Adicionais*.

7. *Configurações Adicionais*:
   - *Fonte de Dados: Selecione **Exemplo* para criar o banco de dados de amostra *AdventureWorksLT*, que contém tabelas e dados para prática.
   - *Ambiente de Carga de Trabalho: Escolha **Desenvolvimento* (otimiza para baixo custo com redundância local).
   - Clique em *Revisar + Criar*.

8. *Revisar e Criar*:
   - Revise as configurações e clique em *Criar*.
   - Aguarde a implantação (pode levar alguns minutos).

9. *Antes de Conectar ao Banco de Dados, vamos instalar o SQL Server Management Studio (SSMS)*:
    - **Acesse o site oficial de download do SSMS**:  
   [Download do SSMS](https://aka.ms/ssms)
    - Baixe a versão mais recente do SSMS disponível.
    - Após o download, execute o instalador **SSMS-Setup-ENU.exe**.
    - Siga os passos de instalação:
      - Aceite os termos de licença;
      - Escolha o diretório de instalação (recomenda-se manter o padrão);
      - Clique em **Instalar** e aguarde a conclusão.

10. *Conectar ao Banco de Dados*:
   - No Azure, após a criação do Banco de Dados, vá para *Bancos de Dados SQL* > mySampleDatabase.
   - Copie o *Nome do Servidor* (ex.: mysqlserver123.database.windows.net).
   - Abra o *SQL Server Management Studio (SSMS)* em seu computador.
   - Conecte-se usando:
     - *Nome do Servidor*: mysqlserver123.database.windows.net.
     - *Autenticação*: Autenticação do SQL Server.
     - *Login*: sqladmin.
     - *Senha*: A senha configurada.
     - *Banco de Dados*: mySampleDatabase.
   - Se solicitado, faça login no Azure para adicionar seu IP ao firewall.

11. *Testar o Banco de Dados*:
    - No SSMS, expanda o banco de dados mySampleDatabase.
    - Execute a consulta abaixo para verificar os dados da amostra:
      sql
      SELECT TOP 10 * FROM SalesLT.Customer;
      
    - Você verá dados da tabela Customer do banco *AdventureWorksLT*.

### Resumo
- Criamos um banco de dados SQL gerenciado no Azure com o plano Básico (5 DTUs, 2 GB) e o banco de amostra *AdventureWorksLT*.
- Configuramos um servidor lógico (mysqlserver123) com autenticação SQL e acesso público para aprendizado.
- Conectamos o banco ao SSMS para consultas.

### Dicas
- *Firewall: Adicione IPs manualmente no portal do Azure se mudar de rede (em **Configurações de Firewall* do servidor).
- *Ferramentas Alternativas: Use o **Azure Data Studio* ou o *Editor de Consultas* no portal do Azure para consultas leves.
- *Exclusão de Recursos*: Exclua o grupo de recursos (myResourceGroup) após o uso para evitar consumo desnecessário.
- *Estudos: Explore o banco **AdventureWorksLT* para praticar consultas T-SQL, como SELECT, JOIN e GROUP BY.

---

## Considerações Finais

Este guia demonstrou como criar e configurar:
1. Um servidor de banco de dados Windows em uma VM com SQL Server 2019.
2. Uma instância de Banco de Dados SQL gerenciada no Azure com o banco de amostra *AdventureWorksLT*.

Ambas as configurações usaram opções básicas e gratuitas, ideais para aprendizado. O processo foi documentado de forma clara para facilitar a reprodução e servir como material de estudo.

*Próximos Passos*:
- Pratique consultas T-SQL no banco *AdventureWorksLT*.
- Explore recursos como *pools elásticos* ou *hiperescala* para cenários avançados.
- Estude a integração do Azure SQL com aplicativos (ex.: ASP.NET) usando tutoriais no [Microsoft Learn](https://learn.microsoft.com).

*Limpeza*:
- Para evitar custos, vá para *Grupos de Recursos* > myResourceGroup > *Excluir grupo de recursos. Confirme o nome e clique em **Excluir*.

---

## Referências
- [Microsoft Learn: Criar um Banco de Dados SQL](https://learn.microsoft.com/azure/azure-sql/database/single-database-create-quickstart)[](https://learn.microsoft.com/pt-br/azure/azure-sql/database/single-database-create-quickstart?view=azuresql)
- [Microsoft Azure: Conta Gratuita](https://azure.microsoft.com/free/)[](https://azure.microsoft.com/pt-br/pricing/purchase-options/azure-account)
- [Documentação do SQL Server em VMs](https://learn.microsoft.com/azure/azure-sql/virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview)[](https://learn.microsoft.com/pt-br/azure-data-studio/deploy-azure-sql-server-vm)

---
