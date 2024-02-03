# Camada de Rede
## Internet Protocol (IP)
É o endereço de um sistema eletrônico na rede da internet. Uma boa alusão seria um endereço de casa/apartamento, já que segue a mesma lógica. Para enviar um pacote de dados a um computador, você precisa saber seu IP da mesma forma que uma pessoa precisa saber seu endereço da sua moradia para lhe mandar uma carta.

Para contextualização, quando uma rede é criada, os parâmetros de identificação do seu dispositivo na rede, como o IP, podem ser definidos manualmente ou automaticamente distribuídos através de um servidor DHCP. DHCP é um protocolo (de camada 7) e serviço responsável por gerenciar os endereços de IP numa rede. Ele oferece endereços de IP automáticos aos dispositivos conectados na rede, sendo extremamente necessários na configuração de qualquer rede. Outro protocolo complementar ao IP e igualmente importante é o TCP. Enquanto o IP é responsável por identificar dispotiivos na rede da mesma forma que números de casa em condomínios, o TCP serve como o carteiro do bairro. O TCP é um protocolo de camada 4 responsável por usufruir dos endereços IPs para estabelecer conexões e manter uma comunicação entre dispositivos na rede. O protocolo será mais abordado na [sessão de transporte](./camadas-osi/4-transporte.md).

O endereço IP é um protocolo comum de camada OSI 3 que identifica a sua máquina em uma rede usando uma série de bytes única, com o IPv4 possuindo 4 bytes e o IPv6, 16 bytes.

### Estrutura comum de IPs e máscaras.
Os IPs, seja o v4 ou o v6, terá uma estrutura comum de:
- **Seção da rede**: seção do IP que indica qual o endereço da rede na qual o host está conectado. Todo computador na mesma seção de rede da sua está na mesma rede que você.
- **Seção de host**: seção que identifica o seu host em específico dentro daquela rede. Numa rede ativa, cada máquina deve ter um IP único.

Como identificar cada seção? Usando as **máscaras de rede**:

#### Máscara de Rede
É uma série de bytes de tamanho igual ao IP utilizado. Compare o IP e a máscara bit a bit. Para cada bit 1 na máscara, o bit do IP na posição correspondente será referente à seção de rede. Enquanto os bits 0 representam a posição dos bits do IP que fazem parte da seção host. Na prática:
- os bits de rede e host são sequencias. Não existe máscara cm bits intercalados como 10101. São bits do tipo 1100000.
- Os bits de rede sempre vem primeiro, logo o primeiro bit nunca será 0.
- O tamanho de cada seção é variável.

A representação clássica da máscara é através de `/` + `quantidade de bits de rede`. Exemplo:

- `/24`  = máscara de rede começa com 24 bits com valores 1 e o resto com 0. 24 primeiros bits de rede.

#### Endereços de Rede e Broadcast
Dentro de uma rede, os IPs disponíveis para os dispositivos dentro daquela rede são no máximo o intervalo de IPs com a seção de rede fixa.

**Ou seja, é a permutação das possibilidades de endereços host.**

Mas isso não é completamente verdade, porque tanto no IPv4 quanto no IPv6, há ao menos dois IPs reservados:
- **IP de Rede / Roteador**: é sempre o IP de menor valor da rede, o primeiro. É o IP reservado para conexão com o roteador da rede.
- **IP de Broadcast**: É sempre o IP de maior valor numérico da rede, o último. Broadcast é quando mandamos um sinal de um IP para todos os ouvintes de uma rede. Por exemplo, podemos citar o VoIP.



### IPV4
Estrutura clássica de IP, dividida em classes e é usada até hoje. É uma série de 4 bytes, analisando cada byte individualmente. Cada byte é separado por ponto em sua representação. Tendo cada byte 256 valores possíveis, os endereços IPs vão de `0.0.0.0` até `255.255.255.255`.



#### Máscara de Rede IPV4
É difícil ver os bits de rede e host no IPV4, portanto é comum a transformação para binário quando há a análise máscaras.

Vejamos alguns exemplos:

```txt
IP: 192.253.72.6 (11000000.11111101.01001000.00000110)
Máscara: 255.0.0.0 (11111111.00000000.00000000.00000000)
Seção de Rede: 192 (11000000)
Seção de Host: 253.72.6(11111101.01001000.00000110)
```

```txt
IP: 173.3.188.1 (10101101.00000011.10111100.00000001)
Máscara: `255.255.252.0`(`11111111.11111111.11111100.00000000`)
Seção de Rede: 10101101.00000011.101111
Seção de Host: 00.00000001
```


#### Classes de IP

|Classe|Intervalo (primeiro octeto)|Padrão de prefixo(binário)|Máscara|Uso|
|-|-|-|-|-|
|A|0-10|0xxxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx|/8|-|
|B|-|10xxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx|/16|-|
|C|-|110xxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx|/24|-|
|D|-|1110xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx|-|IP Multicast|
|E|-|1111xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx|-|Uso Experimental|


#### IPs privados
Recurso exclusivo do IPv4. 

Intervalos:
    - 10.x.x.x (da classe A)
    - 172.16.x.x até 172.31.x.x (da classe B)
    - 192.168.x.x (da classe C)
    
### IPv6
Oficializada em 2012, o IPv6 foi criado devido ao esperado esgotamento de endereços do IPv4. Diferente do IPv4, que usa 4 bytes, o IPv6 usa 
### Máscara de Rede IPV6

### IPs estáticos e dinâmicos 
- **IP estático**: IPs fixos, pré-estabelecidos pelo provedor de internet e/ou no dispositivo. Exemplos: localhost.
    - IPs reservados:
        - Loopback
- **IP dinâmico**: mudam ao longo do tempo de acordo com a disponibilidade. São mais comuns e baratos para as Provedoras de Internet (*Internet Service Provider*, IPS), usados principalmente em redes domésticas.
    - VPNs e Onion usam de uma rápida mudança de IPs para ajudar a mascarar a origem do remetente.

### Internet Message Control Protocol (IMCP)

### ADP