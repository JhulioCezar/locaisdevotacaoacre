# Onde votar • Acre

Aplicação responsiva para consultar locais de votação do Acre, com dados públicos do TRE-AC.

## Recursos

- Botão Pesquisar: os resultados aparecem somente após enviar a busca.
- Pesquisa por seção obrigatória e filtros opcionais de município e zona.
- Lista de todos os locais com busca por nome ou endereço.
- Filtros por município, zona eleitoral e seção.
- Reconhecimento de seções agregadas e números com zeros iniciais.
- Mapa, rota a partir da localização do dispositivo e cópia do endereço.
- Layout adaptado para celular.

## Arquivos

| Arquivo | Função |
| --- | --- |
| index.html | Página principal |
| style.css | Estilos e layout responsivo |
| app.js | Busca, filtros e ações |
| data.json | Base com 660 locais em 22 municípios |
| .nojekyll | Publicação estática no GitHub Pages |

Não precisa de instalação, banco de dados, Node.js, chaves de API ou serviços pagos. O navegador carrega a base JSON junto com a página.

## Publicar no GitHub Pages

1. Extraia o ZIP.
2. Crie um repositório público no seu GitHub, por exemplo `locais-votacao-acre`.
3. Envie os arquivos de dentro desta pasta para a raiz do repositório. O `index.html` deve ficar diretamente na raiz, não dentro de outra pasta.
4. No repositório, abra **Settings → Pages**.
5. Em **Build and deployment**, selecione **Deploy from a branch**.
6. Selecione a branch **main** e a pasta **/(root)**, e clique em **Save**.
7. Aguarde a publicação. A página Pages exibirá o endereço do site.

Endereço padrão para um repositório desse nome: `https://SEU-USUARIO.github.io/locais-votacao-acre/`.

Depois da publicação, qualquer pessoa poderá acessar o site pelo link, sem login no ChatGPT ou GitHub.

## Testar no computador

Abra um terminal dentro da pasta do projeto e execute:

```bash
python -m http.server 8000
```

Abra `http://localhost:8000` no navegador. Em alguns computadores, use `python3` ou `py` no lugar de `python`.

Abrir `index.html` diretamente por duplo clique pode impedir o carregamento do JSON por restrições do navegador. Use um servidor local ou o GitHub Pages.

## Fonte e atualização dos dados

Fonte: https://planeleito.tre-ac.jus.br/rotas-publicas/locais-votacao

Base consultada em **03/10/2026**, com **660 locais** e **22 municípios**.

A base é uma cópia da consulta nessa data. Ela **não se atualiza automaticamente**. Para atualizar, substitua os registros de `data.json` com dados conferidos da fonte oficial e ajuste a data mostrada em `index.html` e nos textos de cópia em `app.js`. Não altere apenas a data sem atualizar os dados.

Estrutura de cada local:

```json
{
  "zone": 1,
  "city": "RIO BRANCO",
  "name": "NOME DO LOCAL",
  "address": "ENDEREÇO INFORMADO PELO TRE-AC",
  "sections": ["005", "009(011)"],
  "notes": ["Seção agregada"],
  "details": []
}
```

Os números entre parênteses são preservados conforme a fonte. O mapa pesquisa pelo nome do estabelecimento, endereço e município. A base não contém coordenadas verificadas nem Place IDs, portanto alguns locais podem continuar exigindo confirmação no Google Maps. Para ligar diretamente a um estabelecimento já conferido, adicione o campo opcional `placeId` ao registro correspondente no `data.json`; os links de mapa e rota passarão a usar esse identificador. Não preencha esse campo com um valor inventado.

## Escopo

Aplicação independente, sem vínculo institucional com o TRE-AC. Pesquisa locais e seções, não eleitores por nome ou CPF. Não coleta cadastros. A medição de acessos é opcional e depende da configuração descrita abaixo.

## Nova interface de aplicativo

Município e zona são opcionais e começam em Todos. A seção é obrigatória na pesquisa. Listar todos os locais dispensa a seção e respeita o município e a zona selecionados. Na lista, é possível pesquisar nomes e endereços. Nova pesquisa volta à tela inicial, preserva município e zona e limpa a seção.

O botão Traçar rota pede localização do dispositivo somente ao ser acionado. Em caso de recusa ou indisponibilidade, abre o Google Maps para informar o ponto de partida. Exige HTTPS e permissão no navegador. As coordenadas são enviadas ao Google Maps, não ao contador. O destino continua dependendo do endereço da base até que suas coordenadas sejam adicionadas.

Para usar coordenadas verificadas, adicione os campos numéricos `latitude` e `longitude` a cada registro em `data.json`, em graus decimais. Exemplo de formato: `"latitude": -9.123456, "longitude": -67.123456`. Esses números são apenas exemplo de formato, não correspondem a um local cadastrado. Também há suporte ao campo opcional `placeId` do Google Maps.

## Ativar contador de acessos

O contador GLOBAL precisa de uma conta externa, porque o GitHub Pages não executa banco ou servidor. A integração GoatCounter está pronta, mas DESATIVADA até configurar sua conta. Nenhum contador local é exibido como total global.

1. Crie sua conta/site em https://www.goatcounter.com/ e cadastre o endereço https://jhuliocezar.github.io/locaisdevotacaoacre/.
2. No arquivo `config.js`, preencha `goatcounterCode` com o código do seu site GoatCounter. Se seu endereço for `https://meu-codigo.goatcounter.com`, use apenas `meu-codigo`.
3. Nas configurações do GoatCounter, habilite **Allow adding visitor counts on your website**, se desejar mostrar a contagem no rodapé. O painel particular funciona mesmo sem mostrar o total no site.
4. Publique o `config.js` atualizado no GitHub.
5. Visite o endereço público e confira o painel do GoatCounter. A contagem começa após ativação e não recupera acessos anteriores.

O código só mede visitas em `jhuliocezar.github.io`; para hospedar em outro domínio, ajuste `analyticsHost`. Zona, seção, município, coordenadas e parâmetros de URL não são enviados ao contador. O contador depende de rede e pode ser bloqueado pelo navegador. Contagem representa visitas segundo a regra de sessões do GoatCounter, não comprova quantas pessoas distintas votaram ou usaram a pesquisa. Se a leitura do contador falhar, ele fica oculto e a pesquisa continua funcionando.
