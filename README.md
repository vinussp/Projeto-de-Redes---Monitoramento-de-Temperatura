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

# Inslando o Node-red no container

   https://nodered.org/docs/getting-started/docker

   Utilizando o seguinte comando no powersheel executando como admnistrador:
    `docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red`
   



## Dispositivo FMJV
Segue o link da simulação do dispositivo utilizando a plataforma wokwi. Nela usamos o microcontrolador ESP32 para controlar o sensor de temperatiura e humidade DHT22. 
https://wokwi.com/projects/382148746978339841

A cnoexão de dados é feita via software Node-Red, no qual recebe os dados via broker mqtt (utilizando um broker test disponibilizado pelo mqtt). O node red roda em um container ubuntu criado com o software Docker, através dele é disponiblizado um endereço onde acessamos o node red para fazermos os nós necessários para a conexão. No nosso caso, os dados são coletados em uma planilha Google Sheet, disponibilizada atraves do SaaS Google Cloud, onde possibilita a transmissão dos dados e o preenchimento da planilha para que os dados sejam utilizados como quiser.
segue o link da planilha criada: 
https://docs.google.com/spreadsheets/d/1e3PiWuxI4qP67w1QK4ryX9rTR2_JE_VGB4VOJ72VHoA/edit?usp=sharing
