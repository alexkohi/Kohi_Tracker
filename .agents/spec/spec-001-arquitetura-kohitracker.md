# Arquitetura do Sistema: KohiTracker

## Estilo Arquitetural
O KohiTracker será projetado no modelo Cliente-Servidor e estruturado internamente com base nos princípios do Domain-Driven Design (DDD). Isso visa isolar claramente as regras de negócio complexas do catálogo das tecnologias de interface ou persistência.

## Organização em Camadas (DDD)
* **Camada de Apresentação (UI):** Interface Web responsável por interagir com o usuário, coletar os dados do catálogo e renderizar o perfil.
* **Camada de Aplicação:** Responsável por orquestrar os Casos de Uso (ex: `AdicionarMidiaAoCatalogo`, `AtualizarPerfil`), delegando o processamento aos objetos do domínio.
* **Camada de Domínio:** O coração arquitetural do sistema. Contém todas as regras de negócio intrínsecas ao problema modelado, incluindo entidades (`Usuario`, `Midia`, `RegistroCatalogo`, `Avaliacao`), objetos de valor e agregações independentes de framework.
* **Camada de Infraestrutura:** Cuida do acesso a dados, provendo integrações com o Banco de Dados (onde serão salvos os perfis e listas) e a comunicação HTTP com as APIs externas de filmes/jogos.

## Fluxo de Dados e Persistência
O sistema trabalhará com a separação estrutural entre os **Dados Globais (Mídias)** — que servem como catálogos fixos de leitura vindos de integrações — e os **Dados Pessoais (Registros de Catálogo)** — informações geradas pelo usuário sobre as entidades globais.
