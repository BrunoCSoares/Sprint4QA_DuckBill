# FIAP - Análise e Desenvolvimento de Sistemas
## Projeto DuckBill

**Autores:**
* Bruno Carlos Soares RM - 559250
* Lucas Borges de Souza RM - 560027
* Pedro Henrique da Silva RM - 560393

**Documento Base De Testes - Sprint 4 (Duckbill)**
*Compliance, Quality Assurance & Tests*
*Trabalho apresentado como requisito parcial ao curso de Análise e Desenvolvimento de Sistemas.*
*Challenge 2º Ano - 2TDSPS*
*São Paulo 2026*

---

## Introdução e Metodologia de Testes

Este documento apresenta a estratégia de Quality Assurance (QA) e o planeamento de testes de validação aplicados ao projeto DuckBill durante a Sprint 4. O objetivo principal é garantir o compliance com os requisitos estipulados, validando tanto as regras de negócio essenciais como a estabilidade e responsividade da interface de utilizador (UI).
Para garantir uma cobertura eficiente, a abordagem foi estruturada em duas frentes complementares: testes manuais de sistema e automação de testes de front-end.

### Configuração: Testes Manuais
A primeira etapa engloba os testes manuais (CT01 a CT03), que foram estruturados e geridos utilizando a plataforma Azure Boards. A configuração foi realizada através da criação de um Test Plan específico para a Sprint 4, utilizando Requirement-based suites para vincular cada Caso de Teste diretamente aos Product Backlog Items (PBIs) correspondentes no Kanban. Todos os cenários foram desenhados com dados de entrada controlados e saídas predefinidas, garantindo a rastreabilidade e a aferição precisa das funções de gestão financeira (transações e metas) e da integração com IA.

### Configuração: Testes Automatizados
A segunda etapa refere-se à automação de interface (CT04 a CT07), implementada através da ferramenta Katalon, utilizando a técnica de Record & Playback. O ambiente de testes foi configurado para correr a aplicação Web localmente (localhost). Para contornar os desafios de sincronização de estado virtual comuns em aplicações modernas (como o React), os scripts foram ajustados tecnicamente com injeção de atrasos (pause) e simulação de eventos reais de teclado (runScript) para garantir a correta validação dos formulários e habilitação de botões. A suíte automatizada abrange Smoke Tests de navegação, testes funcionais de comunicação com a IA e testes negativos de validação de formulários vazios, provando a robustez do sistema contra falhas de uso.

---

## 1. Testes Manuais de Validação de Sistema
Estes testes serão registados nos Work Items (Test Cases) do Azure DevOps, vinculados aos PBIs correspondentes.

### 1.1. CT01: Registar transação de saída e validar saldo (PBI: Manter Transações - Luizito)
* **Teste Planeado:** Validação do cálculo de saldo ao inserir uma nova despesa.
* **Dados de Entrada (Input):**
    * a. Tipo de despesa: Alimentação
    * b. Valor: R$ 36,00
    * c. Descrição: McDonalds Big Mac
* **Dados de Saída (Output):**
    * a. O saldo total na janela de Carteira/Dashboard deve ser decrementado em exatamente R$ 36,00.
    * b. A transação "McDonalds Big Mac" deve aparecer no histórico.
* **Procedimento (Passos):**
    * a. Realizar login na aplicação.
    * b. Aceder à janela “Cofre” da aplicação.
    * c. Clicar no botão para adicionar nova transação.
    * d. Preencher os dados de despesa (Alimentação, R$ 36,00, McDonalds Big Mac).
    * e. Clicar em "Salvar", regressar à janela do Cofre e verificar o valor do Saldo Total e histórico.

### 1.2. CT02: Criar meta e validar progresso inicial (PBI: Manter Metas - Ambição Financeira)
* **Teste Planeado:** Validação da criação de uma meta e do cálculo da barra de progresso.
* **Dados de Entrada (Input):**
    * a. Nome da Meta: Notebook
    * b. Valor Total da Meta: R$ 2.000,00
    * c. Valor do Depósito Inicial: R$ 500,00
* **Dados de Saída (Output):**
    * a. A meta "Notebook" deve ser listada no ecrã.
    * b. A barra ou indicador de progresso deve exibir visualmente a percentagem de 25% concluído.
* **Procedimento (Passos):**
    * a. Aceder à janela "Metas" no menu de navegação.
    * b. Clicar em "+" ao lado de “Minhas Metas”.
    * c. Inserir o Nome (Notebook) e Valor Total (R$ 2.000,00) e guardar.
    * d. Carregar em “Guardar Dinheiro” abaixo da meta referida e adicionar R$ 500,00.
    * e. Carregar em “Guardar Dinheiro” abaixo da meta referida e adicionar R$ 1500,00.

### 1.3. CT03: Categorização Inteligente de Despesa (PBI: Integração IA - Adaptado)
* **Teste Planeado:** Validação do preenchimento automático do campo categoria ao digitar uma despesa conhecida.
* **Dados de Entrada (Input):**
    * a. Valor: R$ 50,00
    * b. Descrição da transação: cinema
* **Dados de Saída (Output):**
    * a. O sistema deve sugerir a categoria Lazer.
* **Procedimento (Passos):**
    * a. Aceder à janela de Cofre.
    * b. Clicar em "+" para registar uma nova despesa.
    * c. Inserir o valor de R$ 50,00 e a descrição “cinema”.
    * d. Clicar em “aceitar” na categoria sugerida.

---

## 2. Testes Automatizados de Validação de Interface

### 2.1. CT04: Interação com Chatbot e Validação de Retorno (Teste Funcional)
Validação da comunicação entre o front-end e o serviço de IA, garantindo que o envio de um prompt gera um retorno na interface.
* **Dados de Entrada (Input):**
    * a. Clique no botão de "Pergunta Sugerida".
* **Dados de Saída (Output):**
    * a. O sistema deve processar a requisição e renderizar um novo componente de mensagem (balão de resposta do bot) na janela de chat.
* **Procedimento (Passos):**
    * a. Com o utilizador já logado, aceder à janela do Chatbot / DuckBill AI.
    * b. Identificar e clicar numa das opções de perguntas rápidas sugeridas no ecrã.
    * c. Aguardar o tempo de processamento da IA.
    * d. Validar se um novo balão de mensagem com a resposta da IA foi adicionado ao histórico do chat.

### 2.2. CT05: Teste de Navegação Completa pelo Menu (SmokeTest)
Validação do roteamento (routing) contínuo entre todas as páginas principais da aplicação através do menu de navegação.
* **Dados de Entrada (Input):**
    * a. Cliques sequenciais nos botões de navegação do menu (ex: "Metas", "Transações/Cofre", "Perfil/Configurações").
* **Dados de Saída (Output):**
    * a. O sistema deve redirecionar o utilizador para todas as rotas solicitadas em sequência, sem apresentar erros (ecrãs em branco ou quebra de layout).
    * b. Os títulos/elementos principais de cada uma das janelas acedidas devem ser renderizados corretamente.
* **Procedimento (Passos):**
    * a. Clicar no botão do “Cofre” no menu de navegação e verificar o carregamento do ecrã.
    * b. Clicar no botão de “Início” no menu para voltar ao ecrã inicial.
    * c. Clicar no botão de “Metas” no menu e verificar o carregamento.
    * d. Clicar no botão de “Início” no menu para voltar ao ecrã inicial.
    * e. Clicar no botão do “Mapa” no menu e verificar o carregamento.
    * f. Clicar no botão de “Início” no menu para voltar ao ecrã inicial.
    * g. Clicar no botão de “Perfil” no menu e verificar o carregamento.
    * h. Clicar no botão de “Início” no menu para voltar ao ecrã inicial.

### 2.3. CT06: Teste de Segurança: Controlo de Acesso (Login/Logout)
Validação da segurança de acesso à aplicação, garantindo que o sistema autentica utilizadores válidos e encerra completamente a sessão ativa após o logout.
* **Dados de Entrada (Input):**
    * a. E-mail: 'bruno@gmail.com'
    * b. Palavra-passe (Senha): '123123'
    * c. Ação do utilizador: Clique no botão "Sair / Log Out".
* **Dados de Saída (Output):**
    * a. No Login: O sistema deve validar as credenciais, gerar o token de sessão e redirecionar o utilizador para a rota privada da Dashboard.
    * b. No Logout: O sistema deve destruir o token de sessão, limpar os dados do local storage/cookies e redirecionar o utilizador de volta para o ecrã público de Login, bloqueando qualquer tentativa de retrocesso de página.
* **Procedimento (Passos):**
    * a. Abrir o navegador e aceder ao URL do ecrã de login da aplicação.
    * b. Preencher os campos de credenciais com os dados de entrada controlados (E-mail e Palavra-passe).
    * c. Clicar no botão "Entrar" e validar o redirecionamento com sucesso para a Dashboard interna.
    * d. Localizar no menu de navegação e clicar no botão correspondente a "Sair" (Logout).
    * e. Aguardar o redirecionamento automático para a página inicial de login.

### 2.4. CT07: Bloqueio de Formulário Vazio na Compra de Ativos (Teste Negativo)
Validação da consistência do front-end ao impedir o envio de um formulário com campos obrigatórios em branco na janela de Mapa.
* **Dados de Entrada (Input):**
    * a. Submissão do formulário de "Nova Compra de Ativo" sem inserir dados em nenhum dos campos (Nome, Valor, Quantidade, etc. mantidos vazios).
* **Dados de Saída (Output):**
    * a. O sistema não deve registar a transação nem fechar a janela.
* **Procedimento (Passos):**
    * a. Com o utilizador já logado, aceder ao ecrã "Mapa" através do menu de navegação.
    * b. Clicar no botão ou opção para iniciar o registo de uma "Nova Compra de Ativo".
    * c. Manter todos os campos de entrada de dados totalmente em branco.
    * d. Clicar no botão de confirmar/guardar a compra.
    * e. Validar se a ação foi bloqueada.

---

## 3. Anexos
* **Link Azure Boards (CT01; CT02; CT03):** https://dev.azure.com/RM559250/DuckBill
* **Vídeo: teste automatizado CT04:** https://youtu.be/UhhfHP9aPIs
* **Vídeo: teste automatizado CT05:** https://youtu.be/2oxwsTnKEmg
* **Vídeo: teste automatizado CT06:** https://youtu.be/nqKj0lAWkks
* **Vídeo: teste automatizado CT07:** https://youtu.be/yStdf12Nj74
