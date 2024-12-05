Eplicação das principais files e folder do nosso projeto. 
Temos como uma das principais files o SRC que contem detro dele "CONFIG", "CONTEXT", SCREENS. Temos um file que contem arquivos .img. Temos nosso file pai chamado APP.JSX. Entre outros, como simulador de banco de dados.

SRC:
Em config temos um file chamado, firebaseConfig.js: 
Importações necessárias do Firebase, Variáveis de ambiente para manter informações sensíveis protegidas, Configurações do Firebase extraídas das variáveis de ambiente,
Inicializa o Firebase apenas se não houver uma instância já inicializada, Exporta o serviço de autenticação e o banco de dados Firestore.

Em context temos dois files, AuthContext.js:
Importações necessárias, Criação do contexto de autenticação, Componente que fornece dados e funções relacionadas à autenticação, Estado que guarda o usuário autenticado (ou null se não autenticado),
Estado para indicar se a autenticação ainda está carregando, Hook useEffect para monitorar o estado de autenticação. O Firebase tem um método `onAuthStateChanged` que detecta alterações no login/logout.
Atualiza o estado com o usuário atual (ou null se deslogado), Termina o carregamento inicial, Cleanup: Remove o observador ao desmontar o componente, Função para logout do usuário.
Chama o método `signOut` do Firebase. Firebase desconecta o usuário, Limpa o estado local, Mostra erros no console. O componente `Provider` envolve toda a aplicação e fornece os seguintes dados:
`user`: Usuário autenticado (ou null). `loading`: Indica se os dados de autenticação ainda estão carregando. `logout`: Função para desconectar o usuário.

E CartoesEstudoContext.js:
Importações necessárias, Criação do contexto para cartões de estudo, Provedor que gerencia os cartões de estudo. Estado para armazenar a lista de cartões, Hook useEffect para carregar os cartões sempre que o usuário logado mudar.
Função para carregar os cartões do Firestore. Busca apenas os cartões associados ao UID do usuário atual. Obtém os documentos do Firestore, Atualiza o estado local com os cartões,
Função para adicionar um novo cartão ao Firestore. Adiciona o UID do usuário. Salva no Firestore. Atualiza a lista local. Função para atualizar um cartão existente. Atualiza o documento no Firestore
Função para excluir um cartão do Firestore. Remove do Firestore, Remove localmente. O componente `Provider` fornece as seguintes funcionalidades: `cartoes`: Lista de cartões carregados.
`adicionarCartao`: Função para criar novos cartões. `atualizarCartao`: Função para editar cartões existentes. `excluirCartao`: Função para deletar cartões.  Exporta o contexto para ser usado nos componentes.

FOLDER screens
EdicaoCartaoScreen.js: 
Importações necessárias do React, React Native e bibliotecas auxiliares, Biblioteca para dropdowns,  Contexto de cartões, Biblioteca para seleção de datas, Biblioteca de ícones.
Tela para criar ou editar cartões de estudo.É usada tanto para criar novos cartões quanto para editar existentes, dependendo da rota. Obtém o ID do cartão da rota, caso seja edição.
Pega os métodos e dados do contexto. Encontra o cartão no estado global (caso seja edição). Estados para os campos do formulário. Status inicial padrão: "backlog". Controle para exibir o modal de seleção de data.
Atualiza os estados com os valores do cartão ao entrar na tela de edição. Salva os dados do cartão no Firestore. Chama `adicionarCartao` ou `atualizarCartao` dependendo se o cartão é novo ou existente.
Salva a data em formato ISO, Retorna para a tela anterior, Funções auxiliares para manipular o DateTimePicker. Campo de Título, Campo de Notas, Campo de Data de Término, Campo de Status, Botão Salvar,
Estilização da tela.

ListaCartaoScreen.js:
Importações necessárias do React, React Native e Context API, Tela principal para exibição dos cartões de estudo. Lista cartões organizados por status: backlog, em progresso, concluídos.
Permite adicionar, editar e excluir cartões. Obtém os dados e métodos do contexto de cartões. Confirmação antes de excluir um cartão. Renderiza um cartão individual. Aplica cores diferentes com base no status do cartão.
Define estilos baseados no status do cartão, Botão para editar o cartão, Botão para excluir o cartão,  Filtra os cartões de estudo por status. Filtra cartões que estão próximos ao vencimento (dentro de 15 dias).
Botão para acessar tarefas a vencer, Lista de cartões em progresso, Lista de cartões concluídos, Lista de cartões em backlog, Botão para adicionar um novo cartão. Estilização da tela, Cinza claro para backlog,
Verde para concluído, Azul para em progresso.

LoginScreen.js:
Importações necessárias do React, React Native e Firebase, Tela de Login, Permite que o usuário insira email e senha para autenticar. Redireciona o usuário para a tela principal após login bem-sucedido.
Estados para capturar email e senha, Realiza o login usando o Firebase Authentication. Tenta realizar login com o Firebase. Exibe mensagens de erro. Logo do aplicativo, Campo de email, Campo de senha,
Botão de login, Link para a tela de registro. Estilização da tela.

RegistroScreen.js:
Importações necessárias do React, React Native e Firebase, Firebase para criar contas de usuário, Configuração do Firebase. Tela de Registro, Permite que novos usuários criem uma conta com email e senha.
Redireciona para a tela de login após o registro bem-sucedido. Estados para capturar email e senha. Função para registrar um novo usuário. Usa o método `createUserWithEmailAndPassword` do Firebase Authentication.
Cria o usuário no Firebase, Retorna para a tela de login após o registro, Exibe mensagens de erro. Título da tela, Campo de email, Campo de senha, Botão de registro. Estilização da tela.

TarefasVencimentoProximoScreen.js: 
Importações necessárias do React e React Native, Contexto dos cartões, Tela para exibir as tarefas próximas do vencimento (dentro de 15 dias). Filtra e exibe apenas os cartões cuja data de término está próxima.
Obtém os dados do contexto de cartões, Data atual. Filtra os cartões cuja data de término está dentro dos próximos 15 dias. Calcula a diferença em dias, Inclui cartões que vencem nos próximos 15 dias
Renderiza os cartões da lista. Exibe título, status e data de término formatada. Cabeçalho da tela, Lista de cartões filtrados. Estilização da tela.

App.js "PAI":
Importações necessárias do React, React Navigation e Context API, Contexto de autenticação, Contexto de cartões, Tela principal, Tela de edição/criação, Tela de vencimento, Tela de login,
Tela de registro, Ícones, Botão de logout. Criação da pilha de navegação, Configura e gerencia as rotas do aplicativo. Obtém o contexto de autenticação. Exibe uma tela em branco enquanto os dados de autenticação estão carregando.
Rotas protegidas (requerem autenticação), Rotas públicas (não requerem autenticação). Componente principal do aplicativo. Envolve a aplicação com os provedores de contexto.





