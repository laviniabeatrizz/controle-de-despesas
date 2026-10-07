Controle de Despesas Pessoais

Identificação

Nome do projeto: Controle de Despesas Pessoais
Integrantes: Lavínia Beatriz
Disciplina: Programação Web
Unidade: I (front-end)
Turma: [coloque sua turma aqui]

Descrição

O sistema resolve o problema de controlar gastos pessoais de forma simples. O usuário registra suas despesas, informa valor, categoria, forma de pagamento, status e data, e consegue visualizar um resumo do que já foi pago e do que ainda está pendente.

O público-alvo são pessoas que querem organizar melhor o dinheiro no dia a dia, sem precisar de planilhas complicadas.

A aplicação roda inteiramente no navegador. Os dados ficam em memória, pois o foco da avaliação é o domínio de HTML, CSS e JavaScript.

Funcionalidades

Dashboard com total de despesas, pendentes e pagas, calculado dinamicamente pelo JavaScript.
Cadastro de novas despesas com validação em JavaScript.
Listagem de despesas em formato de cards.
Busca textual por descrição.
Filtro por status (Pendente ou Pago).
Alteração de status com um clique.
Visualização de detalhes completos de uma despesa.
Carregamento inicial assíncrono simulando busca de dados.

Tecnologias

HTML5 para a estrutura semântica da página.
CSS3 para layout, cores, espaçamento e responsividade.
JavaScript para comportamento, DOM, eventos, validação e programação assíncrona.
Git e GitHub para versionamento e hospedagem do código.

Não foi utilizada nenhuma biblioteca ou framework externo. Tudo foi feito com HTML, CSS e JavaScript puros, conforme pedido no enunciado.

Estrutura do projeto

controle-de-despesas/
  index.html          -> estrutura da página
  css/
    style.css         -> estilos e responsividade
  js/
    app.js            -> lógica, DOM, eventos, validação e async
  README.md           -> documentação do projeto

O index.html contém o header, o dashboard, o formulário de cadastro, a listagem, a seção de detalhes e o footer.
O css/style.css cuida da apresentação, incluindo foco visível e layout responsivo.
O js/app.js contém os dados em memória, as funções de renderização, validação, eventos e o carregamento assíncrono.

Como executar

1. Baixe ou clone o repositório:
   git clone https://github.com/laviniabeatrizz/controle-de-despesas.git

2. Abra a pasta do projeto.

3. Dê um duplo clique em index.html ou abra com o navegador de sua preferência.

4. A aplicação já estará funcionando. Aguarde 1 segundo para o carregamento inicial das despesas.

Não é necessário instalar nada, nem rodar servidor. Basta abrir o index.html.

Histórico de desenvolvimento

O projeto foi dividido em etapas:

1. Estrutura HTML: criação do header, dashboard, formulário, listagem e detalhes.
2. Estilos CSS: layout, cores, responsividade e foco visível.
3. Lógica JavaScript: dados em memória, renderização da lista e do dashboard.
4. Validação: checagem dos campos do formulário com mensagens de erro.
5. Busca e filtro: filtragem dinâmica por descrição e status.
6. Detalhes e alteração de status: interação com os cards da listagem.
7. Programação assíncrona: simulação de carregamento inicial com Promise e async/await.

Branches utilizadas:

main, versão estável.
feature/formulario.
feature/listagem.
feature/filtros.
feature/dashboard.

Principais decisões: usar cards em vez de tabela, separar a renderização da lógica dos dados e manter a validação no JavaScript, como pedido no enunciado.

Dificuldades encontradas: fazer a delegação de eventos funcionar corretamente nos botões gerados dinamicamente e manter a interface atualizada sem recarregar a página.

Decisões técnicas

1. Cards em vez de tabela. Em telas pequenas, cards se adaptam melhor e são mais fáceis de ler. Cada despesa tem seu próprio bloco com informações e botões.

2. Validação no JavaScript. O enunciado pede que a validação não dependa apenas do atributo required do HTML. Além disso, validar no JavaScript permite mensagens de erro personalizadas e controle total do fluxo.

3. Renderização separada da lógica dos dados. As funções renderizarLista e atualizarDashboard apenas leem o array de despesas e atualizam o DOM. Isso facilita manutenção e evita misturar regra de negócio com interface.

4. Delegação de eventos. Em vez de adicionar um listener em cada botão da lista, foi adicionado um único listener na lista. Isso funciona mesmo para botões criados depois e deixa o código mais limpo.

Programação assíncrona

1. Onde existe programação assíncrona?
Na função carregarDespesas, chamada por iniciar.

2. Qual operação ela representa?
Representa a busca inicial das despesas. Como não há servidor, a operação é simulada com setTimeout de 1 segundo.

3. Onde são utilizados Promise, async e await?
Promise: dentro de carregarDespesas, que retorna uma promessa resolvida após 1 segundo.
async: na função iniciar, declarada como async function.
await: dentro de iniciar, esperando o resultado de carregarDespesas.

4. O que aparece na interface enquanto a operação está sendo realizada?
Aparece a mensagem "Carregando despesas..." no elemento carregando, que depois é escondido quando os dados chegam.

Limitações e melhorias futuras

O sistema ainda não faz:

Persistência dos dados. Ao recarregar a página, tudo se perde.
Login ou autenticação de usuários.
Integração com API real ou banco de dados.
Edição completa de uma despesa. Só o status pode ser alterado.
Exportação de relatórios.
Notificações de contas a vencer.

Com mais tempo, seria interessante adicionar:

Banco de dados ou localStorage para persistir os dados.
Autenticação simples.
Integração com uma API real.
Gráficos de gastos por categoria.
Níveis de acesso, como administrador e usuário comum.

Uso de IA

Data: 07/10/2026
Modelo: Assistente de IA
Prompt: Revisar o código e sugerir melhorias de semântica e acessibilidade.
Onde foi usado: Revisão do HTML e do JavaScript.

Data: 07/10/2026
Modelo: Assistente de IA
Prompt: Ajuda para montar o README conforme o enunciado.
Onde foi usado: Documentação.

O código sugerido foi revisado e adaptado. As sugestões foram aplicadas apenas quando fizeram sentido para o projeto. Toda a lógica foi compreendida e testada antes da entrega.