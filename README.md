# FórumHub API

![Status](https://img.shields.io/badge/status-concluído-brightgreen)
![Java](https://img.shields.io/badge/Java-17%2B-blue)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-green)
![Security](https://img.shields.io/badge/Security-JWT-blueviolet)

## 📖 Sobre o Projeto

**FórumHub** é uma API RESTful desenvolvida como parte do Challenge de Back End da Alura em parceria com a Oracle (ONE). O projeto simula o back-end de um fórum de discussões, permitindo a criação, consulta, atualização e exclusão de tópicos (CRUD).

A API é protegida, exigindo autenticação via Token JWT para a maioria das operações, garantindo que apenas usuários autenticados possam interagir com os dados.

## ✨ Funcionalidades

-   ✅ **Autenticação:** Endpoint `/login` para autenticar usuários e gerar tokens JWT.
-   ✅ **CRUD de Tópicos:**
    -   **C**reate: Criar um novo tópico.
    -   **R**ead: Listar todos os tópicos (com paginação) e detalhar um tópico específico por ID.
    -   **U**pdate: Atualizar as informações de um tópico.
    -   **D**elete: Excluir um tópico do banco de dados.
-   ✅ **Validações:** Validações de dados de entrada conforme as regras de negócio (ex: campos obrigatórios, não duplicidade de tópicos).
-   ✅ **Controle de Versão do Banco de Dados:** Uso do Flyway para gerenciar as migrações do schema do banco de dados de forma automática.

## Endpoints da API

| Método | URI             | Protegido? | Descrição                                        |
| :----- | :-------------- | :--------- | :------------------------------------------------- |
| `POST` | `/login`        | Não        | Autentica um usuário e retorna um token JWT.       |
| `POST` | `/topicos`      | Sim        | Cria um novo tópico.                               |
| `GET`  | `/topicos`      | Sim        | Lista todos os tópicos de forma paginada.          |
| `GET`  | `/topicos/{id}` | Sim        | Detalha um tópico específico pelo seu ID.          |
| `PUT`  | `/topicos`      | Sim        | Atualiza um tópico existente (ID enviado no corpo). |
| `DELETE`| `/topicos/{id}` | Sim        | Exclui um tópico específico.                       |

## 🛠️ Tecnologias Utilizadas

-   **Java 17**
-   **Spring Boot 3**
-   **Spring Web**
-   **Spring Security** (com autenticação via JWT)
-   **Spring Data JPA**
-   **Flyway Migration**
-   **MySQL** (Banco de Dados Relacional)
-   **Lombok**
-   **Maven**

## 🚀 Como Executar o Projeto

Siga os passos abaixo para executar a API localmente.

### Pré-requisitos

-   **JDK 17** ou superior.
-   **Maven** 3.8 ou superior.
-   **MySQL 8** instalado e em execução.
-   Uma ferramenta para testar APIs, como **[Insomnia](https://insomnia.rest/)** ou **[Postman](https://www.postman.com/)**.

### Passos para Execução

1.  **Clone o Repositório**
    ```bash
    git clone https://github.com/Gabaes/forumhub-api.git
    cd forumhub-api
    ```

2.  **Configure o Banco de Dados**
    -   Crie um banco de dados no MySQL com o nome `forumhub`.
    -   Abra o arquivo `src/main/resources/application.properties`.
    -   Atualize as seguintes propriedades com seu usuário e senha do MySQL:
        ```properties
        spring.datasource.username=seu_usuario_aqui
        spring.datasource.password=sua_senha_aqui
        ```

3.  **Execute a Aplicação**
    -   Você pode executar o projeto de duas formas:
        -   **Via Maven (no terminal):**
            ```bash
            mvn spring-boot:run
            ```
        -   **Via IDE (IntelliJ, Eclipse, etc.):**
            -   Abra o projeto.
            -   Execute a classe principal `ApiApplication.java`.
    -   *Ao iniciar, o Flyway criará automaticamente as tabelas `topicos` e `usuarios` no seu banco de dados.*

## 🧪 Como Testar a API

Como a API é protegida, você precisa primeiro se autenticar para obter um token.

1.  **Crie um Usuário (Opcional)**
    * Para testar, você precisará de um usuário no banco. Você pode inseri-lo manualmente no seu banco de dados MySQL. A senha precisa ser criptografada com BCrypt.

2.  **Faça o Login**
    -   Envie uma requisição `POST` para `http://localhost:8080/login`.
    -   No corpo (body) da requisição, envie um JSON com as credenciais:
        ```json
        {
          "login": "seu_usuario@email.com",
          "senha": "sua_senha"
        }
        ```
    -   A API retornará um token JWT. Copie este token.

3.  **Acesse os Endpoints Protegidos**
    -   Para acessar qualquer outro endpoint (ex: `GET /topicos`), adicione o seguinte cabeçalho (Header) na sua requisição:
        -   **Chave:** `Authorization`
        -   **Valor:** `Bearer SEU_TOKEN_COPIADO_AQUI`
    -   Agora suas requisições serão autorizadas e funcionarão corretamente.
