# Camada Física
Camada referente às regras e procedimentos na prepração e organização física dos equipamentos de rede.

## Cabos de metal / cobre
- Ideal para distâncias curtas (até uns 300 metros)
- Barato

### Cabos de par trançado (Twisted Pair Cable)

Usando a ideia básica de transportar através de fios condutores de eletricidade, deparamo-nos com um problema quando adicionamos mais de um fio por cabo, os **campos eletromagnéticos**.

Ao passar eletricidade por um cabo, uma corrente magnética é gerada em volta. Da mesma forma, ao passar uma corrente magnética perto de um cabo, eletricidade é gerada e movida. Assim, dois fios um ao lado do outro vão interferir na passagem de sinais um do outro, causando informações danificadas.

Para solucionar isso, usamos os cabos de par trançado! Com conhceimento de eletromagnética, trançamos os fios em posições muito específicas, anulando o campo eletromagnético e permitindo mais fios em um só cabo.

Para possibilitar ainda maior quantidade de fios e informação transmitida, cabos de par trançado mais capazes incluem uma placa de plástico interna separando os fios em uma tentativa de evitar troca de sinais. Muito usado em cabos capazes de transportar de 1 até 10 Gbps.

Outro adicional que cabos mais capazes possuem é uma malha de alumínio. Ela é usada para isolar os fios do cabo de interferência magnética do ambiente externo. Cabos com essa proteção são chamados de *Shielded Twisted Pair (STP)* e os sem proteção são chamados de *Unshielded Twisted Pair (UTP)*.

Exemplos de cabos que usam esse protocolo:
- Cabo Ethernet

#### Conector RJ-45
Bem conhecido por serem usados em cabos ethernet. Seus fios internos possuem uma organização específica e importante na conexão com os pinos (extremidades dos conectores) dos dois conectores para o funcionamento do cabo. As especificações da pinagem (para o posicionamento e organização dos fios e os pinos) estão na norma *EIA/TIA-568-A* e *EIA/TIA-568-B*

Todo cabo RJ-45 possui uma série de 4 pares de fios, totalizando 8 fios, em que cada par tem uma cor correspondente x. O primeiro fio do par é sempre listrado com as cores branca e x, enquanto o segundo fio do par é completamente preenchido pela cor x. Todo cabo possui duas extremidades e cada uma delas podem ter duas configurações, ***T568-A e T568-B***. A diferenteça entre as duas terminações se dá pela ordem do posicionamento dos fios. Veja a imagem abaixo para entender.

[Terminações T568-A e T568-B]()

Cabos com ambas as terminações do mesmo tipo não precisam de nenhuma adaptação especial em sua organização, portanto os fios vão **direto através do cabo (Straight Through Cable)**, apresentando-se na mesma ordem de disposição em ambas as terminações. Entretanto ao conectar terminações T568A com T568B, os fios fazem um **cruzamento pelo cabo (Crossover Cable)**, mudando assim a ordem de disposição dos cabos para coincidir com ambas as terminações. É importante saber como é a terminação do seu cabo e sua pinagem, pois se ele usadas as conexões indevidas entre as terminações, é capaz do cabo perder 70% da sua capacidade de transporte.

Conexões entre computadores e switches normalmente usam Straight Through Cables, mas quando conectamos computadores com outros computadores ou switches com outros switches, precisamos usar Crossover Cables.

- Auto-Medium-Dependent-Interface Crossover (Auto-MDI-X): é uma tecnologia de software presente na maioria dos computadores modernos. Ela é responsável por ajustar eletronicamente as pinagens dos cabos, diminuindo a perda de capacidade por conexões indevidas no uso de cabos. O software faz isso através da análise da placa de rede do dispositivo.

### Cabo Coax
#### RG-6
#### Conector F-type
#### Twinaxial Cable
Usado mais em datacenters para transmitir dados em alta capacidade, compatível com 10 Gbps até 40 Gbps. Usam conectores SFP, que vão ser mais abordados posteriormente na Fibra Óptica.


## Fibra Óptica
A ideia é transmitir informação codificada em ondas eletromagnéticas (luz) através de um cabo grosso com um pequeno cilindro interno de vidros e espelhos que ajuda na propagação e conservação da luz.

---
|Característica|Single Mode|Multi Mode|
|-|-|-|
|Cor|Amarelo|Laranja (comum) ou Verde-Aqua (raro)|
|Distância|10 km ou mais|Cerca de 1 km|
|Direção da luz|Paralelo a direção do cabo|Normalmente vai batendo nas bordas|
|Preço|Muito caro|Caro|
|Qualidade do vidro|Alta|Média/baixa|
|Tipo do Laser|LX/LR|SX/SR|
---

### Conecores de NIC
Conectores NIC são bem diferentes por possuírem *placas de interface de rede (NIC)* em suas extremidades. São usados em fibras ópticas e cabos twinaxiais e os conectores NIC mais utilizados são os SFPs. Estes são os sucessores dos conectores GBIC, outros que possuem NICs em suas extremidades, mas são consideravelmente maiores do que os SFPs e atualmente são considerados tecnologia legada. Além do GBIC e do SFP, também é possível encontrar QSFP, que possui 4 vezes a capacidade de um SFP comum, sendo normalmente usado em datacenters e acompanha até mesmo uma cor diferente em seu cabo multi-mode, o verde. Tanto o SFP quanto o QSFP hoje em dia possuem versões melhoradas, os SFP+ QSFP+.

É interessante entender que conectores NIC não são conectados diretamente no cabo. Eles são dispositivos separados da fibra e possuem duas extremidades, uma com o NIC em si e outra com um conector próprio da fibra óptica. Este último nós vamos estudar agora.

### Conectores próprios das fibras ópticas
- LC (mais comum)
- ST
- SC
- MTRJ (raro)
- FC (raro)

### Conexões de fibras
Fibras Ópticas podem ser extremamente frágeis, principalmente as Single Mode. Por isso é comum que as fibrar passem por um *patch panel* antes de se conectarem ao Switch.

Um *patch panel* é uma espécie de intermediário na conexão. Ele termina a fibra óptica e começa outra fibra óptica, passando o sinal entre elas. A fibra entre

`Computador <-----> Patch Panel`

costuma ser mais cara e fráfil do que a fibra entre

`Patch Panel <---> Switch`,

resultando numa maior manipulação da fibra mais barata e menos perda de dinheiro em caso de problemas nesta fibra.

Dentro das conexões de um *patch panel*,cada fibra óptica a ser terminada (mais cara) deve ter cada um de seus pequenos fios de vidro conectados a nova fibra (mais barata). Para realizar esta conexão, existem dois métodos:


- Angled Physical Contact (APC)

Contato entre fibras ópticas cortadas num ângulo específico. Infelizmente gera uma certa perda de luz. Veja a iamgem.

- Ultra Physical Contact (UPC)

Contato no formato de funil entre as fibras. Dessa forma, ocorre uma afunilação da luz e a informação não perde tanta luz. Veja a imagem.


### Operações de Fibra Óptica

As fibras ópticas podem transportar as informações através de operações distintas.

- Par Simplex

Fibras ópticas com fios de transporte unidimensional. Cada fio transmite em um única direção a informação. Dessa forma, alguns fios vão para uma direção e outros para a direção oposta. Em cada extremidade de cada fio pode haver um "ouvinte" de sinal e um "transmissor" de sinal.


- Par Bidirecional

Um único fio possui tanto ouvintes quanto transmissores em cada extremidade. Fibras bidirecionais transmitem então ondas em ambas as direções, mas, para evitar interferências, usam diferentes comprimentos de onda.

A tecnologia responsável por dividir as informações em ondas de diferentes comprimentos é chamada de *Wave Division Multiplexing (WDM)*. O WDM não é um segredo ou algo extremamente complexo, ele usa o princípio de transmissão de luz através de prismas:
- Um raio de luz através de um prisma é multiplexado, transformando-se um um arco-íris.
- Um arco íris através de um prisma é demultiplexado, transformando-se novamente em um raio completo.

WDM podem ser divididos em:
- Coarse WDM (CWDM): funcionamento passivo, funciona sem energia.
- Dense WDM (DWDM): precisa de energia, mas cobre maiores distâncias e maiores amplitudes de onda.

## Bluetooth

