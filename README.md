# Onde votar • Acre

Aplicação responsiva para consultar locais de votação do Acre, com dados públicos do TRE-AC.

## Recursos

- Botão Pesquisar: os resultados aparecem somente após enviar a busca.
- Busca por nome do local, rua ou bairro, sem diferenciar acentos.
- Filtros por município, zona eleitoral e seção.
- Reconhecimento de seções agregadas e números com zeros iniciais.
- Google Maps com nome + endereço + município, botão Como chegar, cópia do endereço e impressão dos resultados.
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

Aplicação independente, sem vínculo institucional com o TRE-AC. Pesquisa locais e seções, não eleitores por nome ou CPF. Não coleta cadastros e não inclui ferramentas de análise de visitantes.
