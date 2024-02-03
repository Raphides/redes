# Hypertext Trasnfer Protocol (HTTP)

Um dos protocolos mais utilizados na internet. É o principal responsável pela transferências de hypertextos aos usuários na camada de aplicação.

Entre as suas característics, podemos citar:
- Utiliza a arquitetura Cliente-Servidor.
- Protocolo sem estado. Não salva as informações e/ou autenticações no próprio protocolo, tendo que reenviar as informações de autenticaçãoo toda vez a fim de autenticar uma comunicação ou identificar uma sessão.

## Uniform Resource Locator (URL)
É um elemento de mapeamento, nomeação e identificação de recursos em um domínio. Os protocolos da camada 7 utilizam as URLs para se referir aos recursos na internet.

Estrutura básica

```
protocolo:servidor:porta/caminho-de-recurso
protocolo:servidor:porta/caminho-de-recurso?consulta
protocolo:servidor:porta/caminho-de-recurso#fragmento
```

1. protocolo: protocolo utilizado na comunicação. http, ftp, file (local), etc.
2. servidor: nome do domínio do servidor. Deve ser precedido de duas barras, uma para indicar de fato o caractere da barra e outra para evitar que seja ocnsiderado um "escape", ficando: "protocolo://domain-name"
3. porta (opcional): especifica a porta a ser utilizada na comunicação.
4. caminho-de-recurso: precedido de uma barra para indicar o diretório raiz, o caminho indica de fato o caminho a ser percorrido no respectivo servidor do domínio para adquirir o recurso requerido. Caminhos podem ou não mostrar a extensão de arquivo associada ao recurso.
5. consulta: refere-se a uma pequena string de par chave-valor enviada ao servidor para filtrar resultados. Antigamente era usado para autenticação, mas não é recomendado. A estrutura é `parametro=argumento` e usa-se `&` e `|` para adicionar mais parâmetros. Precedido sempre por interrogação.
6. fragmento: precedido sempre por `#`, indica uma parte do recurso. normalmente usado para referir-se a algum título do HTML. A página é mostrada completamente, mas começa a visualização na posição do fragmento