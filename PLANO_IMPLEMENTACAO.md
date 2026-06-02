<<<<<<< HEAD
# SA_ferrorama_FastRail
**Seção 1 — Identificação e visão geral**

- Nome do Grupo: FastRail
- Integrantes: Arthur N., Larissa, Matheus P. e Vinicius.
- Link do Mockup: https://www.figma.com/design/rQUNDWUKXz0W6GPQ4GEKNk/Mockup-SA-Ferrorama?node-id=0-1&t=ygM9QbtWePesGjj0-1

FastRail é um sistema de monitoramento ferroviário feito para funcionários e gestores. A plataforma permite acompanhar trens, estações e ocorrências em tempo real, facilitando a tomada de decisões e aumentando a segurança operacional. Seu diferencial está na interface mobile-first, intuitiva e responsiva, que centraliza informações críticas em um único ambiente de fácil acesso.

Em nosso projeto será implementado:
HTML: Para estruturar as páginas do sistema
CSS: Para estilizar as telas
JS: Utilizado para adicionar interatividade no sistema
Bootstrap: para facilitar a responsividade e acelerar o desenvolvimento da interface.

**Seção 2 — Identificação e visão geral**
ferrorama/
├── index.html                 # Boas-vindas (porta de entrada do app)
├── README.md
├── docs/
│   ├── plano-implementacao.md
│   ├── fluxos-navegacao.md
│   └── mockup.png
├── assets/
│   ├── img/
│   │   ├── logo-fastrail.svg
│   │   ├── mapa-linha.png
│   │   └── icones/
│   └── fonts/
├── css/
│   ├── base/
│   │   ├── reset.css
│   │   ├── variaveis.css      # paleta vermelha, tipografia (tokens)
│   │   └── tipografia.css
│   ├── componentes/
│   │   ├── botao.css
│   │   ├── card.css
│   │   ├── formulario.css
│   │   ├── cabecalho.css
│   │   └── nav-inferior.css
│   └── paginas/
│       ├── login.css
│       ├── dashboard.css
│       ├── sensores.css
│       └── ...               # só o que é específico de cada tela
├── js/
│   ├── core/
│   │   ├── auth.js           # sessão, login, logout, papel do usuário
│   │   ├── dados.js          # leitura/escrita de dados (mock → API depois)
│   │   ├── navegacao.js      # ir entre páginas, passar parâmetros
│   │   └── validacao.js      # regras de validação de formulário
│   ├── componentes/
│   │   ├── cabecalho.js      # injeta o header compartilhado
│   │   ├── nav-inferior.js   # injeta a barra de navegação
│   │   └── card-sensor.js    # monta card de sensor a partir de dados
│   └── paginas/
│       ├── login.js
│       ├── cadastro.js
│       ├── comprar-ingressos.js
│       ├── dashboard.js
│       ├── sensores.js
│       └── ...               # um JS por página, orquestra a tela
├── data/                     # dados mockados, trocáveis por API real
│   ├── usuarios.json
│   ├── trens.json
│   ├── sensores.json
│   ├── linhas.json
│   └── ingressos.json
└── paginas/
    ├── auth/
    │   ├── cadastro.html
    │   └── login.html
    ├── cliente/
    │   ├── home.html
    │   ├── comprar-ingressos.html
    │   ├── linha.html
    │   ├── pagamento.html
    │   ├── pix.html
    │   ├── cartao.html
    │   ├── meu-perfil.html
    │   ├── meu-bilhete.html
    │   └── ajuda.html
    └── funcionario/
        ├── dashboard.html
        ├── trens.html
        ├── sensores.html
        ├── sensor-adicionar.html
        ├── sensor-remover.html
        ├── relatorios.html
        └── funcionarios.html

Organização. Topo por tipo de arquivo; dentro de paginas/, por perfil (auth/cliente/funcionario) — porque cliente↔funcionário é a fronteira mais forte do sistema (quase dois apps com login comum), e isolar funcionario/ deixa a área restrita visível na própria árvore.
CSS em três camadas. base/ = tokens (a cor primária mora em variaveis.css; troca em 1 arquivo, não em 20). componentes/ = botão/card/nav que se repetem em toda tela, estilizados uma vez. paginas/ = só o que é exclusivo (grid do dashboard, mapa). Só por tela duplica tudo; só por componente não tem onde pôr layout específico. Fraqueza real: em JS puro nada obriga esse isolamento — é disciplina de equipe.
auth.js separado de dados.js. Razões de mudança diferentes: auth.js = sessão/papel/segurança; dados.js = buscar e gravar domínio. Separados, você troca a fonte (JSON → API) sem encostar no login. Regra de fundo: o que muda por motivos diferentes fica em arquivos diferentes.
O custo escondido: HTML puro não tem template, então as ~21 páginas repetem header e nav. Por isso js/componentes/cabecalho.js e nav-inferior.js os injetam em runtime — senão você corrige o menu em 21 lugares. É o maior gargalo de manutenção do projeto se ignorado; a alternativa (SPA) elimina a duplicação mas pede roteamento em JS, complexo demais para a SA.


**Seção 3: Componentes reutilizáveis identificados**

- Header (cabeçalho): utilizado para navegação e identificação do sistema.
- Botões de ação: presentes em formulários, filtros e confirmações.
- Cards informativos: exibem dados de trens, sensores e indicadores.
- Campos de formulário: usados em login, cadastro e pesquisas.
- Tabelas de listagem: organizam informações e registros do sistema.
- Ícones de ação: permitem visualizar, editar e pesquisar dados.
- Alertas e notificações: informam eventos e atualizações importantes.

**Seção 4: Critérios de Pronto**
1. Fundações (Interface e Acesso)
Componentes UI: Criar botões, formulários e cartões base (para garantir consistência visual).
Autenticação: Ecrãs de Login e Registo (para garantir acesso seguro antes de qualquer interação).
2. Núcleo Operacional (Administração)
Comboios (Trens) e Sensores: Implementar primeiro o registo da frota, rotas e sensores. Sem estes dados físicos inseridos no sistema, nenhuma outra funcionalidade terá informação para processar.
3. Monitorização e Gestão
Dashboard Geral: Painel de administração que só pode ser implementado depois de os comboios e sensores existirem para alimentar os gráficos e alertas.
4. Jornada do Cliente (Vendas)
Pesquisa de Bilhetes e Pagamento: O cliente só pode procurar viagens e pagar se as rotas (criadas na etapa 2) já existirem no servidor.
5. Pós-Venda e Tempo Real
Bilhete e Linha ao Vivo: O bilhete (QR Code) depende do pagamento aprovado. A "Linha ao Vivo" (tempo de chegada) depende dos sensores em tempo real.
6. Dados Históricos e Estáticos
Perfil, Relatórios e Contactos: Dependem do acumular de dados de viagens passadas ou são apenas páginas informativas sem impacto no funcionamento central do sistema.

**Seção 5: Critérios de Pronto**
Fluxo 1 — Cadastrar-se e acessar pela primeira vez
Perfil: novo usuário (Funcionário)
Boas-vindas → "Cadastrar" → Cadastro → aba "Funcionário" → preenche dados → "Cadastrar" → confirmação de sucesso → Login → preenche login e senha → "Login" → Dashboard Geral.
Fluxo 2 — Identificar alerta de sensor crítico e ver o trem afetado
Perfil: operador (Funcionário)
Dashboard Geral → nav inferior → Sensores → identifica card em estado de alerta (ex.: SEN-003, 52ºC) → toca no card → Gerenciamento de Trem do trem afetado → lê informações.
Fluxo 3 — Cadastrar um novo funcionário
Perfil: admin (Funcionário)
Dashboard → Funcionários → "Adicionar" → Cadastro → aba "Funcionário" → preenche dados → "Cadastrar" → confirmação → volta para Funcionários com o novo registro na lista.
Fluxo 4 — Gerar relatório de falhas de um período
Perfil: técnico (Funcionário)
Dashboard → nav → Relatórios → seleciona "tipo de relatório" → define intervalo de datas → seleciona "tipo de exibição" → "Gerar" → tabela de resultados → "Baixar em PDF".
Fluxo 5 — Comprar ingresso e obter o bilhete
Perfil: cliente
Home (FastRail) → "Comprar Ingressos" → seleciona partida e chegada → "Confirmar" → lista de resultados → seleciona viagem → Linha Joinville (mapa + pontos) → "Prosseguir" → Formas de Pagamento → "Pix" → tela Pix (QR + "Copiar") → confirmação de pagamento → Meu Bilhete (QR de embarque, código FRM-2026-XXXX).
Fluxo 6 — Sair do sistema
Perfil: qualquer
Tela atual → Meu Perfil (cliente) ou menu da área Funcionário → "Sair" → confirmação → Boas-vindas.

**Seção 6: Critérios de Pronto**
Código e Estrutura
[ ] HTML Semântico: Uso correto e consciente de tags estruturais (como <header>, <main>, <section>, <footer>, <article>).

[ ] CSS Limpo: Estilização feita inteiramente em arquivos externos ou módulos; proibido o uso de estilos inline (style="...").

[ ] Console Limpo: Ausência de erros (errors) ou alertas graves (warnings) no console de desenvolvedor do navegador.

Responsividade e Design
[ ] Compatibilidade Mobile: Interface adaptada e totalmente funcional em telas mobile (largura de 390px), sem elementos cortados ou quebras de layout.

[ ] Compatibilidade Desktop: Interface perfeitamente ajustada para telas desktop (largura de 1440px).

[ ] Fidelidade ao Mockup: Identidade visual (cores, tipografia, pesos de fonte e espaçamentos) totalmente consistente com o protótipo definido pelo grupo.

Usabilidade e Fluxo
[ ] Navegação Funcional: Todos os links, botões e elementos clicáveis direcionam para as telas corretas (mesmo que a funcionalidade final da tela de destino ainda esteja em desenvolvimento).

Processo de Trabalho (Git & Qualidade)
[ ] Code Review: Código revisado, testado e aprovado por pelo menos um outro integrante do grupo antes da mesclagem.

[ ] Boas Práticas de Commit: Alterações salvas no repositório com mensagens de commit claras, curtas e descritivas (ex: feat: adiciona responsividade à tela de login).