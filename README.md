# MUSE-releases

O que o **app MUSE** baixa sem login: o próprio app, o firmware do painel, os dados
do modo offline e os catálogos das estradas. O MUSE é um painel para motocicleta:
app Android, firmware do painel e carcaça impressa.

**Este repositório não tem código e não roda nada.** Ele guarda o que é publicado,
como anexos de releases de etiqueta fixa, e a [política de privacidade](PRIVACY.md)
do app. O projeto do MUSE fica num repositório privado, e o GitHub não entrega anexo
de release privada sem login. Como o app baixa sem login, o que ele baixa precisa
morar num repositório público. É para isso que este existe.

---

## As releases

| Etiqueta | O que guarda | Quando muda |
|---|---|---|
| [`app`](https://github.com/Memphyz/MUSE-releases/releases/tag/app) | O app Android, que se atualiza sozinho | A cada versão |
| [`firmware`](https://github.com/Memphyz/MUSE-releases/releases/tag/firmware) | O firmware do painel, que o app instala por Bluetooth | A cada versão |
| [`offline-data`](https://github.com/Memphyz/MUSE-releases/releases/tag/offline-data) | Os alertas da via e a camada de vias, por estado | Alertas todo dia; vias no dia 1 de cada mês |
| [`rota-biker`](https://github.com/Memphyz/MUSE-releases/releases/tag/rota-biker) | Os monumentos do passaporte da Rota Biker | Todo dia |
| [`blue-lanes`](https://github.com/Memphyz/MUSE-releases/releases/tag/blue-lanes) | A Faixa Azul de São Paulo | Toda segunda-feira |
| [`ride-roads`](https://github.com/Memphyz/MUSE-releases/releases/tag/ride-roads) | As estradas do modo passeio | Dia 2 de cada mês |

### `app`

| Arquivo | O que tem |
|---|---|
| `app-manifest.json` | A versão mais recente e as notas de cada versão |
| `muse-app-X.Y.Z.apk` | O app assinado. Ficam as **três** versões mais novas |

### `firmware`

| Arquivo | O que tem |
|---|---|
| `firmware-manifest.json` | A versão mais recente, o tamanho, o SHA-256 e as notas de cada versão |
| `muse-fw-X.Y.Z.bin` | O firmware da moto. Ficam as **três** versões mais novas |

Só o build da moto é publicado. O app oferece a atualização, mostra as notas da
versão e transfere por Bluetooth. Quem quiser voltar a uma versão anterior instala
de um arquivo, pelo próprio app.

### `offline-data`

| Arquivo | O que tem |
|---|---|
| `manifest.json` | O índice dos alertas: versão do formato, quando a rodada foi gerada (`generatedAt`, em UTC), as fontes com a data de cada uma, e o tamanho de cada estado |
| `regions.json.gz` | Os contornos dos 27 estados (IBGE), para saber em que estado cada ponto está |
| `AC.json.gz` … `TO.json.gz` | Os alertas de cada estado: radares, lombadas, pedágios, semáforos, trechos com acidentes |
| `source-*.json.gz` | Cópias das fontes do governo da última rodada boa. O gerador usa quando uma fonte não responde; o app ignora |
| `roads-manifest.json` | O índice da camada de vias, separado do de alertas: ela é muito maior e se atualiza uma vez por mês |
| `roads-XX.ndjson.gz` | As vias do estado, para baixar inteiras |
| `roads-XX.tiles` | As mesmas vias, quadrado por quadrado, para o app ler só as da rota por HTTP Range, sem baixar o estado |

Cada estado de alertas é uma lista de elementos no formato `out center` do
Overpass (a API de consulta do OpenStreetMap). As fontes do governo entram
traduzidas para as tags equivalentes do OSM, e o que não tem tag no OSM, como os
trechos com acidentes, entra com prefixo `muse:`:

```json
{ "format": 2, "uf": "SP", "generatedAt": "…", "elements": [
  { "type": "node", "id": 123, "lat": -23.56, "lon": -46.65, "tags": { "highway": "speed_camera", "maxspeed": "50" } },
  { "type": "node", "id": -3000000000017, "lat": -22.52, "lon": -43.23, "tags": { "muse:accidents": "30", "muse:deaths": "2" } }
] }
```

Os alertas do Brasil inteiro somam cerca de 4 MB compactados. As vias somam cerca de
**430 MB** para baixar (São Paulo sozinho, ~60 MB), mais ~730 MB dos `.tiles`, que o
app lê aos pedaços: é por isso que elas têm índice próprio e rodada mensal.

### Os catálogos

| Arquivo | Release | O que tem |
|---|---|---|
| `monuments.json` | `rota-biker` | Os monumentos da Rota Biker, de monumentobikers.com.br |
| `blue-lanes.json` | `blue-lanes` | As linhas da Faixa Azul: o texto vem da página da CET, a coordenada vem do OpenStreetMap, e uma linha só é publicada se a quilometragem bater |
| `ride-roads.json` | `ride-roads` | Os trechos sinuosos do modo passeio, medidos nas vias do OpenStreetMap, e os quadrados de área urbana |
| `ride-sources.json` | `ride-roads` | A memória da leitura dos blogs, para a rodada seguinte; o app ignora |
| `ride-sources.md` | `ride-roads` | O relatório dessa leitura; o app ignora |

Os blogs só dão nome e fama a um trecho, nunca decidem por onde a rota passa.

---

## Como é atualizado

Tudo sai de workflows do GitHub Actions no repositório do MUSE, que escrevem aqui
com um token *fine-grained* restrito a este repositório (*Contents: Read and write*),
guardado nos secrets de lá.

| O quê | Quando (Brasília) |
|---|---|
| App | Quando entra uma versão nova no changelog do app |
| Firmware | Quando entra uma versão nova no changelog do firmware |
| Alertas | Todo dia, 05:00 |
| Rota Biker | Todo dia, 05:30 |
| Faixa Azul | Toda segunda, 06:00. Quase sempre só compara a página da CET; a leitura do OpenStreetMap roda na primeira segunda do mês |
| Vias | Dia 1, 08:00. Três horas depois da rodada de alertas, para as duas nunca publicarem ao mesmo tempo |
| Modo passeio | Dia 2, 08:00. Um dia depois das vias, de onde sai a medição |

Os agendados também podem ser rodados à mão.

Na `offline-data`, os estados sobem primeiro e o índice por último, cada arquivo
trocado no lugar. Quem baixar no meio da troca ainda lê o índice antigo, que continua
batendo com os arquivos.

Se uma fonte do governo não responder, a rodada usa a cópia da rodada anterior
(`source-*.json.gz`). Se o OpenStreetMap ou o IBGE falharem, a rodada inteira falha e
a publicação anterior continua valendo. O modo passeio faz o mesmo se o país sair com
menos de 300 trechos.

## Como o app usa

| O quê | Quando o app confere |
|---|---|
| App | A cada abertura |
| Firmware | Ao conectar o painel |
| Alertas e vias | Ao abrir, no máximo a cada 12 horas |
| Rota Biker | No máximo a cada 12 horas |
| Faixa Azul | No máximo a cada 24 horas |
| Modo passeio | No máximo a cada 7 dias |

O app baixa sozinho o estado de quem usa e os estados de cada rota iniciada, e o
Brasil inteiro se o piloto ligar em Ajustes > Armazenamento. Se o `generatedAt` for
de uma rodada mais nova que a do aparelho, ele baixa esses estados de novo. As vias
só se atualizam sozinhas em rede sem franquia. Dentro da área baixada, o app responde
do próprio banco, sem consultar a rede. O dado baixado não expira: sem rede, o app
continua com o que tem.

---

## Cuidados para não quebrar o app

- **Mantenha este repositório público.** Privado, o download do app dá 404.
- **Não apague as releases acima, nem mude as etiquetas ou os nomes dos arquivos.**
  Eles fazem parte do endereço gravado no app. Outras releases aqui não atrapalham,
  porque o app usa essas etiquetas fixas e nunca a "latest".
  Se uma release for apagada por engano, o workflow correspondente a recria na rodada
  seguinte. A `offline-data` também guarda o `regions.json.gz`, do qual a rodada de
  vias depende para não ir ao IBGE: rode **alertas antes de vias** para se recuperar.
  E a `ride-roads` lê as vias: rode **vias antes do modo passeio**.
- **Não mova nem apague o `PRIVACY.md`.** O app abre a política por este endereço.
- **Não renomeie este repositório** sem antes acertar o `PublicReleases.kt` no MUSE e
  publicar um app novo: o endereço fica gravado no app instalado.
- **Não arquive o repositório.** Repositório arquivado não aceita anexo novo, e tudo
  para de atualizar.
- **Não coloque os pacotes no git.** Eles vivem só como anexos das releases, que os
  workflows trocam.

---

## Fontes e licenças

| Fonte | O que vira | Licença |
|---|---|---|
| OpenStreetMap, extrato do Brasil da Geofabrik | Tudo o que os filtros de alerta do app encontram (radares, lombadas, semáforos, PARE, pedágios, cruzamentos de trem…), a camada de vias, com o limite de velocidade e o piso, e as coordenadas da Faixa Azul e do modo passeio | ODbL |
| ANTT: radares e praças de pedágio das rodovias federais concedidas | Radares com o limite de velocidade, e praças de pedágio | CC-BY |
| DNIT e DER-SP | Radares | Não conferida |
| PRF: boletins de acidentes (últimos 3 anos) | Trechos de 1 km com 10 ou mais acidentes | Não conferida |
| IBGE: malhas territoriais | Contornos dos estados | — |
| CET São Paulo | Quais vias têm Faixa Azul | Não conferida |
| monumentobikers.com.br | Os monumentos da Rota Biker | Não conferida |

Os dados do OpenStreetMap são **© colaboradores do OpenStreetMap**, sob a
[Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/). Quem
reusar precisa dar esse crédito, e um banco derivado distribuído publicamente segue a
mesma licença. O `manifest.json` de cada rodada lista as fontes que entraram e a data
de cada uma.
