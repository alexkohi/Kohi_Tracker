# Domínio do Problema: KohiTracker

## História e Contexto
Atualmente, consumidores de cultura pop e mídias de entretenimento (filmes, séries, livros, animes, mangás e jogos) precisam utilizar múltiplas plataformas para catalogar e acompanhar o que consomem. Serviços como Letterboxd (filmes), MyAnimeList (animes/mangás), Backloggd (jogos) e Goodreads (livros) operam de forma isolada. Isso gera a fragmentação da identidade do usuário, dificultando uma visão unificada dos seus hobbies e a centralização do seu catálogo.

## Objetivos do Sistema
O KohiTracker tem como objetivo fornecer uma aplicação web unificada para concentrar o catálogo de todos os tipos de mídia. O sistema permitirá que o usuário crie um perfil personalizado, busque conteúdos diversos, defina o status de consumo (Planejo, Fazendo, Concluído, Abandonado), avalie, comente e destaque seus favoritos em um único ecossistema.

## Regras de Negócio
1. **Autenticação Obrigatória:** O acesso às funcionalidades de interação e adição ao catálogo exige uma conta de usuário autenticada.
2. **Unicidade no Catálogo:** Um usuário não pode adicionar a mesma obra duas vezes ao seu catálogo; ele deve atualizar o status e o progresso do registro existente.
3. **Pré-requisito de Avaliação:** Apenas usuários que adicionaram a mídia ao seu catálogo pessoal podem atribuir uma nota e publicar uma resenha.
4. **Restrições de Destaque:** O "Hall de Destaques" do perfil possui um limite de itens para manter a integridade visual da interface, segmentados por tipo de mídia.

## Limitações e Restrições
* Inicialmente, a aplicação dependerá de integrações com APIs externas de bases de dados (ex: TMDB, IGDB, Google Books) para popular o catálogo de buscas.
* Mídias que não constam nas bases de dados conectadas não poderão ser adicionadas livremente pelos usuários sem uma curadoria ou aprovação prévia para evitar duplicações e dados inconsistentes.
