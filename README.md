![fmjv](https://github.com/vinussp/Projeto-de-Redes---Monitoramento-de-Temperatura/assets/78106775/5f245d1f-9381-48c0-a267-fd3aa94b9ddc)

# Projeto de Redes (FMJV): Monitoramento de Temperatura
Este projeto IoT envolve o uso de um módulo de rede para facilitar a comunicação
entre os sensores e permitir a transmissão dos dados coletados. Esses dados serão disponibilizados em uma planilha online no Google Sheets através do serviço da nuvem do Google Cloud, onde poderão ser
visualizados e analisados em tempo real.

 ## Proposta comercial
 [Proposta_comercial.pdf](https://github.com/vinussp/Projeto-de-Redes---Monitoramento-de-Temperatura/files/12811266/Proposta_comercial.pdf)
 ## Plano de Ataque

 ## Cronograma
 ![cronograma](https://github.com/vinussp/Projeto-de-Redes---Monitoramento-de-Temperatura/assets/78106775/295285c7-75b9-4003-9e37-b23ea643fff5)


<h1 align="center"> Monitoramento de temperatua </h1>


# 📒 Resumo do projeto
Projeto consiste na criação de um dispositivo que monitora a temperatura e humidade e transmite os dados via mqtt e os diponibiliza para uma plataforma IOT.

## ✔️ Técnicas e tecnologias utilizadas

- ``Docker e conteiners``
- ``MQTT``
-  ``IOT``

## 📁 Passo a passo
# Habilitar o WSL na maquina
   https://learn.microsoft.com/pt-br/windows/wsl/install-manual
   
   O WSL é um subsistema do Windows para Linux que permite que os desenvolvedores executem um ambiente GNU/Linux, incluindo a maioria das ferramentas de linha de comando, utilitários e aplicativos, diretamente      no Windows, sem modificações e sem a sobrecarga de uma máquina virtual tradicional ou instalação dualboot.
   
   Ele é um passo importante na criação de uma maquina virtual linux na qual o broker vai ser instalado para receber os dados enviados pelo dispositivos e restransmiti-los para a plataforma IOT.

# Instalação do Docker
  https://www.docker.com/
  
  O Docker é um conjunto de produtos de plataforma como serviço que usam virtualização de nível de sistema operacional para entregar software em pacotes chamados contêineres. Os contêineres são isolados uns dos    outros e agrupam seus próprios softwares, bibliotecas e arquivos de configuração
  .
  A utilização do docker serve para organizar e gerenciar os containers criados.
  
# Configurando o Docker
   - Depois de instalado, abra o Docker para desktop, realize o cadastro para utilização;
   - Vá em configurações, resorces e habilite para a integração com o WSL;

## Node-red
   https://nodered.org/
   
   O Node-RED é uma ferramenta de desenvolvimento de baixo código baseada em fluxo para programação visual desenvolvida originalmente pela IBM para conectar dispositivos de hardware, APIs e serviços online como     parte da Internet das Coisas.

   No projeto, o Node-red faz a comunicação entre o boker mqtt e a a plataforma IOT. Ele também foi utilizado para a exibição dos dados em um Dashboard.

# Instalando o Node-red no container

   https://nodered.org/docs/getting-started/docker

   Utilizando o seguinte comando no powersheel executando como admnistrador:
   
   `docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red`

   Automaticamente o Docker criara um container linux contendo node-red, onde poderemos fazer os nós de conexão dos dados mqtt e a plataforma IOT.

   No prompt de comando aparacerá o endereço para o acesso da pagina dos nós.

   `24 Nov 22:40:15 - [info] Server now running at http://127.0.0.1:1880/`

   Nessa linha aparece a data na qual foi iniciado o programa, e no final o endereço de acesso pelo navegador.
   
## Simulação do Dispositivo FJMV
   Segue o link da simulação do dispositivo utilizando a plataforma WOKWI. Nela usamos o microcontrolador ESP32 para controlar o sensor de temperatiura e humidade DHT22. 

   https://wokwi.com/projects/382148746978339841

   Utilizamos o sensor DHT22 para a captação da temperatura e da humidade por ser um sensor de facil acesso e baixo custo. O integramos com a ESP32 por fazer nativamente a conexão por wifi paara a transmissão de    dados. Esses dados são transfmitidos para um broquer mqtt e depois enviados para a maquina virtual (container) e captados pelo node-red para a transmissão para a plataforma IOT.

   O código para criado na linguagem C, pode ser acessado nos arquivos desse GitHub. Nele configuramos a conexão com o servidor broker mqtt:

   https://test.mosquitto.org

   Ele hospeda um servidor/corretor Eclipse Mosquitto MQTT disponível publicamente para testes. MQTT é um protocolo muito leve que usa um modelo de publicação/assinatura. Isso o torna adequado para mensagens        "máquina para máquina", como sensores de baixa potência ou dispositivos móveis.

   No codigo também utilizamos a porta 1883 para a transmissão de dados. e configuramos a forma de pulicação das variaveis, com `/FJMV/temp` para a temperatura e `/FJMV/hum` para humidade.

## Configurando o Node-Red

   Inicialmente é preciso preparar o fluxo para a transmissão dos dados. Em gerenciar paletas e instalar nós, é necessário intalar os nós Dashboard "node-red-dashboard" e Google Sheets "node-red-contrib-google-sheets".

   o Nó Dashboar serve para criar um relógio mostrador, para exibir as informações recebidas pelo broker. E o nó Google sheet serve para a transmissão dos dados para a planilha.

   Criamos dos nós mqtt in, um para a temperatura e outro para a humidade. Na sua configuração, colocamos o servidor "test.mosquitto.org" e a porta 1883, ajustamos o QoS para 0 e o tópico, `/FJMV/temp` para a temperatura e `/FJMV/hum` para humidade.

   O proximo nó são os mostradores, um para temperatura e outro para humidade. Na sua configuração, editamos o Group, preenchendo o nome "FJMV" e editamos a tab com o nome "Home" e o icon "dashboard". Essa parte é comum para os dois.
   Ainda na parte da ediçao, escolhemos o type: Gauge para temperatura e Donut para a humidade, editamos o label: Temperatura e humidade, o unit: ºC e %, o range: 0 a 45, temperatura e 0 a 100 humidade, ajustamos as cores e o nome no final, temp para temperatura e hum pata humidade.

   Dessa forma, ja podemos visualizar os dados enviados pelo sensor em um dashboard.

   # Transmissão dos dados para o Google Sheet

 

No nosso caso, os dados são coletados em uma planilha Google Sheet, disponibilizada atraves do SaaS Google Cloud, onde possibilita a transmissão dos dados e o preenchimento da planilha para que os dados sejam utilizados como quiser.
segue o link da planilha criada: 
https://docs.google.com/spreadsheets/d/1e3PiWuxI4qP67w1QK4ryX9rTR2_JE_VGB4VOJ72VHoA/edit?usp=sharing
