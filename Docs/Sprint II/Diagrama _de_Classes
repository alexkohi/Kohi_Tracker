# Sprint II — Diagrama de Classes

**Projeto:** KohiTracker
**Etapa:** Engenharia de Software — Sprint II
**Objetivo:** Definição da estrutura estática do sistema por meio de UML.

---


O diagrama abaixo representa a estrutura conceitual para o sistema.

```mermaid
classDiagram
    class Usuario {
        - UUID id
        - String email
        - String senhaHash
        - DateTime dataCadastro
        + autenticar(email, senha) boolean
        + redefinirSenha(novaSenha) void
    }

    class Perfil {
        - UUID id
        - String apelido
        - String avatarUrl
        - String bannerUrl
        - String biografia
        + atualizarIdentidade(avatar, banner, bio) void
    }

    class HallDestaque {
        - int limiteItens
        + adicionarDestaque(midia) boolean
        + removerDestaque(midia) void
        + reordenarItens() void
    }

    class Midia {
        <<abstract>>
        - UUID id
        - String titulo
        - String sinopse
        - String capaUrl
        - Date dataLancamento
        + obterDetalhes() String
        + calcularMediaAvaliacoes() double
    }

    class Jogo {
        - String desenvolvedora
        - int tempoMedioConclusao
    }

    class Livro {
        - String autor
        - int numeroPaginas
        - String editora
    }

    class Filme {
        - String diretor
        - int duracaoMinutos
    }

    class Serie {
        - String criador
        - int quantidadeTemporadas
    }

    class Anime {
        - String estudio
        - int quantidadeEpisodios
    }

    class Manga {
        - String autor
        - int quantidadeVolumes
    }

    class Plataforma {
        - UUID id
        - String nome
        + obterNome() String
    }

    class RegistroCatalogo {
        - UUID id
        - StatusConsumo status
        - int progressoAtual
        - int progressoTotal
        - String unidadeProgresso
        - Date dataInicio
        - Date dataConclusao
        + atualizarProgresso(novoProgresso) void
        + alterarStatus(novoStatus) void
    }

    class Avaliacao {
        - UUID id
        - float nota
        - String comentario
        - DateTime dataPublicacao
        + editarConteudo(nota, comentario) void
        + registrarCurtida(usuario) void
        + removerCurtida(usuario) void
    }

    class StatusConsumo {
        <<enumeration>>
        PLANEJO
        FAZENDO
        CONCLUIDO
        ABANDONADO
    }

    Usuario "1" *-- "1" Perfil : possui
    Perfil "1" *-- "1" HallDestaque : contem

    HallDestaque "1" o-- "0..*" Midia : destaca

    Usuario "1" *-- "0..*" RegistroCatalogo : mantém
    RegistroCatalogo "*" --> "1" Midia : referencia

    RegistroCatalogo "1" *-- "0..1" Avaliacao : possui

    Usuario "0..*" --> "0..*" Avaliacao : curte

    RegistroCatalogo "*" --> "0..*" Plataforma : utiliza

    RegistroCatalogo --> StatusConsumo : utiliza

    Midia <|-- Jogo
    Midia <|-- Livro
    Midia <|-- Filme
    Midia <|-- Serie
    Midia <|-- Anime
    Midia <|-- Manga
```

## 3. Descrição das Classes

### 3.1. Usuario

Representa a conta de acesso à plataforma, sendo responsável pelas informações de autenticação e identificação do usuário.

### 3.2. Perfil

Representa a identidade pública e personalizada do usuário, contendo informações como apelido, avatar, banner e biografia.

### 3.3. HallDestaque

Representa a seção de mídias em destaque no perfil do usuário, permitindo adicionar, remover e organizar obras selecionadas.

### 3.4. Midia

Classe abstrata responsável por representar as características comuns às obras cadastradas no sistema, como título, sinopse, capa e data de lançamento.

Também centraliza o comportamento relacionado à obtenção de detalhes e cálculo da média das avaliações.

### 3.5. Jogo, Livro, Filme, Serie, Anime e Manga

Representam especializações da classe Midia, contendo atributos específicos de cada categoria.

### 3.6. RegistroCatalogo

Representa a relação entre um usuário e uma mídia, armazenando informações individuais de consumo, como status, progresso, plataforma utilizada e datas de início e conclusão.

### 3.7. Avaliacao

Representa a avaliação publicada pelo usuário sobre uma mídia presente em seu catálogo, permitindo registrar nota, comentário e interações de curtida.

### 3.8. Plataforma

Representa as plataformas utilizadas para consumir determinada mídia, permitindo identificar, por exemplo, se um jogo foi registrado como jogado no PC ou PlayStation.

### 3.9. StatusConsumo

Enumeração responsável por definir os estados possíveis de um registro pessoal: Planejo, Fazendo, Concluído e Abandonado.

---

## 4. Considerações Finais

A estrutura proposta estabelece uma separação entre as informações globais das mídias e os dados particulares de consumo de cada usuário.

Essa organização permite que diferentes usuários acompanhem a mesma obra de maneira independente, mantendo seus próprios registros, avaliações, progressos e preferências.

A utilização de herança e relacionamentos UML também proporciona uma base extensível para a implementação de novas categorias de mídia e funcionalidades futuras.
