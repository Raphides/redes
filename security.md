# Fundamentos de Segurança em Redes

##  CIA Original
- Confidencialidade: garantir que pessoas não autorizadas não tenham acesso a documentos não autorizados.
- Integridade: garantir que uma mensagem não tenha seu conteúdo alterado durante o transporte.
- Disponibilidade (Avaliability): manter o serviço funcionando nos respectivos períodos de tempo pré-decididos.

## Outros pilares
- Não repúdio: ninguém pode dizer que não foi você que fez aquilo.
- Legalidade: respeita as leis dos países que atuam, órgãos de controle, boas práticas de mercado, etc.
- Privacidade: 
- Controle de Acesso:
    - Mandatory Access Control (MAC): permissões decididas por ordens de cima. Normalmente usados em bases militares.
    - Discretionary Access Control (DAC): permissões decididas pelos grupos que pertencem.
    - Role Based Access Control (RBAC): permissões baseado em funções / papéis. O mais usado.
    - Attribute Based Acess Control (ABAC): permissões baseados nos projetos e atividades que você produz. Uma tendência atual.

### AAA
- Autentication: Provar que você é quem diz ser.
- Autorization: Provar que você tem autorização para acessar aquilo que quer.
- Accounting: Provar que você de fato fez aquilo, ou seja, registro de logs.

## Ataques de Rede:
### Distributed Denial of Service (DDoS)

### Man in the Middle (MitM)
Quando se intercepta uma mensagem na transmissão de um commputador a outro.

## Defesas de Rede:
### Criptografia
- Criptografia Simétrica.
- Criptografia Assimétrica.

### Fatores de Autenticação
#### Vias de autenticação
- O que você tem? Senha / outro serviço externo comum.
- O que você sabe? Palavra-passe.
- O que você é? Biometria digital e visual.

#### Fatores múltiplos
- 1FA
- 2FA
- MFA

## Modelos e Soluções

### Arquitetura Zero Trust

