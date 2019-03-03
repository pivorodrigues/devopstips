# [Estácio] Implementação de Banco de Dados

**Aula 1 - Modelo Relacional**

- **Sistemas tradicionais:** Nos Sistemas Tradicionais os dados são armazenados em arquivos que estão fisicamente armazenados, separados uns dos outros. O acesso é feito pelos programas de aplicação, utilizando o nome externo dos arquivos e definindo todo o registro, independente da utilização dos campos.

- **Sistemas de Banco de Dados:** Nos Sistemas de Banco de Dados os dados são definidos para o Sistema Gerenciador de Banco de Dados (SGBD), através da DDL (linguagem de definição de dados). Fisicamente estão armazenados em um único local, e o acesso só se realiza através do SGBD.  Nos programas de aplicação, é necessário apenas definir os campos a serem utilizados pelo programa.

<p align="center"><img src="images/sgbd.png" width="500px"></p>

- **Programas Aplicativos e Consultas:** Os programas são escritos em uma linguagem front-end (Java, Python, etc), possibilitando o acesso do usuário a informações contidas no banco. Já as consultas representam as informações solicitadas pelo usuário ao banco de dados.

- **Software para processar consultas/manipulação:** Módulo do SGBD responsável por determinar a forma de executar a consulta solicitada pelo usuário, via aplicação. Realiza a interpretação do comando (análise sintática, léxica e semântica) e elabora o plano de execução do comando, estabelecendo a forma de acessar fisicamente os dados.

- **Software para acessar dados armazenados:** Módulo do SGBD responsável pelo controle do acesso físico aos dados.

- **Dados:** Conjunto de valores armazenados pelo banco de dados em seus arquivos.

- **Catálogo:** Armazena meta-dados, ou seja, informações referentes ao tipo e organização dos dados do banco.
