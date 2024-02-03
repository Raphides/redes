## Conceitos iniciais
### Protocolos

Protocolo pode ser descrito como uma norma ou regra. Em Redes, quando falamos de protocolo, estaremos direcionando um entendimento mais voltado para procedimento roteirizados, normas e técnicas utilizadas para realizar uma determinada ação. A área de comunicação em si é recheada de protocolos sobre como trocar informações de formas eficientes. Por exemplo, para conversar presencialmente com alguém, necessitamos de:
- Soprar o ar pelas nossas cordas vocais para criar um som.
- Saber expressar esse som numa linguagem que a pessoa entenda.
- Vibrar o ar com o som em:
    - um ângulo aceitável em relação a orelha do ouvinte.
    - uma distância relativamente próxima do ouvinte.
    - Um volume aceitável
    - Etc.

As especificações, requisitos e procedimentos nesta comunicação podem ser traduzidas em um protocolo, assim como descrito acima.
### Servidores 
	São essencialmente computadores que hospedam algum conteúdo. São programados para receber e reponder a requisições.
### Rede
	É considerada uma rede todo ambiente onde pode haver troca de informações e dados entre computadores. Essa “troca de informações” é um termo abstrato para se referir aos vários protocolos que os computadores seguem para de fato realizar essa troca de informações.
## Modelo OSI 
O modelo Open System Interconnect Model (OSI) nasceu nos anos 70 tem o propósito de categorizar os protocolos de rede em camadas de fácil compreensão. A divisão em camadas representa a transferência de informação entre computadores em diferentes perspectivas, permitindo-nos entender melhor onde as dezenas de protocolos atuam. É importante entender que esse modelo é bem teórico, resultando que os protocolos usados atuem em mais de uma camada.

Surgiu com um total de 5 camadas, mas devido a necessidades de segurança em redes, apareceram protocolos que pertenciam a 2 novas camadas. São elas:
1.	**Camada Física** - mais próximo do hardware: camada voltado a protocolos de hardware. Toda comunicação de rede precisa de um hardware preparado, com materiais e medidas certas para o trabalho. Por exemplo, numa rede cabeada, podemos dizer que essa camada com a construção e disposição dos cabos, se usam fios de cobre ou não, etc. Protocolos de rede que atuem na parametrização e normatização na área de hardware atuam na Camada Física.
2.	**Camadas de Encadeamento de dados**: área pertencente a todo protocolo que se preocupa em como os pacotes de dados serão construídos, organizados e distribuídos através da camada física.
3.	**Camada de Rede**: enquanto as camadas 1 e 2 se preocupam com pré-disposições, é na camada 3 que a mágica começa. A camada 3 se utiliza dos aparatos da capacidade de comunicação gerada pelas camadas 1 e 2 para de fato criar uma nova rede ou conectar-se a uma pré-existente. Protocolos desta camada se preocupam em como abrir esta conexão e se organizar perante as outras diversas conexões que uma rede abriga. Um exemplo clássico de protocolo que atua na camada 3 é o IP (Internet Protocol), cuja finalidade reside em localizar e identificar um computador no meio de uma rede para trocar informações. Perceba que um IP facilita bastante a organização na Camada de Rede.
4.	**Camada de Transporte**: estabelecer uma rede e achar o endereço do servidor na rede não é o suficiente para a comunicação, é preciso criar de fato um canal de comunicação com o servidor, ou seja, uma sessão.
5.	**Camada de Sessão**: 
6.	**Camada de Apresentação**: 
7.	**Camada de Aplicação** – Mais próximo do Software: 

Essas camadas podem ser chamadas de ordenadas por estarem classificadas da camada mais próxima de hardware para a mais próxima de software.

