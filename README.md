# 🦷 API OdontoPrev - .NET 8 com Oracle Database

## 📋 Sobre o Projeto

Esta API foi desenvolvida em **.NET 8** para gerenciar operações odontológicas, incluindo pacientes, dentistas, consultas e procedimentos. A solução utiliza **Oracle Database** e está configurada para deploy automatizado no **Azure App Service** via **Azure DevOps Pipelines**.

### 🏗️ Arquitetura da Solução

![image](https://github.com/user-attachments/assets/3ace0c49-16e3-42e5-be27-67ac252bd93c)


### 🚀 Tecnologias Utilizadas

- **.NET 8** - Framework principal
- **Oracle.ManagedDataAccess** - Driver Oracle
- **Swagger/OpenAPI** - Documentação da API
- **Azure App Service** - Hospedagem cloud
- **Azure DevOps** - CI/CD Pipeline

---

## 🏗️ Funcionamento Detalhado da Pipeline

### Visão Geral do Fluxo

A pipeline representa um exemplo moderno de **DevOps e CI/CD** para aplicações .NET, demonstrando a integração completa desde o desenvolvimento até a produção, passando por infraestrutura automatizada e deploy contínuo.

### Detalhamento por Estágios

#### **1. Desenvolvedores** 👨‍💻
O processo inicia com a **equipe de desenvolvimento** criando e modificando o código da API OdontoPrev. Esta etapa representa o trabalho colaborativo onde múltiplos desenvolvedores contribuem para a evolução da aplicação.

#### **2. Visual Studio** 💜
O **ambiente de desenvolvimento integrado (IDE)** onde o código .NET 8 é escrito, testado localmente e preparado para versionamento. O Visual Studio fornece ferramentas essenciais como IntelliSense, debugging e integração com Git.

#### **3. Azure Repos Git** 🧡
O **repositório centralizado** que armazena todo o código-fonte. Quando os desenvolvedores fazem **push** para as branches `main` ou `develop`, automaticamente **acionam a pipeline** através dos triggers configurados no YAML.

### Pipeline Automatizada - Núcleo da Solução

#### **4. Implantação (Infrastructure as Code)** 🔧
- **Grupo de Recursos**: Criação automatizada do Resource Group no Azure
- **App Service Plan**: Provisionamento da infraestrutura de hospedagem (tier F1)
- **Benefício**: Infraestrutura **versionada, repetível e auditável**

#### **5. Build e Testes** 🏗️
- **Build .NET**: Compilação da aplicação com .NET 8 SDK
- **Artefatos**: Geração dos binários otimizados para produção
- **Testes**: Execução de testes unitários e de integração
- **Benefício**: **Qualidade garantida** antes do deploy

#### **6. Deploy** 🚀
- **Criação do Web App**: Instanciação do Azure App Service
- **Configuração**: Aplicação das connection strings Oracle
- **Deploy**: Publicação dos artefatos na infraestrutura
- **Benefício**: Deploy **consistente e automatizado**

### Ambiente de Produção

#### **7. Web App Azure** ☁️
A **aplicação .NET hospedada** no Azure App Service, oferecendo:
- **Escalabilidade automática**
- **Alta disponibilidade**
- **Monitoramento integrado**
- **SSL/TLS automático**

#### **8. VM Windows + Banco Oracle SQL** 🗄️
O **banco de dados Oracle** rodando em máquina virtual da FIAP, fornecendo:
- **Persistência robusta** dos dados odontológicos
- **Performance empresarial**
- **Integridade transacional**

### Aspectos Técnicos Avançados

#### **🔄 Automação Completa**
- **Zero intervenção manual** após configuração inicial
- **Rollback automático** em caso de falhas
- **Notifications** de status via Azure DevOps

#### **🛡️ Segurança Integrada**
- **Service Connections** com princípios de menor privilégio
- **Connection strings** gerenciadas como variáveis seguras
- **Secrets** não expostos no código

#### **📊 Observabilidade**
- **Logs centralizados** no Azure Monitor
- **Métricas** de performance e disponibilidade
- **Alertas** proativos para problemas

### Benefícios Organizacionais

#### **⚡ Velocidade de Entrega**
- **Deploy em minutos** vs. horas manuais
- **Feedback rápido** sobre qualidade do código
- **Time-to-market** reduzido significativamente

#### **🎯 Qualidade e Confiabilidade**
- **Padronização** de processos
- **Testes automatizados** garantem estabilidade
- **Ambiente** idêntico entre dev/prod

#### **💰 Eficiência Operacional**
- **Redução de erros humanos**
- **Economia** de recursos de TI
- **Escalabilidade** sob demanda

### Impacto Final

Esta arquitetura representa uma implementação **enterprise-grade** de DevOps, combinando **Infrastructure as Code**, **Continuous Integration/Deployment**, e **Cloud-native services**. O resultado é uma **solução moderna, escalável e maintível** que permite à equipe focar na **inovação do negócio** ao invés de tarefas operacionais repetitivas.

**🎯 Transformação Digital**: Estabelece base sólida para crescimento e evolução contínua da plataforma OdontoPrev.

---

## 🔧 Pré-requisitos para Reprodução

### 1. Contas e Acessos
- **Azure Subscription** ativa (Azure for Students ou similar)
- **Azure DevOps** account gratuita
- **Credenciais Oracle** da FIAP (RM + senha)

### 2. Ferramentas Locais (Opcional)
- **Visual Studio 2022** ou **VS Code**
- **.NET 8 SDK**
- **Git**

---

## 🚀 Guia de Execução da Pipeline

### Passo 1: Fork do Repositório

1. Faça **fork** deste repositório para sua conta GitHub
2. Clone o fork para sua máquina local (opcional)

```bash
git clone https://github.com/[SEU-USUARIO]/api_dotnet.git
cd api_dotnet
```

### Passo 2: Configuração Azure DevOps

#### 2.1 Criar Projeto
1. Acesse [dev.azure.com](https://dev.azure.com)
2. Crie um novo projeto: **"OdontoPrev-API"**
3. Importe o repositório GitHub

#### 2.2 Configurar Service Connection
1. **Project Settings** → **Service connections**
2. **+ New service connection** → **Azure Resource Manager**
3. Configurar:
   - **Connection name**: `Azure-Connection-[SEU-RM]`
   - **Subscription**: Sua subscription Azure
   - Marcar: "Grant access permission to all pipelines"

### Passo 3: Personalizar Pipeline YAML

#### 3.1 Editar Variáveis
No arquivo `azure-pipelines.yml`, substitua:

```yaml
variables:
  # ALTERAR ESTES VALORES:
  resourceGroup: 'rg-odontoprev-[SEU-RM]'     # Ex: rg-odontoprev-553241
  appServicePlan: 'plan-odontoprev-[SEU-RM]'   # Ex: plan-odontoprev-553241
  appName: 'app-odontoprev-[SEU-RM]'           # Ex: app-odontoprev-553241
  oracleConnectionString: 'Data Source=//oracle.fiap.com.br:1521/orcl;User Id=[SEU-RM];Password=[SUA-SENHA];'
```

#### 3.2 Configurar Service Connection
Substitua todas as ocorrências de:
```yaml
azureSubscription: '[NOME-DA-SUA-CONEXAO-AZURE]'
```
Por:
```yaml
azureSubscription: 'Azure-Connection-[SEU-RM]'
```

### Passo 4: Executar Pipeline

1. **Pipelines** → **+ New pipeline**
2. **Azure Repos Git** → Selecionar repositório
3. **Existing Azure Pipelines YAML file**
4. Selecionar `/azure-pipelines.yml`
5. **Save and run**

### Passo 5: Monitorar Execução

A pipeline executará 3 estágios:
- ✅ **Infraestrutura** (~3 min): Cria Resource Group e App Service Plan
- ✅ **Build** (~5 min): Compila aplicação .NET 8
- ✅ **Deploy** (~4 min): Cria Web App e faz deploy

---

## 🧪 Testes da API

### URLs de Acesso

Após deploy bem-sucedido:
- **API Base**: `https://app-odontoprev-[SEU-RM].azurewebsites.net`
- **Swagger**: `https://app-odontoprev-[SEU-RM].azurewebsites.net/swagger`

### Endpoints Principais

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/pacientes` | Lista todos os pacientes |
| POST | `/api/pacientes` | Cria novo paciente |
| GET | `/api/pacientes/{id}` | Busca paciente por ID |
| PUT | `/api/pacientes/{id}` | Atualiza paciente |
| DELETE | `/api/pacientes/{id}` | Remove paciente |
| GET | `/api/dentistas` | Lista todos os dentistas |
| POST | `/api/consultas` | Agenda nova consulta |

---

## 📄 Scripts JSON para Testes CRUD

### 1. Criar Paciente (POST)

**Endpoint**: `POST /api/pacientes`

```json
{
  "nome": "João Silva Santos",
  "cpf": "123.456.789-01",
  "email": "joao.silva@email.com",
  "telefone": "(11) 99999-8888",
  "dataNascimento": "1985-05-15",
  "endereco": {
    "logradouro": "Rua das Flores, 123",
    "bairro": "Centro",
    "cidade": "São Paulo",
    "cep": "01234-567",
    "uf": "SP"
  },
  "convenio": {
    "numero": "12345678901",
    "plano": "Premium",
    "validade": "2025-12-31"
  }
}
```

### 2. Atualizar Paciente (PUT)

**Endpoint**: `PUT /api/pacientes/{id}`

```json
{
  "id": 1,
  "nome": "João Silva Santos",
  "cpf": "123.456.789-01",
  "email": "joao.novo@email.com",
  "telefone": "(11) 88888-7777",
  "dataNascimento": "1985-05-15",
  "endereco": {
    "logradouro": "Rua das Palmeiras, 456",
    "bairro": "Vila Madalena",
    "cidade": "São Paulo",
    "cep": "05678-901",
    "uf": "SP"
  }
}
```

### 3. Criar Dentista (POST)

**Endpoint**: `POST /api/dentistas`

```json
{
  "nome": "Dra. Maria Oliveira",
  "cro": "SP-12345",
  "especialidade": "Ortodontia",
  "email": "dra.maria@odontoprev.com",
  "telefone": "(11) 3333-4444",
  "horarioAtendimento": {
    "segundaQuinta": "08:00-18:00",
    "sextaFeira": "08:00-16:00",
    "sabado": "08:00-12:00"
  }
}
```

### 4. Agendar Consulta (POST)

**Endpoint**: `POST /api/consultas`

```json
{
  "pacienteId": 1,
  "dentistaId": 1,
  "dataHora": "2024-12-15T14:30:00",
  "tipo": "Consulta",
  "procedimento": "Limpeza e avaliação geral",
  "observacoes": "Paciente com sensibilidade nos dentes posteriores",
  "valor": 150.00,
  "status": "Agendada"
}
```

### 5. Criar Procedimento (POST)

**Endpoint**: `POST /api/procedimentos`

```json
{
  "nome": "Canal do dente 36",
  "descricao": "Tratamento endodôntico completo",
  "valor": 800.00,
  "sessoes": 3,
  "duracao": 90,
  "categoria": "Endodontia"
}
```

---

## 🧪 Sequência de Testes Recomendada

### Teste 1: Verificar API Online
```bash
curl -X GET "https://app-odontoprev-[SEU-RM].azurewebsites.net/api/health"
```

### Teste 2: Listar Dados (GET)
1. `GET /api/pacientes` - Deve retornar lista (pode estar vazia)
2. `GET /api/dentistas` - Deve retornar lista de dentistas
3. `GET /api/consultas` - Deve retornar lista de consultas

### Teste 3: Criar Dados (POST)
1. Criar um dentista usando o JSON acima
2. Criar um paciente usando o JSON acima
3. Agendar uma consulta entre eles

### Teste 4: Atualizar e Excluir
1. `PUT /api/pacientes/{id}` - Atualizar dados do paciente
2. `DELETE /api/consultas/{id}` - Cancelar consulta
3. `GET /api/pacientes/{id}` - Verificar atualização

---

## 🔍 Verificação de Funcionalidades

### ✅ Checklist de Testes

- [ ] **Pipeline executou com sucesso** (3 estágios verdes)
- [ ] **API responde** na URL base
- [ ] **Swagger acessível** e carregando endpoints
- [ ] **GET** retorna dados do Oracle
- [ ] **POST** cria novos registros
- [ ] **PUT** atualiza registros existentes  
- [ ] **DELETE** remove registros
- [ ] **Validação** de dados funciona
- [ ] **Connection String Oracle** configurada corretamente

### 🐛 Troubleshooting

**Erro 500 - Internal Server Error**
- Verificar connection string Oracle no Azure Portal
- Checar logs: App Service → Log stream

**Erro de Connection Timeout**
- Validar credenciais Oracle (RM + senha)
- Testar conectividade com o banco FIAP

**Pipeline falha no Deploy**
- Verificar service connection Azure
- Nome do app deve ser único globalmente

---

## 📊 Monitoramento e Logs

### Azure Portal
1. **Resource Group**: `rg-odontoprev-[SEU-RM]`
2. **App Service**: Monitorar CPU, memória, requests
3. **Log Stream**: Ver logs da aplicação em tempo real

### Métricas Importantes
- **Response Time**: < 2 segundos
- **Availability**: > 99%
- **Error Rate**: < 1%

---

## 🚀 Deploy Manual (Alternativo)

Se preferir deploy local para testes:

```bash
# 1. Restaurar dependências
dotnet restore

# 2. Configurar connection string
export ConnectionStrings__OracleConnection="Data Source=//oracle.fiap.com.br:1521/orcl;User Id=[RM];Password=[SENHA];"

# 3. Executar aplicação
dotnet run

# 4. Acessar Swagger
# http://localhost:5000/swagger
```

---

## 📞 Suporte

Para dúvidas ou problemas:
1. Verificar logs da pipeline no Azure DevOps
2. Consultar documentação oficial:
   - [Azure App Service](https://docs.microsoft.com/azure/app-service/)
   - [Azure DevOps](https://docs.microsoft.com/azure/devops/)
3. Revisar connection string e credenciais Oracle

---

## 📄 Estrutura do Projeto

```
api_dotnet/
├── Controllers/           # Controladores da API
├── Models/               # Modelos de dados
├── Services/             # Lógica de negócio
├── Data/                 # Contexto do Oracle
├── azure-pipelines.yml   # Pipeline CI/CD
├── README.md            # Este arquivo
└── Scripts/             # Scripts SQL e JSON
```

**🎯 Resultado Esperado**: API .NET 8 funcional no Azure, conectada ao Oracle, com deploy automatizado e documentação Swagger completa.
