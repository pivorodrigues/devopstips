# <img src="images/amazon-web-services-logo.png" width="30px"> AWS Solutions Training for Partners: Foundations <img src="images/amazon-web-services-logo.png" width="30px">

## Módulo 1: Clientes estão mudando para a AWS

**Cinco benefícios fundamentais da computação em nuvem:**

  - Agilidade;

  - Elasticidade;

  - Redução de custos;

  - Alcance Global;

  - Variedade de serviços.


## Módulo 2: AWS Solution Architects

**Princípios de liderança da Amazon:**

  - Obsessão pelo cliente;

  - Aprender a ser curioso;

  - Conquistar confiança;

  - Envolver-se profundamente;

  - Inventar e simplificar;

  - Pensar grande;

  - Estar pronto para agir;

  - Entregar resultados.

#

**Os SA's da Amazon tornam os clientes bem-sucedidos quando:**

  - Definem o escopo;

  - Envolvem-se profundamente;

  - Projetam as soluções do "Well-architected";

  - Conquistam confiança;

  - Ensinam;

  - Inventam, simplificam e inovam.

#

**Para gerar sucesso em longo prazo, os SA's da Amazon devem saber:**

  - Que a migração para a nuvem é um processo;

  - Que os clientes precisam de experiência e ajuda do SA;

  - Conhecer seus clientes;

  - Conhecer a plataforma e os serviços da AWS;

  - Agir no melhor interesse em longo prazo do cliente;

  - Usar a estratégia de longo prazo.


## Módulo 3: Você sabe mais do que imagina

<p align="center"><img src="images/aws-common-services.png" width="700px"></p>

#

**AWS Lambda**

  - Seviço de computação stateless;

  - Executa o código em resposta a um evento;

  - Acionamento em milissegundos;

  - Baixo custo - faturado em incrementos de 100 ms + memória;

  - Foco no aplicativo, não na infraestrutura.

**Amazon Machine Learning (Amazon ML)**

  - Machine Learning (ML) como um serviço;

  - Criação de modelos de ML usando APIs simples;

  - Permite que desenvolvedores de todos os níveis de habilidade criem aplicativos de ML.

**Modelos de AWS Blockchain**

  - Comece rapidamente com o blockchain;

  - Experimente estruturas de blockchain - Ethereum, Hyperledger Fabric e outras;

  - Controle o acesso a recursos da AWS com políticas de permissão granulares;

  - Casos de uso:

      - Cadeia de fornecimento;

      - Transações financeiras;

      - Identidade e compatibilidade.

#

**O todo é maior que a soma das partes**

<p align="center"><img src="images/aws-external-services.png" width="700px"></p>


## Módulo 4: Conceitos de Arquitetura AWS

**Regiões e Zonas de disponibilidade da AWS**

<p align="center"><img src="images/aws-regions.png" width="700px"></p>

#

**Mapa de regiões da AWS**

<p align="center"><img src="images/aws-region-map.png" width="700px"></p>

#

**Conceitos:**

  - **Região:** Área geográfica específica no globo;

  - **Zona de disponibilidade:** Múltiplas locações isoladas (datacenters);

  - **Edge Locations:** Pontos de presença da AWS, AWS Cloudfront (CDN).

#

**Pontos de presença da AWS**

<p align="center"><img src="images/aws-points-presence.png" width="700px"></p>

#

**Robustez regional da AWS**

  - Dois centros de trânsito redundantes;

  - Instalações altamente espelhadas e conectadas;

  - 16 (agora 18) regiões;

  - As regiões estão localizadas em áreas geográficas separadas;

  - As regiões são isoladas umas das outras;

  - Cada região tem várias zonas de disponibilidade;

  - Os dados nunca são movidos de uma região para outra pela AWS;

  - As zonas de disponibilidade estão em locais isolados (energia, rede, zona de inundação, etc.) dentro das regiões;

  - As zonas de disponibilidade têm um ou mais datacenters (algumas têm até 8);

  - As zonas de disponibilidade são projetadas para oferecer alta disponibilidade dos serviços aos clientes;

  - As zonas de disponibilidade em uma região têm uma latência inferior a 1ms entre elas;

  - Cada criação de datacenter da AWS possui entre 50.000 e 80.000 servidores físicos;

#

**O gerenciamento contínuo**

<p align="center"><img src="images/aws-continuous-management.png" width="700px"></p>

#

**Serviços gerenciados: Global, regional e zonal**

<p align="center"><img src="images/aws-managed-services.png" width="700px"></p>

#

**Modelo de segurança compartilhada**

<p align="center"><img src="images/aws-shared-security.png" width="700px"></p>

#

**Infrastructure as Code**

 - O AWS é baseado em APIs;

 - Os SDKs são usados para criar e operar.


## Módulo 5: Elementos fundamentais

**Serviços fundamentais da AWS: Computação**

<p align="center"><img src="images/aws-fundamental-services.png" width="700px"></p>

#

**Amazon Elastic Compute Cloud (Amazon EC2)** [[link](https://aws.amazon.com/pt/ec2/)]

  - Instância de máquina virtual em execução em um hipervisor da AWS;

  - Suporte para várias distribuições do Linux ou Microsoft Windows;

  - O cliente controla o sistema operacional do host com contas root e de administrador;

  - O cliente é responsável por todos os aplicativos instalados.

**Famílias do EC2** [[link](https://aws.amazon.com/pt/ec2/instance-types/)]

  - [Uso geral](https://aws.amazon.com/pt/ec2/instance-types/#General_Purpose)

  - [Computação otimizada](https://aws.amazon.com/pt/ec2/instance-types/#Compute_Optimized)

  - [Memória otimizada](https://aws.amazon.com/pt/ec2/instance-types/#Memory_Optimized)

  - [Armazenamento denso](https://aws.amazon.com/pt/ec2/instance-types/#Storage_Optimized)

  - E/S otimizada

  - [GPU](https://aws.amazon.com/pt/ec2/instance-types/#Accelerated_Computing)

  - Micro

#

**Nomes de instâncias do Amazon EC2**

<p align="center"><img src="images/aws-instance-name.png" width="500px"></p>

#

**Opções de definição de preço do Amazon EC2** [[link](https://aws.amazon.com/pt/ec2/pricing/)]

<p align="center"><img src="images/aws-price-options.png" width="700px"></p>

#

**Auto Scaling do Amazon EC2** [[link](https://aws.amazon.com/pt/autoscaling/)]

  - Escale as instâncias do Amazon EC2 de forma contínua e automática;

  - Inicie ou encerre instâncias para atender à capacidade desejada;

  - Mantenha a capacidade balanceada pelas AZs;

  - Substitua instâncias não íntegras ou inacessíveis;

  - Baseado em políticas;

  - Integrado com outros serviços da AWS;

  - Casos de uso:

    - Escalabilidade dinâmica - otimize recursos do EC2 rapidamente;

    - Reduza custos e gerencie a definição de preço;

    - Gerenciamento de frotas - balanceamento, recuperação de falhas.

**Amazon Container Services (ECS)** [[link](https://aws.amazon.com/pt/ecs/)]

  - Amazon Elastic Container Service (ECS) e Amazon Elastic Container service for Kubernetes (EKS);

  - A AWS executa o gerenciamento do cluster do Amazon EC2 para os clientes;

  - Elimina a complexidade da infraestrutura de contêineres em operação;

  - Casos de uso:

      - Implante os microsserviços para acelerar a inovação;

      - Execute processos em lote;

      - Migre os aplicativos legados sem precisar de alterações de código;

      - Acelere o Machine Learning.

**AWS Fargate** [[link](https://aws.amazon.com/pt/fargate/)]

  - Permite que os clientes executem contêineres sem gerenciar um cluster;

  - Expande o Amazon ECS e o EKS;

  - Executa dezenas de milhares de contêineres em segundos;

  - Integra-se ao Auto Scaling para uso ideal.

<p align="center"><img src="images/aws-fargate.png" width="500px"></p>

**AWS Lambda** [[link](https://aws.amazon.com/pt/lambda/)]

  - Serviço de computação stateless, executa o código em resposta a um evento;

  - Acionamento em milissegundos;

  - Faturado em incrementos de 100 ms + memória;

  - Pague somentte pelo o que usar;

  - Os servidores virtuais não são necessários;

  - Casos de uso:

    - Criar aplicativos modulares, escaláveis e leves;

    - Processamento de dados sem servidor sob demanda;

    - Use o AWS Step Functions para orquestrar arquiteturas do Lambda;

    - Execute a validação dos dados, filtragem, classificação e outras transformações;

    - Miniaturas de imagem, atividade no aplicativo, cliques no website e saída do dispositivo.

#

**Serviços fundamentais da AWS: Armazenamento**    

<p align="center"><img src="images/aws-fundamental-services.png" width="700px"></p>

#

**Amazon Elastic Block Storage (EBS)** [[link](https://aws.amazon.com/pt/ebs/)]

  - Volumes de armazenamento de bloco para uso com instâncias do Amazon EC2;

  - Armazenamento persistente anexado a instâncias do EC2 como disco nativo;

  - Formatado usando um sistema de arquivos padrão do SO (como ext4 ou NTFS);

  - Armazenamento escalável e de alta performance para aplicativos;

  - Casos de uso:

    - Volumes de inicialização/raiz para instância do Amazon EC2;

    - Volumes de dados para aplicativos corporativos, como SAP, Microsoft Exchange e Microsoft Sharepoint;

    - Bancos de dados relacionais ou NoSQL que oferecem suporte a milhões de usuários.

#

**Amazon Simple Storage Service (Amazon S3)** [[link](https://aws.amazon.com/pt/s3/?nc=sn&loc=0)]

  - Armazenamento de objetos altamente escalável, confiável, rápido e durável;

  - Armazene e recupere qualquer quantidade de dados em qualquer lugar online, usando HTTP e HTTPS;

  - Um serviço laborioso que serve para muitos propósitos;

  - Integrado com serviços de segurança da AWS, fornece acesso granular e criptografia transparente;

  - Casos de uso:

    - Hospedagem de arquivos de aplicativos;

    - Backup para recuperação de desastres;

    - Hospedagem na web estática;

    - Dados de streaming;

    - Data lakes.

**Classes de armazenamento do Amazon S3** [[link](https://aws.amazon.com/pt/s3/storage-classes/?nc=sn&loc=3)]    

<p align="center"><img src="images/aws-s3-classes.png" width="700px"></p>

**Amazon Data Lakes** [[link](https://aws.amazon.com/pt/big-data/datalakes-and-analytics/)]

<p align="center"><img src="images/aws-data-lakes.png" width="700px"></p>

#

**Serviços fundamentais da AWS: Rede** [[link](https://aws.amazon.com/pt/products/networking/)]

<p align="center"><img src="images/aws-fundamental-services.png" width="700px"></p>

#

**Amazon Virtual Private Cloud (Amazon VPC)** [[link](https://aws.amazon.com/pt/vpc/)]

  - Sub-redes virtuais isoladas na Nuvem AWS;

  - Seguro, com alta performance, altamente configurável;

  - Suporte de segurança sofisticado;

  - Casos de uso:

    - Hospedar recursos públicos e privados;

    - Organizar/isolar componentes do aplicativo;

    - Isolar recursos por entidade lógica, grupo, sensibilidade ou função;

    - Estender redes locais para a nuvem.

**Amazon VPC definida**

  - Seção logicamente isolada da Nuvem AWS;

  - Por padrão, não há acesso à internet e as instâncias não são endereçáveis pela internet;

  - Controle completo sobre o ambiente de rede virtual;

  - Conceitos de redes comprovados e bem compreendidos:

    - Intervalo de endereços IP definidos pelo usuário;

    - Sub-redes;

    - Tabelas de rotas;

    - Listas de acesso de controle;

    - Gateways de rede;

  - Uma forma de obter agilidade e segurança adicional.  

  <p align="center"><img src="images/aws-defined-vpc.png" width="250px"></p>

**Amazon VPCs como estratégia**

  - Como qualquer aplicativo de produção, as soluções dos serviços da AWS devem ser implantadas em um cenário de vários ambientes.

    - Cada "ambiente" deve estar em sua própria Amazon VPC;

    - No mínimo, considere os ambientes de produção e desenvolvimento de VPC;

    - Se fizer sentido, adicione ambientes para teste, desenvolvimento futuro ("dev + 1"), preparação e outros propósitos;

    - Lembre-se de que os ambientes da AWS com uso intermitente (como teste) podem ser interrompidos quando não estão em uso, ajudando a limitar os custos.

    <p align="center"><img src="images/aws-strategy-vpcs.png" width="400px"></p>
