# Sprint II — Justificativas das Decisões de Modelagem

**Projeto:** KohiTracker
**Etapa:** Engenharia de Software — Sprint II

---

## 1. Introdução

A modelagem do KohiTracker foi desenvolvida considerando princípios de orientação a objetos, buscando estabelecer uma estrutura organizada, coesa e extensível.

As decisões foram fundamentadas nos conceitos de UML, princípios SOLID e padrões GRASP, visando reduzir o acoplamento entre as classes, evitar duplicação de responsabilidades e facilitar a evolução do sistema.

## 2. Separação de Responsabilidades (SRP — SOLID)

A separação entre as classes Usuario e Perfil foi adotada para estabelecer responsabilidades distintas dentro do sistema.

A classe Usuario concentra informações relacionadas à conta, autenticação e segurança, enquanto a classe Perfil gerencia informações de identidade visual e personalização, como apelido, avatar, banner e biografia.

Essa separação contribui para a coesão das classes e facilita a manutenção e evolução independente de suas funcionalidades.

## 3. Especialista na Informação (GRASP)

O método calcularMediaAvaliacoes() foi associado à classe Midia, pois ela representa a obra dentro do catálogo global e é o elemento ao qual as avaliações estão vinculadas.

A centralização desse comportamento permite que a média seja obtida a partir das avaliações relacionadas à mídia, evitando a duplicação da lógica de cálculo em diferentes partes do sistema.

## 4. Criador (GRASP) e Classe Associativa

A classe RegistroCatalogo foi introduzida para representar a relação entre Usuario e Midia.

Essa decisão permite armazenar informações particulares do consumo, como status, progresso, plataforma utilizada e datas de início e conclusão.

A utilização dessa classe evita que informações individuais sejam armazenadas diretamente na entidade global Midia ou concentradas na classe Usuario.

Além disso, possibilita que o sistema mantenha registros independentes para diferentes usuários que consomem a mesma obra.

## 5. Polimorfismo e Herança

A classe abstrata Midia concentra os atributos e comportamentos comuns às diferentes categorias de conteúdo.

As subclasses Jogo, Livro, Filme, Serie, Anime e Manga especializam essa estrutura conforme suas características particulares.

O polimorfismo permite que o sistema manipule diferentes tipos de mídia por meio de uma referência comum à classe Midia, reduzindo a necessidade de tratamentos específicos para cada categoria.

Essa decisão também facilita a expansão futura do sistema, permitindo a inclusão de novas categorias sem modificar a estrutura fundamental do catálogo.

## 6. Encapsulamento e Enumeração

A utilização da enumeração StatusConsumo restringe os estados possíveis de um registro pessoal.

Essa abordagem evita valores inconsistentes e facilita a implementação de regras de negócio relacionadas à alteração de status e progresso.

O encapsulamento dos atributos permite que alterações sejam realizadas por meio de métodos específicos, possibilitando validações e preservando a consistência dos dados.

## 7. Composição

A composição foi utilizada nas relações em que existe dependência de ciclo de vida entre os elementos.

### Usuario e Perfil

O perfil pertence exclusivamente a uma conta e não possui existência independente dentro do domínio da aplicação.

### Perfil e HallDestaque

O HallDestaque representa uma parte da estrutura de personalização do perfil, sendo dependente deste para existir.

### Usuario e RegistroCatalogo

Os registros do catálogo são particulares de cada usuário. Caso uma conta seja removida, seus registros pessoais também poderão ser excluídos, sem afetar as mídias globais.

### RegistroCatalogo e Avaliacao

A avaliação está vinculada ao registro pessoal de consumo, sendo dependente dele dentro da modelagem proposta.

## 8. Agregação

A agregação foi aplicada entre HallDestaque e Midia.

O HallDestaque organiza referências para diferentes mídias selecionadas pelo usuário, porém essas mídias possuem existência independente no catálogo global.

Assim, a remoção de uma obra do HallDestaque não implica sua exclusão do sistema.

Essa decisão representa o conceito de agregação, no qual os elementos agrupados podem existir independentemente do elemento agregador.

## 9. Associação

A associação entre RegistroCatalogo e Midia representa a vinculação de uma obra ao catálogo pessoal do usuário.

Essa relação permite armazenar informações particulares de consumo sem modificar os dados globais da obra.

A associação entre RegistroCatalogo e Plataforma permite identificar os meios utilizados para consumir determinada mídia.

Já a associação entre Usuario e Avaliacao representa as interações de curtida realizadas pelos usuários sobre avaliações publicadas.

## 10. Extensibilidade e Manutenibilidade

A modelagem foi estruturada visando a evolução incremental do KohiTracker.

A separação entre entidades globais e registros pessoais permite implementar novas funcionalidades, como estatísticas de consumo, histórico, listas personalizadas, conquistas e sistemas de recomendação, sem exigir a reformulação completa do modelo inicial.

A utilização de uma classe abstrata para as mídias também facilita a inclusão de novas categorias de conteúdo.

Dessa maneira, a estrutura proposta busca equilibrar os requisitos atuais do projeto com a possibilidade de expansão futura.

## 11. Considerações Finais

As decisões de modelagem estabelecem uma base conceitual para o desenvolvimento do KohiTracker, priorizando a separação de responsabilidades, a organização das entidades e a clareza dos relacionamentos.

A aplicação dos conceitos de orientação a objetos permite estruturar o sistema de forma que suas funcionalidades possam ser desenvolvidas e ampliadas progressivamente, acompanhando a evolução dos requisitos do projeto.
