# Camada de Enlace de Dados
Trata dos protocolos envolvidos no transporte de dados.

## Ethernet
Desenvolvida pelos anos 60 por Robert Metcalfe num projeto de fim de doutorado.

Já em 1982, alguns engenheiros se juntaram e redigiram as especificações oficiais para a Ethernet, que mais tarde foi publicada na IEEE.

#### Carrier Sense Multiple Access with Collision Detection (CSMA/CD)
Tecnologia legada responsável pela Ethernet por volta dos anos 1972.

Sua arquitetura consistia em um único cabo coax central com várias ramificações aos computadores. Toda a informação era transmitida com transmissão de +5 Volts. Por usar um único cabo, os computadores deveriam checar se ninguém está mandando informações pela ethernet e caso não estejam, poderiam mandar dados. Caso dois computadores acabassem mandando dados ao mesmo tempo, as duas voltagens iriam se somar, criando +10 Volts, o que causaria um *Voltage Spike* e em seguida uma **Colisão**. A partir da colisão, os computadores parariam de ouvir a rede por tempo aleatório e depois voltariam a ouvir, todos ao mesmo tempo, checando se ainda há colisão de dados.

Assim esse sistema criaria uma *Collision Domain*, em que se espera colisões a partir do funcionamento normal do sistema. Isso também geraria a necessidade de se criar um conjunto de dispositivos capazes de parar de ouvir e voltar a ouvir a ethernet todos ao mesmo tempo.

Não é assim que a Ethernet moderna funciona, mas é o modelo base.

### A revolução do Duplex

- **Half Duplex**: modelo semelhante ao walkie-talkie. Você pode transmitir informações da máquina A para B ou B para A, mas nunca as duas simultaneamente.

- **Full Duplex**: modelo semelhante ao atual telefone. Você pode transmitir e receber informações simultanemanete, além de permitir conexões mais velozes.

No CSMA/CD, tudo era a base de *half duplex* (meio duplex), mas com *full duplex*, não com o que se preocupar com colisões.


### Ethernet Frame / Protocol Data Unit (PDU)
Lembre-se do Encapsulamento de dados! O frame é o mensagem passada através da camada 2.

Ele possui a seguinte estrutura:

```
Ethernet Header + Packet + FCS
```

- Ethernet Header(): composto por:
    - Endereço MAC de onde veio (48 bits).
    - Endereço MAC de destino (48 bits).
    - Tipo (16 bits): indica o tipo de informação passada. Caso for uma pacote da camada 3, indica o protocolo da camada 3, como IPv4, IPv6, ARP.
    - Footer: rodapé
- Packet (1500 bytes): um pacote  (encapsulamento da camada 3) ou alguma mensagem de algum protocolo da camada 2. 1500 bytes é o tamanho máximo de dados carregáveis para um frame de ethernet e acaba sendo chamado de ***Maximum Transmission Unit (MTU)***, mas o MTU às vezes pode ser ultrapassado em ocasiões muito especiais, como em *datacenters* com as de redes de armazenaemnto, ou SANs. O hardware nesses casos é preparado para receber esses frames que também recebem um nome especial, os *Jumbo Frames*.
- FCS (32 bits): Frame Check Sequence - gerado a partir do algorítmo Cyclical Redundancy Check (CRC), que digere o CRC e o torna um número de 32 bits com a intenção de identificar erros em sua estrutura. O FSC é codificado na máquina enviadora e ao ser recebido, é comparado a outro FSC codificado pela máquina receptora. Se não forem idênticos, o frame é descartado.

#### Endereços Media Access Control (MAC)
É o identificador das placas de interface de rede (NIC) gerenciado pela IEEE.

É composto por 2 identificadores:
- ID do fabricante (identifica o fabricante. Normalmente um fabricante produz só uma categoria de dispostivos)
- Número Serial (identifica o dispositivo unicamente)

Como o MAC usa 6 bytes, cada um dos dois componentes usa 3 bytes. 3 bytes = 24 bits = 6 vezes 4 bits = 6 hexadecimais. Logo, cada componente usa 6 hexadecimais para representar seu valor, totalizando 12 hexadecimais.


### Layer 2 Switch

O switch de camada 2 é o dispositivo responsável por ser um agente intermediário entre várias conexões. Ele possui várias portas físicas em que servidores e clientes podem se conectar e a partir disso, o switch gerencia os frames que vem e vão através de suas conexões.

O gerenciamento é feito através da tabela de endereços MAC. A tabela possui duas colunas, uma com as identificações de suas portas físicas e outra com os endereços MAC. Já a nível de hardware, o switch possui um Application Specific Integrated Circuit (ASIC): um pequeno ciruito integrado responsável por ler os endereços MAC de origem e destino dos nossos *frames*.

- MACs e Frames de Broadcast

Assim como nos endereços IPs, os switches de Camada 2 também podem enviar mensagens de broadcast a nível de camada 2. Seu uso é muito mais comum e abrangente do que pacotes com endereço IP para broadcast, mas tem um funcionamento similar.

Um endereço MAC é para broadcast quando for *FF-FF-FF-FF-FF-FF*, última combinação disponível, assim como os IPs. O *frame de ethernet* com endereço MAC de destino sendo um endereço MAC de broadcast vai ser considerado um frame para broadcast. Um switch de Camada 2 considera um *frame de broadcast* como um frame que deve ser encaminhado para todas os outros clientes e portanto, replica a mensagem para todos os computadores clientes conectados às suas portas, com exceção da porta de onde veio o pacote.

Todos os computadores clientes conectados ao switch de camada 2 e que irão receber o frame de ethernet são chamados de ***Domínio de Broadcast***.

Domínios de Broadcast são um assunto importante e crítico que deve ser abordado aqui com cuidado. Vejamos os casos:

1. *O que acontece se um switch se conectar a outro switch que por sua vez possui mais computadores clientes? A mensagem broadcast no switch original vai chegar no computador cliente do novo switch?*

A resposta é sim, o novo switch está no domínio de broadcast do switch original e quando aquele receber uma mensagem de broadcast fará questão de reenviar a mensagem para todo o seu próprio domínio de broadcast, com exceção da porta de conexão com o switch original, já que esta é a porta de origem do frame de ethernet.


2. *Se conectarmos dois switches um com o outro através de duas portas, a capacidade da rede aumenta?*

Não e sim. Se fizer isso sem nenhuma preparação prévia, causará um problema justamente nos domínios de broadcast da rede. Quando algum computador cliente enviar um frame em broadcast, imaginemos que essa mensagem vá para o switch A que por sua vez a reenvia através do resto de suas portas, ou seja, para os clientes diretos do switch A e para o próprio switch B. Aí já temos um problema, já que o switch B vai receber a mensagem duplicada, já que está conectado por 2 portas no switch A. Posteriormente quando o switch B encaminhar o frame de broadcast para as suas próprias portas, cada frame vai ser enviado para todas as portas, com exceção da sua porta de origem. Isso vai fazer com que o switch A receba novamente os dois frames. Isso vai continuar, gerarando um loop e uma sobrecarga na rede até que a rede pare. Isso é chamado de **tempestade de broadcast**. switches conseguem previnir tempestades de broadcast usando o ***Spanning Tree Protocol (STP)***, responsável por identificar essa porta repetida e bloquear a passagem de dados pela porta.

Foi "não" grande esse, não foi? Há como fazer essa ideia dar certo usando o ***Link Aggregation Control Protocol (LACP)***, responsável por realizar uma agregação de portas. Ele realiza exatamente a ideia proposta no enunciado fazendo com que o switch considere ambas as portas como se fossem uma só, mas utilizando a capacidade de ambas.

- Virtual Local Area Networks

A ideia por trás de VLANs é "como dividir diferentes áreas de broadcast na minha rede?". A intenção é tomar controle da criação de domínios de broadcast e organizá-los virtualmente, sem ter que mudar a infraestrutura física da rede, somente a virtual.

As VLANs são somente domínios de broadcast, mas, ao invés de incluírem no domínio todos as portas ativas com computadores clientes conectados e excluírem a porta fonte do frame, as VLANs também consideram os parâmetros de *etiquetagem*.

Etiquetagem é a chave para entender as VLANs. Toda mensagem em uma VLAN recebe uma etiqueta, incluída no cabeçalho do frame. Ela por sua vez indica a para qual VLAN o frame será encaminhado. Isso muda tudo, porque a partir daí podemos definir quantas VLANs quisermos conectados a um switch e os frames de broadcast serão encaminhados para as suas respectivas VLANs.

Para suportar a etiquetagem, switches devem usar o protocolo *802.1q*. Com o protocolo 802.1q, os switches configuram suas portas com as etiquetas correspondentes das conexões, evitando com que os computadores clientes também tenham que ter suporte ao potocolo e receber a etiqueta com o frame. Entretanto um outro switch conectado precisa receber a etiqueta para reencaminhar o pacote de dentro às suas próprias portas ativas e por isso precisa do protocolo 802.1q também. Dois dispositivos com suporte ao protocolo 802.1q serão capazes de configurar uma *conexão truncada*, responsável por transportar o frame junto à etiqueta correspondente.

Veja como fica essa confusão de domínios de broadcast na prática:

![VLANS]()


- Espelhamento de portas

Técnica de se conectar a um switch ou alguma parte da rede e espelhar o tráfego acontecendo ali para a sua máquina. Muito usado em resolução de problemas na rede e é também o que ferramentas como o Wireshark fazem.

- Power over Ethernet (PoE)

É uma tecnologia em swithes especiais que possibilita energizar aparelhos conectados ao switch uma recarga. Feito através de 2 protocolos:

- 802.3af (2003): gera até 15.4 Watts DC.
- 802.3at (2009): gera até 25.5 Watts DC. O aumento de capacidade culminou no nome "PoE+".

### Roteadores, DOCSIS e ARP.



### Cable Modem Router

## ARP