# Construindo um Esquema Conceitual para Banco De dados

Descrição do Desafio
Agora você irá criar um esquema conceitual do zero. A partir da narrativa fornecida você será capaz de criar todas as entidades, relacionamentos e atributos. Caso encontre algo que não foi definido na narrativa, utilize a sua compreensão do contexto e deixe uma descrição no README do seu github. para verificação.

O esquema deverá ser adicionado a um repositório do Github para futura avaliação do desafio de projeto. Adicione ao Readme a descrição do projeto conceitual para fornecer o contexto sobre seu esquema.

# Objetivo:
Criar o esquema conceitual para o contexto de oficina com base na narrativa fornecida

# Narrativa:

Sistema de controle e gerenciamento de execução de ordens de serviço em uma oficina mecânica

Clientes levam veículos à oficina mecânica para serem consertados ou para passarem por revisões  periódicas

- Cada veículo é designado a uma equipe de mecânicos que identifica os serviços a serem executados e preenche uma OS com data de entrega.

- A partir da OS, calcula-se o valor de cada serviço, consultando-se uma tabela de referência de mão-de-obra

- O valor de cada peça também irá compor a OSO cliente autoriza a execução dos serviços

- A mesma equipe avalia e executa os serviços

- Os mecânicos possuem código, nome, endereço e especialidade

- Cada OS possui: n°, data de emissão, um valor, status e uma data para conclusão dos trabalhos.

  # Esquema Conceitual para um Banco de Dados de uma Oficina

  ![img](https://github.com/ThiagoKioshima/Esquema_Conceitual_BD_Oficina/blob/main/Oficina.png)


  # Modelagem e Estrutura do Banco de Dados da Oficina Mecânica
O projeto de Banco de Dados para o sistema de controle e gerenciamento de Ordens de Serviço (OS) da oficina mecânica foi concebido seguindo os princípios de modelagem lógica, garantindo a integridade e a rastreabilidade de todas as operações.

1. Estrutura Central (Entidades e Relações 1:N)
O modelo é ancorado em entidades primárias que mapeiam os atores e objetos da oficina:

Clientes e Veículos: O relacionamento é 1:N, onde um Cliente pode possuir múltiplos Veículos, mas cada veículo está ligado exclusivamente a um cliente. A chave estrangeira (Cliente_id_Cliente) na tabela Veículo assegura essa ligação.

Equipes e Mecânicos: O modelo define equipes de trabalho. Uma Equipe pode ser composta por vários Mecânicos (1:N), permitindo a identificação da especialização e alocação de cada profissional.

Ordem de Serviço (OS): A tabela Ordem de Serviço é a espinha dorsal do sistema, registrando detalhes como DataEmissao, DataEntrega, Status e o ValorTotal. Ela é diretamente vinculada ao Veículo e à Equipe responsável por meio de chaves estrangeiras.

2. Resolução de Complexidade (Relacionamentos N:M)
Os relacionamentos Muitos para Muitos (N:M) — essenciais para calcular o custo total de uma OS — foram resolvidos através da criação de tabelas de junção, garantindo a contabilização precisa dos itens utilizados:

OS_Servico_tempo_servico (Serviços e Mão de Obra): Esta tabela resolve a relação entre Ordem de Serviço e Serviço. Sua característica fundamental é a inclusão do campo Tempo_Servico, que, ao ser multiplicado pelo CustoMao_de_obra da tabela Serviço, permite calcular o custo exato da mão de obra na OS.

OS_Servico_Peça (Peças Utilizadas): Esta tabela relaciona a Ordem de Serviço com a Peça. Inclui o campo Quantidade_utilizada, que, ao ser multiplicado pelo ValorUnitário da peça, permite o cálculo exato do custo de material na OS.

3. Garantia de Cálculo e Rastreabilidade
Os refinamentos aplicados garantem que o BD está apto a fornecer o cálculo completo da OS:

Valor Total Derivado: O campo ValorTotal na tabela Ordem de Serviço será um atributo derivado, calculado pela soma dos custos registrados nas tabelas de junção (OS_Servico_tempo_servico e OS_Servico_Peça).

Nomenclatura Funcional: As tabelas de junção foram renomeadas (ex: de _has_ para OS_Servico_tempo_servico) para aumentar a clareza e aderir a práticas modernas de modelagem.
