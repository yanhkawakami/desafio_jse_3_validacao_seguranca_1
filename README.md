# Sistema de Gestão de Eventos e Cidades

Este projeto implementa uma API REST para gerenciamento de eventos e cidades, com sistema completo de autenticação, autorização e validação de dados utilizando Spring Boot e Spring Security.

## 📋 Sobre o Projeto

O sistema permite gerenciar cidades e eventos com diferentes níveis de acesso:
- **Cidades**: Listagem pública, criação restrita a administradores
- **Eventos**: Listagem pública, criação disponível para usuários logados
- **Autenticação**: Sistema OAuth2 com diferentes perfis de usuário

## 🚀 Tecnologias Utilizadas

- **Java 17**
- **Spring Boot 3.x**
- **Spring Security 6.x** (OAuth2 Resource Server)
- **Spring Data JPA**
- **H2 Database** (para testes)
- **Bean Validation**
- **Maven**
- **JUnit 5** (para testes)

## 📊 Modelo de Dados

### Entidades

**City** (Cidade)
- `id`: Identificador único
- `name`: Nome da cidade

**Event** (Evento)
- `id`: Identificador único
- `name`: Nome do evento
- `date`: Data do evento
- `url`: URL relacionada ao evento
- `city`: Cidade onde ocorre o evento (relacionamento ManyToOne)

**User** (Usuário)
- `id`: Identificador único
- `email`: Email do usuário
- `password`: Senha criptografada
- `roles`: Perfis de acesso

**Role** (Perfil)
- `id`: Identificador único
- `authority`: Nome do perfil (ROLE_ADMIN, ROLE_CLIENT)

## 🔐 Sistema de Segurança

### Perfis de Usuário

- **ROLE_ADMIN**: Administrador com acesso completo
- **ROLE_CLIENT**: Cliente com acesso limitado

### Regras de Autorização

#### Endpoints de Cidades (`/cities`)
- `GET /cities`: Acesso público (sem autenticação)
- `POST /cities`: Acesso restrito a ADMIN

#### Endpoints de Eventos (`/events`)
- `GET /events`: Acesso público (sem autenticação)
- `POST /events`: Acesso para CLIENT e ADMIN autenticados

## 📝 Validações

### Cidade
- Nome obrigatório e não pode estar em branco

### Evento
- Nome obrigatório e não pode estar em branco
- Data obrigatória
- URL obrigatória
- Cidade obrigatória (deve existir no sistema)

## 🛠️ Como Executar

### Pré-requisitos
- Java 17
- Maven 3.x

### Executando a aplicação

```bash
# Clone o repositório
git clone <repository-url>

# Entre no diretório
cd <project-directory>

# Execute com Maven
./mvnw spring-boot:run
```

### Executando os testes

```bash
# Executa todos os testes
./mvnw test
```

## 📡 API Endpoints

### Autenticação
```
POST /oauth/token
```

### Cidades
```
GET    /cities          # Lista todas as cidades (público)
POST   /cities          # Cria nova cidade (ADMIN apenas)
```

### Eventos
```
GET    /events          # Lista eventos paginados (público)
POST   /events          # Cria novo evento (CLIENT/ADMIN)
```

## 🧪 Dados de Teste

O sistema vem pré-configurado com dados de teste:

### Usuários
- **Admin**: `bob@gmail.com` / `123456`
- **Cliente**: `ana@gmail.com` / `123456`

### Cidades
- São Paulo, Brasília, Fortaleza, Salvador, etc.

### Eventos
- Feira do Software, CCXP, Congresso Linux, etc.

## 📋 Funcionalidades Implementadas

✅ CRUD completo de cidades com autorização  
✅ CRUD completo de eventos com autorização  
✅ Sistema de autenticação OAuth2  
✅ Validação de dados com Bean Validation  
✅ Tratamento global de exceções  
✅ Testes de integração  
✅ Paginação de eventos  
✅ Ordenação alfabética de cidades  

## 🏗️ Arquitetura

O projeto segue uma arquitetura em camadas:

```
├── controllers/     # Controladores REST
├── dto/            # Objetos de transferência de dados
├── entities/       # Entidades JPA
├── repositories/   # Repositórios de dados
├── services/       # Lógica de negócio
├── config/         # Configurações de segurança
└── handlers/       # Tratamento de exceções
```

## 🤝 Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
