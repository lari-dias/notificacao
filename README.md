# API Notificação

API REST desenvolvida em **Java com Spring Boot** para envio de notificações por e-mail relacionadas ao agendamento de tarefas. O projeto utiliza Spring Mail para comunicação SMTP, Thymeleaf para criação de templates HTML e integração com outros microsserviços.

A aplicação faz parte de uma arquitetura de microsserviços responsável pelo gerenciamento de usuários, tarefas e notificações.

## 🚀 Tecnologias utilizadas

- Java 17
- Spring Boot
- Spring Web
- Spring Mail (JavaMailSender)
- Thymeleaf
- SMTP
- Gmail SMTP
- Lombok
- Gradle
- HTML

## 📌 Funcionalidades

- Envio de notificações por e-mail
- Recebimento de requisições HTTP para envio de mensagens
- Integração com o microsserviço BFF Agendador
- Geração de mensagens HTML com Thymeleaf
- Personalização do conteúdo das notificações
- Envio de informações sobre tarefas agendadas
- Configuração de remetente e destinatário
- Comunicação com servidor SMTP
- Separação de responsabilidades utilizando arquitetura em camadas

## 🏗️ Estrutura do projeto

A aplicação organiza suas responsabilidades em componentes de API, serviço de e-mail e apresentação das mensagens.

```text
src/main
├── java
│   └── com/javanauta/notificacao
│       ├── Controller
│       ├── Service
│       └── DTO
│
└── resources
    ├── templates
    │   └── Template HTML de notificação
    │
    └── application.properties
```

A organização permite separar o recebimento das requisições, o processamento das notificações e a geração do conteúdo HTML.

## 📧 Envio de notificações

O envio de mensagens é realizado utilizando a interface `JavaMailSender`, disponibilizada pelo Spring Mail.

A aplicação utiliza `MimeMessage` e `MimeMessageHelper` para criar mensagens HTML com codificação UTF-8.

O conteúdo é processado pelo Thymeleaf, permitindo inserir informações dinâmicas sobre a tarefa.

**Fluxo:**

1. O serviço recebe os dados da tarefa.
2. O EmailService prepara as informações da notificação.
3. O Thymeleaf processa o template HTML.
4. O JavaMailSender configura a mensagem.
5. O servidor SMTP realiza o envio.
6. O usuário recebe a notificação por e-mail.

## 📍 API de envio de e-mail

O serviço disponibiliza uma operação HTTP para solicitar o envio de notificações.

Exemplo de corpo da requisição:

```json
{
  "nomeTarefa": "Estudar Spring Boot",
  "descricao": "Revisar integração entre microsserviços",
  "dataEvento": "20-10-2026 14:00:00",
  "emailUsuario": "usuario@email.com"
}
```

**Campos utilizados:**

- `nomeTarefa`: nome da tarefa agendada.
- `descricao`: descrição da atividade.
- `dataEvento`: data e horário do evento.
- `emailUsuario`: endereço de e-mail do destinatário.

A rota HTTP exata deve ser consultada no controller da aplicação.

## 🎨 Template HTML

O projeto utiliza Thymeleaf para gerar o conteúdo das notificações.

O template permite apresentar informações como:

- Título da notificação
- Nome da tarefa
- Descrição da atividade
- Data e horário do evento
- Informações do agendamento

A utilização de templates HTML permite organizar o conteúdo visual das mensagens e separar a apresentação da lógica de envio.

## 🔗 Integração entre microsserviços

O microsserviço de Notificação é integrado ao BFF Agendador, responsável por centralizar a comunicação entre as APIs.

O BFF utiliza OpenFeign para encaminhar os dados necessários ao envio das notificações.

**Arquitetura simplificada:**

```text
Cliente
   |
   v
BFF Agendador
   |
   +-- API Usuário
   |
   +-- API Agendador de Tarefas
   |
   +-- OpenFeign
          |
          v
     API Notificação
          |
          +-- EmailService
          |
          +-- Thymeleaf
          |
          +-- JavaMailSender
                 |
                 v
            Servidor SMTP
                 |
                 v
           E-mail do usuário
```

Essa estrutura permite manter o envio de e-mails separado das regras de negócio relacionadas ao gerenciamento de usuários e tarefas.

## ⚙️ Como executar o projeto

### Pré-requisitos

- Java 17+
- Gradle
- Conta de e-mail com acesso SMTP
- Configuração de autenticação no servidor de e-mail

### Configuração SMTP

No arquivo `application.properties`, configure:

```properties
server.port=8082

spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=${MAIL_USERNAME}
spring.mail.password=${MAIL_PASSWORD}

spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

Configure as variáveis de ambiente `MAIL_USERNAME` e `MAIL_PASSWORD` com as credenciais apropriadas.

Para utilizar Gmail, pode ser necessário gerar uma senha de app, conforme as configurações de segurança da conta.

**Importante:** não publique senhas, tokens ou credenciais SMTP no GitHub.

### Executar aplicação

**Linux/Mac:**

```bash
./gradlew bootRun
```

**Windows:**

```powershell
.\gradlew.bat bootRun
```

A aplicação será iniciada em:

```text
http://localhost:8082
```

## 🧪 Testes

O envio de notificações pode ser validado utilizando Postman ou outro cliente HTTP.

Para testar, envie uma requisição ao endpoint configurado no controller, informando os dados da tarefa e um endereço de e-mail válido.

Verifique a resposta da API, os logs da aplicação e o recebimento da mensagem na caixa de entrada.

## 👩‍💻 Desenvolvimento

Projeto desenvolvido para estudo e prática de:

- Desenvolvimento de APIs REST
- Arquitetura em camadas
- Integração entre microsserviços
- Comunicação HTTP com OpenFeign
- Envio de e-mails com JavaMailSender
- Configuração de servidores SMTP
- Criação de templates HTML com Thymeleaf
- Utilização de DTOs
- Separação de responsabilidades
- Boas práticas de desenvolvimento Back-end com Java

## 🔗 Projetos relacionados

**API Usuário:**  
https://github.com/lari-dias/usuario

**API Agendador de Tarefas:**  
https://github.com/lari-dias/agendador-tarefas

**BFF Agendador:**  
https://github.com/lari-dias/bff-agendador-tarefa

## 📄 Licença

Consulte o repositório para verificar as condições de licenciamento do projeto.
