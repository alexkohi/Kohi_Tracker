# Arquitetura e Comunicação de Componentes: KohiTracker

## 1. Arquitetura do Sistema
O KohiTracker adota uma **Arquitetura em Camadas (Layered Architecture)** baseada nos princípios de separação de responsabilidades. A estrutura segue o fluxo clássico: `Controller -> Service -> Repository`.

### Responsabilidades dos Componentes

* **Controllers (Camada de Apresentação/API):**
  * **Responsabilidade:** Receber as requisições HTTP do cliente web (GET, POST, PUT, DELETE), extrair os dados (payload JSON), chamar o serviço adequado e retornar as respostas formatadas com os respectivos códigos HTTP (200 OK, 201 Created, 400 Bad Request).
  * **Regra:** Não devem conter regras de negócio, apenas orquestração de entrada e saída.

* **Services (Camada de Aplicação / Domínio):**
  * **Responsabilidade:** Concentrar a lógica e as regras de negócio identificadas no DDD. É o Service que verifica se o usuário já tem um jogo no catálogo antes de tentar adicioná-lo de novo.
  * **Regra:** Conhece as entidades e objetos de valor, mas não sabe como eles são salvos no banco de dados.

* **Repositories (Camada de Infraestrutura):**
  * **Responsabilidade:** Isolar a persistência de dados. O Repositório recebe os objetos montados pelo Service e executa as queries (`INSERT`, `SELECT`, `UPDATE`) no banco de dados relacional (ex: MySQL).
  * **Regra:** Devolve entidades de domínio hidratadas com dados do banco para o Service trabalhar.

## 2. Comunicação e Uso de REST
A comunicação entre o Cliente (Frontend/Navegador) e o Servidor (Backend) será feita via **API RESTful** trafegando dados no formato JSON.
* Para buscar filmes: `GET /api/midias?tipo=filme`
* Para adicionar ao catálogo: `POST /api/catalogo`
* Para atualizar o progresso de leitura/jogo: `PUT /api/catalogo/{id}`

Os componentes internos se comunicam via injeção de dependência. O Controller instancializa e chama métodos do Service, e o Service chama os métodos do Repository.

## 3. Justificativa das Decisões
A escolha pela divisão em Controller-Service-Repository atende perfeitamente ao contexto do KohiTracker porque:
1. **Desacoplamento:** Permite alterar a interface do usuário (fazer um app mobile no futuro) sem precisar reescrever a lógica de gerenciamento de catálogos e avaliações.
2. **Isolamento da Infraestrutura:** O uso de Repositórios garante que, caso o banco de dados mude, as regras contidas nos Services continuarão intactas. 
3. **Mapeamento Direto do DDD:** Os Services orquestram as mudanças de estado dos *Aggregates* mapeados na modelagem de domínio.

## 4. Diagrama de Arquitetura

```mermaid
flowchart TD
    %% Atores e Clientes
    ClienteWeb["Cliente Web"] -->|Requisições HTTP REST (JSON)| Controller

    %% Backend Camadas
    subgraph Backend [Backend API (Arquitetura em Camadas)]
        direction TB
        Controller[Controllers\nValidam inputs e rotas]
        Service[Services\nRegras de Negócio e Domínio]
        Repository[Repositories\nAcesso a Dados abstrato]
        
        Controller -->|Chama métodos| Service
        Service -->|Persiste/Busca Entidades| Repository
    end

    %% Infraestrutura
    Repository -->|Queries SQL| BD[(Banco de Dados\nRelacional)]
    Service -.->|Requisição HTTP| APIExterna[APIs Externas\nTMDB, IGDB]
```
