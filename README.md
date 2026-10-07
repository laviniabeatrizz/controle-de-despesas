Controle de Despesas Pessoais

Integrantes: Lavínia Beatriz
Disciplina: Programação Web
Unidade: I
Turma: Ciência da Computação - 6º período

Sobre o projeto

Este projeto foi desenvolvido com o objetivo de controlar despesas pessoais de forma simples. A aplicação permite cadastrar gastos, acompanhar o que já foi pago e o que ainda está pendente. Os dados ficam armazenados apenas em memória, portanto, ao recarregar a página, as informações são perdidas.

Funcionalidades

- Exibe o total de despesas, a quantidade de pendentes e a quantidade de pagas.
- Permite cadastrar uma nova despesa com descrição, valor, categoria, forma de pagamento, status e data.
- Lista as despesas cadastradas em formato de cards.
- Permite buscar despesas por descrição e filtrar por status.
- Permite alterar o status de uma despesa entre Pendente e Pago.
- Exibe os detalhes completos de uma despesa.
- Realiza o carregamento inicial dos dados de forma assíncrona, simulando uma busca.

Tecnologias utilizadas

Foram utilizados HTML, CSS e JavaScript puro. Nenhuma biblioteca ou framework externo foi empregado.

Estrutura do projeto

index.html        - estrutura da página
css/style.css     - estilos e responsividade
js/app.js         - lógica, eventos, validação e programação assíncrona
README.md         - documentação do projeto

Como executar

Basta abrir o arquivo index.html em qualquer navegador. Não é necessário instalar nada nem executar servidor.

Histórico de desenvolvimento

O projeto foi dividido em etapas, cada uma registrada em uma branch separada:

- Estrutura inicial do HTML, com header, dashboard, formulário, listagem e detalhes.
- Estilização com CSS, incluindo responsividade e foco visível.
- Implementação da lógica em JavaScript para renderizar a lista e o dashboard.
- Validação do formulário com mensagens de erro.
- Busca por descrição e filtro por status.
- Visualização de detalhes e alteração de status.
- Carregamento assíncrono dos dados iniciais.

As branches utilizadas foram: main, feature/formulario, feature/listagem, feature/filtros e feature/dashboard.

As principais dificuldades encontradas foram a delegação de eventos nos botões gerados dinamicamente e a atualização da interface sem recarregar a página. Ambas foram resolvidas com o uso de event.target.closest e chamadas à função de atualização após cada mudança.

Decisões técnicas

1. Uso de cards em vez de tabela. Em telas menores, os cards se adaptam melhor e facilitam a leitura das informações.

2. Validação feita em JavaScript. O enunciado solicita que a validação não dependa apenas do atributo required do HTML. Além disso, validar em JavaScript permite mensagens de erro personalizadas e maior controle sobre o fluxo.

3. Renderização separada da lógica dos dados. As funções de renderização apenas leem o array de despesas e atualizam o DOM, o que facilita a manutenção do código.

4. Delegação de eventos. Em vez de adicionar um listener para cada botão da lista, foi adicionado um único listener na lista, que funciona inclusive para botões criados depois.

Programação assíncrona

1. Onde existe programação assíncrona?
Na função carregarDespesas, chamada pela função iniciar.

2. Qual operação ela representa?
Representa a busca inicial das despesas. Como não há servidor, a operação é simulada com setTimeout de 1 segundo.

3. Onde são utilizados Promise, async e await?
Promise: dentro de carregarDespesas, que retorna uma promessa resolvida após 1 segundo.
async: na função iniciar, declarada como async function.
await: dentro de iniciar, aguardando o resultado de carregarDespesas.

4. O que aparece na interface enquanto a operação é realizada?
Aparece a mensagem "Carregando despesas..." no elemento de carregamento, que é ocultado quando os dados chegam.

Limitações e melhorias futuras

O sistema ainda não faz:
- Persistência dos dados. Ao recarregar a página, tudo é perdido.
- Login ou autenticação de usuários.
- Integração com API real ou banco de dados.
- Edição completa de uma despesa. Apenas o status pode ser alterado.
- Exportação de relatórios.

Com mais tempo, seria interessante adicionar:
- Armazenamento local (localStorage) para persistir os dados.
- Autenticação simples.
- Integração com uma API real.
- Gráficos de gastos por categoria.

Uso de IA

A IA foi utilizada apenas como apoio durante o desenvolvimento, principalmente para revisão do código e testes. Todo o conteúdo sugerido foi analisado, compreendido e adaptado antes de ser incluído no projeto.

Data: 06/10/2026
Modelo: Assistente de IA
Prompt: Revisão do código com o objetivo de identificar erros de sintaxe e possíveis melhorias.
Onde foi usado: Revisão do HTML, do CSS e do JavaScript.



Data: 07/10/2026
Modelo: Assistente de IA
Prompt: Auxílio na organização do README conforme as orientações da atividade.
Onde foi usado: Documentação do projeto.

Todas as sugestões foram revisadas e adaptadas ao contexto do projeto. 