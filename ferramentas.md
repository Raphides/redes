# Ferramentas de Rede

## Ferramentas exclusivamente de Software

### ipconfig / ifconfig
Mostra as informações básicas atuais da sua interface de rede, como placa de rede, endereço IP nas redes atuais, se permite IPv4 ou não, máscara de rede, gateway, etc.

### Ping / ICMP
Semelhante as chamadas de telefone, seu funcionamentose dá por: 

1.	Sua máquina envia um pacote de dados.
2.	O receptor recebe o pacote e o devolve sem mexer nele.
3.  O remetente recebe de volta o pacote, checando assim:
    
    a. Existência Conexão: se há uma conexão entre as máquinas.
    
    b.  RTT (round to trip): o tempo de transmissão total da mensagem. É a soma dos Echo Request (tempo de transmissão do remetente ao receptor) e Echo Reply (tempo de transmissão do receptor ao remetente). 
    
    c.	TTL (Time to Live): é um número de 1 byte que indica a quantidade restante de computadores pela qual um pacote de dados pode percorrer. O TLL é criado com um valor máximo e vai tendo uma unidade removida a cada computador que passa. Quando o TLL chega a zero, todo roteador tem uma função responsável por eliminar o pacote, evitando assim a possibilidade de mensagens transitando infinitamente na rede em casos de má configuração ou erro.
    
    d.	Data Loss: integridade do pacote, procurando qualquer corrupção, perda ou alteração de dados.

### NSLookup

Verifica algumas informações básicas de rede de um determinado DNS.

### Trace Route no Linux (e tracert no Windows)

Traça a rota do remetente ao destinatário, listando cada intermediário e medindo o RTT de todos. Para isso, ele usa o ICMP para testar a conexão e conseguir os dados.
•	São disponibilizados 3 RTTs para cada máquina, a fim de tentar conseguir uma resposta mais precisa ou identificar alguma alteração repentina na rede.
•	Alguns administradores de rede desativam a resposta ICMP para evitar a engenharia reversa na rede.

### Cisco Packet Tracer

### Wireshark
### Burp Suite Repeator

## Ferramentas de Hardware e Software

### Servidor
### Roteador
### Switch
### Firewall

