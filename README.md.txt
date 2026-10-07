// ---------- DADOS (ficam só na memória) ----------
let despesas = [];
let proximoId = 1;

const dadosIniciais = [
  { id: 1, descricao: "Almoço", valor: 25.5, categoria: "Alimentação", pagamento: "Pix", status: "Pago", data: "2026-10-01" },
  { id: 2, descricao: "Conta de luz", valor: 120, categoria: "Contas", pagamento: "Cartão", status: "Pendente", data: "2026-10-05" }
];

// Valores permitidos (usados na validação)
const categorias = ["Alimentação", "Transporte", "Lazer", "Contas"];
const pagamentos = ["Dinheiro", "Pix", "Cartão"];
const statusValidos = ["Pendente", "Pago"];

// ---------- ASSÍNCRONO: simula o carregamento inicial ----------
function carregarDespesas() {
  return new Promise((resolve) => {
    setTimeout(() => resolve(dadosIniciais), 1000);
  });
}

async function iniciar() {
  try {
    const dados = await carregarDespesas();
    despesas = dados;
    proximoId = dados.length + 1;
    document.getElementById("carregando").hidden = true;
    document.getElementById("dashboard").hidden = false;
    document.getElementById("listagem").hidden = false;
    atualizarTela();
  } catch (erro) {
    document.getElementById("carregando").textContent = "Erro ao carregar despesas.";
  }
}

// ---------- DASHBOARD ----------
function atualizarDashboard() {
  const pendentes = despesas.filter((d) => d.status === "Pendente").length;
  const pagas = despesas.filter((d) => d.status === "Pago").length;
  document.getElementById("total").textContent = despesas.length;
  document.getElementById("pendentes").textContent = pendentes;
  document.getElementById("pagas").textContent = pagas;
}

// ---------- LISTAGEM + BUSCA/FILTRO ----------
function formatarValor(v) {
  return "R$ " + Number(v).toFixed(2).replace(".", ",");
}

function criarBotao(texto, acao, id) {
  const botao = document.createElement("button");
  botao.type = "button";
  botao.textContent = texto;
  botao.dataset.acao = acao;
  botao.dataset.id = id;
  return botao;
}

function renderizarLista() {
  const busca = document.getElementById("busca").value.toLowerCase();
  const filtro = document.getElementById("filtro-status").value;
  const lista = document.getElementById("lista");
  lista.innerHTML = "";

  const visiveis = despesas.filter((d) => {
    const combinaTexto = d.descricao.toLowerCase().includes(busca);
    const combinaStatus = filtro === "" || d.status === filtro;
    return combinaTexto && combinaStatus;
  });

  if (visiveis.length === 0) {
    const vazio = document.createElement("li");
    vazio.textContent = "Nenhuma despesa encontrada.";
    lista.appendChild(vazio);
    return;
  }

  visiveis.forEach((d) => {
    const item = document.createElement("li");
    item.className = d.status.toLowerCase();

    const titulo = document.createElement("strong");
    titulo.textContent = d.descricao;

    const resumo = document.createElement("p");
    resumo.textContent = formatarValor(d.valor) + " — " + d.status;

    const textoStatus = d.status === "Pendente" ? "Marcar como pago" : "Marcar como pendente";

    item.appendChild(titulo);
    item.appendChild(resumo);
    item.appendChild(criarBotao(textoStatus, "status", d.id));
    item.appendChild(criarBotao("Ver detalhes", "detalhes", d.id));

    lista.appendChild(item);
  });
}

function atualizarTela() {
  atualizarDashboard();
  renderizarLista();
}

// ---------- VALIDAÇÃO ----------
function mostrarErro(campo, mensagem) {
  document.getElementById("erro-" + campo).textContent = mensagem;
}

function validar() {
  let valido = true;

  const descricao = document.getElementById("descricao").value.trim();
  const valor = document.getElementById("valor").value;
  const categoria = document.getElementById("categoria").value;
  const pagamento = document.getElementById("pagamento").value;
  const status = document.getElementById("status").value;
  const data = document.getElementById("data").value;

  ["descricao", "valor", "categoria", "pagamento", "status", "data"].forEach((c) => mostrarErro(c, ""));

  if (descricao === "") {
    mostrarErro("descricao", "Informe a descrição.");
    valido = false;
  } else if (descricao.length < 3) {
    mostrarErro("descricao", "A descrição precisa ter pelo menos 3 letras.");
    valido = false;
  }

  if (valor === "" || Number(valor) <= 0) {
    mostrarErro("valor", "Informe um valor maior que zero.");
    valido = false;
  }

  if (!categorias.includes(categoria)) {
    mostrarErro("categoria", "Escolha uma categoria.");
    valido = false;
  }

  if (!pagamentos.includes(pagamento)) {
    mostrarErro("pagamento", "Escolha a forma de pagamento.");
    valido = false;
  }

  if (!statusValidos.includes(status)) {
    mostrarErro("status", "Escolha o status.");
    valido = false;
  }

  if (data === "") {
    mostrarErro("data", "Informe a data.");
    valido = false;
  }

  return valido;
}

// ---------- DETALHES ----------
function mostrarDetalhes(despesa) {
  const dl = document.getElementById("detalhes-lista");
  dl.innerHTML = "";

  const campos = [
    ["Descrição", despesa.descricao],
    ["Valor", formatarValor(despesa.valor)],
    ["Categoria", despesa.categoria],
    ["Pagamento", despesa.pagamento],
    ["Status", despesa.status],
    ["Data", despesa.data]
  ];

  campos.forEach(([termo, valor]) => {
    const dt = document.createElement("dt");
    dt.textContent = termo;

    const dd = document.createElement("dd");
    dd.textContent = valor;

    dl.appendChild(dt);
    dl.appendChild(dd);
  });

  document.getElementById("detalhes").hidden = false;
}

// ---------- EVENTOS ----------
document.getElementById("formulario").addEventListener("submit", (evento) => {
  evento.preventDefault();
  if (!validar()) return;

  despesas.push({
    id: proximoId++,
    descricao: document.getElementById("descricao").value.trim(),
    valor: Number(document.getElementById("valor").value),
    categoria: document.getElementById("categoria").value,
    pagamento: document.getElementById("pagamento").value,
    status: document.getElementById("status").value,
    data: document.getElementById("data").value
  });

  evento.target.reset();
  atualizarTela();
});

document.getElementById("busca").addEventListener("input", renderizarLista);
document.getElementById("filtro-status").addEventListener("change", renderizarLista);

// Delegação de eventos na lista
document.getElementById("lista").addEventListener("click", (evento) => {
  const botao = evento.target.closest("button");
  if (!botao) return;

  const despesa = despesas.find((d) => d.id === Number(botao.dataset.id));
  if (!despesa) return;

  if (botao.dataset.acao === "status") {
    despesa.status = despesa.status === "Pendente" ? "Pago" : "Pendente";
    atualizarTela();
  } else if (botao.dataset.acao === "detalhes") {
    mostrarDetalhes(despesa);
  }
});

document.getElementById("fechar-detalhes").addEventListener("click", () => {
  document.getElementById("detalhes").hidden = true;
});

iniciar();