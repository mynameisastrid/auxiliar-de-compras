Controle de Mercado

Sobre o Projeto

O Controle de Mercado é uma aplicação web de página única (SPA - Single Page Application) desenvolvida para auxiliar no gerenciamento de compras de supermercado. O sistema permite que o usuário defina um orçamento inicial, adicione produtos ao carrinho (por unidade ou peso), acompanhe o valor total gasto em tempo real e gere um comprovante de compra em formato de imagem para compartilhamento.

O projeto foi construído em um único arquivo HTML, encapsulando a estrutura, a estilização e a lógica de funcionamento, garantindo facilidade de execução e portabilidade.

Funcionalidades

Controle de Orçamento: Definição de limite de gastos com barra de progresso visual que indica a porcentagem consumida e alerta sobre saldo restante ou excedido.

Gestão de Itens: Inserção de produtos informando nome, quantidade e valor unitário.

Suporte a Produtos Pesáveis: Opção para alternar a entrada de itens, permitindo especificar o peso em quilogramas (kg) ou gramas (g).

Cálculo Automático: Atualização instantânea da quantidade total de itens, contagem de produtos e soma do valor final do carrinho.

Configuração de Recibo: Personalização dos dados do estabelecimento (nome e endereço) e inclusão de informações sobre a divisão da compra.

Geração e Compartilhamento de Recibo: Conversão dos dados do carrinho em um recibo visual (estilo cupom fiscal) exportado em formato PNG. Utiliza a Web Share API para envio direto via WhatsApp em dispositivos móveis ou fallback para download em desktops.

Persistência de Dados: Salvamento automático das informações (orçamento, configurações de recibo e lista de itens) no navegador através da API localStorage.

Notificações (Toast): Sistema de alertas não intrusivos para feedback ao usuário (ex: erros de validação, sucesso ao baixar a imagem).

Tecnologias Utilizadas

HTML5: Semântica e estruturação da interface.

CSS3: Estilização utilizando variáveis nativas (Custom Properties), Flexbox, Grid Layout e animações. Interface responsiva com design moderno.

JavaScript (Vanilla): Lógica de manipulação do DOM, cálculos matemáticos, formatação de moeda, integração com Web APIs (localStorage, Web Share API).

Dependências

A aplicação utiliza uma biblioteca externa carregada via CDN para a renderização do recibo em formato de imagem:

html2canvas (v1.4.1): Utilizada na função shareWhatsApp() para capturar o elemento HTML do recibo renderizado em background e convertê-lo em um elemento Canvas, possibilitando a extração em formato PNG.

Como Usar

Por ser uma aplicação baseada inteiramente no lado do cliente (Client-side), não há necessidade de configuração de ambiente, servidores ou processos de build.

Faça o clone ou o download deste repositório.

Abra o arquivo index.html em qualquer navegador web moderno.

A aplicação estará pronta para uso. Os dados inseridos serão mantidos no armazenamento local do navegador mesmo após o fechamento da aba.

Estrutura do Código

O arquivo index.html está dividido em três seções principais:

1. CSS (Estilos)

Define o tema escuro da aplicação através de variáveis de raiz (:root). Utiliza Grid e Flexbox para o alinhamento de formulários e listas. Inclui regras específicas para a renderização do layout do recibo visual (.receipt-wrap), simulando um papel impresso com bordas serrilhadas via propriedades de background e gradientes.

2. HTML (Estrutura)

Composto por seções encapsuladas na classe .section-box. Inclui o cabeçalho com o total geral, bloco de definição de orçamento, formulário de configurações do recibo, formulário de entrada de itens (com toggle para habilitar campos de peso), lista de exibição do carrinho e uma barra de resumo inferior afixada (.summary-bar). O container de notificações (#toast-container) é posicionado de forma absoluta.

3. JavaScript (Lógica)

Gerenciamento de Estado: O array global items armazena os produtos. A variável pesoOn controla a exibição do formulário de peso.

Funções de Entrada: onCurrencyInput aplica uma máscara de moeda brasileira em tempo real nos campos numéricos.

Operações CRUD: addItem valida os dados do formulário e insere o objeto no array. removeItem exclui itens pelo índice.

Renderização: renderList atualiza a interface iterando sobre o array items e chamando a função updateBudget para recálculo do orçamento.

Exportação (html2canvas): A função shareWhatsApp cria um elemento DOM temporário oculto preenchido pela função getReceiptHTML, converte este elemento em Canvas usando a biblioteca externa, gera um Blob (PNG) e aciona a Web Share API ou o download.

Storage: saveData converte o estado atual em JSON e armazena. loadData é executada no carregamento da janela (window.onload) para restaurar a sessão anterior.
