![fmjv](https://github.com/vinussp/Projeto-de-Redes---Monitoramento-de-Temperatura/assets/78106775/5f245d1f-9381-48c0-a267-fd3aa94b9ddc)

# Projeto de Redes (FMJV): Monitoramento de Temperatura
Este projeto IoT envolve o uso de um módulo de rede para facilitar a comunicação
entre os sensores e permitir a transmissão dos dados coletados. Esses dados serão disponibilizados para o usuário final por meio de um aplicativo móvel, onde poderão ser
visualizados e analisados em tempo real.

 ## Proposta comercial
 [Proposta_comercial.pdf](https://github.com/vinussp/Projeto-de-Redes---Monitoramento-de-Temperatura/files/12811266/Proposta_comercial.pdf)
 ## Plano de Ataque

 ## Cronograma
 ![cronograma](https://github.com/vinussp/Projeto-de-Redes---Monitoramento-de-Temperatura/assets/78106775/295285c7-75b9-4003-9e37-b23ea643fff5)
 ### 04/10/2023
- 
-
## Dispositivo FMJV
Segue o link da simulação do dispositivo utilizando a plataforma wokwi. Nela usamos o microcontrolador ESP32 para controlar o sensor de temperatiura e humidade DHT22. 
https://wokwi.com/projects/382148746978339841

A cnoexão de dados é feita via software Node-Red, no qual recebe os dados via broker mqtt (utilizando um broker test disponibilizado pelo mqtt). O node red roda em um container ubuntu criado com o software Docker, através dele é disponiblizado um endereço onde acessamos o node red para fazermos os nós necessários para a conexão. No nosso caso, os dados são coletados em uma planilha Google Sheet, disponibilizada atraves do SaaS Google Cloud, onde possibilita a transmissão dos dados e o preenchimento da planilha para que os dados sejam utilizados como quiser.
segue o link da planilha criada: 
https://docs.google.com/spreadsheets/d/1e3PiWuxI4qP67w1QK4ryX9rTR2_JE_VGB4VOJ72VHoA/edit?usp=sharing
