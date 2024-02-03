# Encapsulaemnto de Dados

O modelo OSI é bem dividido, mas na prática, todos os protocolos e informações são transportados através de bytes transmitidos por fios. Como esses bytes são organizados para carregar os dados de cada protocolo em cada camada. Vamos mostrar um processo bem cohecido desse encapsulamento.

Vamos começar da camada 7, de forma mais simples. Imaginemos que você está pedindo uma página HTML para um servidor dentro da web. Você primeiro manda uma:

## Requisição HTTP

Série de bytes que encapsula o cabeçalho e o corpo de uma requisição HTTP / HTTPs. Entretanto o HTTP só possui as informações para adquirir o HTML. Antes disso, você precisa das informações das camadas anteriores, por isso essa requisição será somada e virará um:

## Segmento de dados

Série de bytes que encapsula uma requisição HTTP com o cabeçalho TCP da camada de transporte e outras possíveis informações relevantes das camadas 5 e 6. Um cabeçalho TCP deve possuir informações das portas utilizadas do 

- Porta de Origem
- Porta de Destino
- +Requisição HTTP

Mas não adianta saber as portas usadas sem saber qual computador direcionar o segmento de dados na rede. Por isso adicionaremos mais informações, transformando o segmento em um:

## Pacote de dados

Série de bytes que encapsula um segmento de dados com informações de identificação na rede. Mais comumente utilizado para com a seguinte estrutura:

- IP de Origem
- IP de destino
- +Segmento de Dados

## Frame de Dados

Série de bytes que encapsula um pacote de dados com identificação identificação de das interfaces de conexão de redes dentro de computadores. Possui a seguinte estrutura:

- Endereço MAC de Origem
- Endereço MAC de Destino
- +Pacotes de Dados

