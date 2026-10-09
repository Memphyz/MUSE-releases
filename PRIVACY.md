# Política de privacidade do MUSE

Última atualização: 9 de outubro de 2026

O MUSE é um aplicativo de navegação para motociclistas que conversa com um
painel instalado na moto. É um projeto pessoal, sem fins comerciais. Esta página
explica que dados o app usa, onde eles ficam e com quem eles são trocados.

## Resumo

- O MUSE **não tem servidor próprio**. Nada do que você faz no app é enviado
  para o desenvolvedor.
- Não há anúncios, rastreamento, análise de uso nem venda de dados.
- Seus dados ficam no seu celular e, se você quiser, numa pasta escondida do
  **seu próprio** Google Drive.

## O que fica guardado no celular

- Locais salvos (como Casa e Trabalho), rotas salvas e as últimas buscas.
- O histórico das últimas viagens, com o trajeto percorrido.
- Números de uso acumulados (quilômetros, tempo, recordes) e o seu ritmo de
  pilotagem, usado para estimar a hora de chegada.
- Ajustes do app e, se você informar, a sua chave de acesso ao TomTom.
- Mapas e alertas baixados para usar sem internet.
- O pareamento com o painel da moto.

Esses dados ficam no armazenamento do próprio app. O Android pode copiá-los para
um celular novo na transferência entre aparelhos; o pareamento com o painel nunca
é copiado.

## Localização

O app usa a localização do celular para mostrar a sua posição, calcular rotas,
avisar de radares e lombadas e gravar o histórico de viagens. A localização é
usada no próprio celular e só sai dele nas consultas aos serviços de mapa
descritos abaixo.

## Serviços externos que o app consulta

Para funcionar, o app faz consultas a serviços de mapa e clima. Em cada consulta
vai apenas o necessário para a resposta (por exemplo, a sua posição e o destino
para calcular uma rota, ou o texto que você digitou numa busca). Nenhuma delas
leva seu nome, e-mail ou identificação da conta.

| Serviço | Para quê |
|---|---|
| OpenStreetMap (Nominatim e Overpass) | Busca de endereços, limites de velocidade, radares e dados das vias |
| OSRM | Cálculo de rotas |
| TomTom (só se você ativar com a sua própria chave) | Rotas com trânsito, busca de endereços e camada de trânsito |
| Open-Meteo | Previsão do tempo ao longo da rota |
| ViaCEP | Busca de endereço pelo CEP |
| GitHub | Download dos mapas offline e das atualizações do app e do painel |

Cada serviço tem a própria política de privacidade.

## Sincronização com a conta Google (opcional)

Se você conectar uma conta Google em Ajustes > Conta, o app guarda uma cópia dos
seus dados numa **pasta escondida do seu Google Drive** (a pasta de dados do
aplicativo), para você recuperá-los em outro celular. Vão para lá os locais e
rotas salvas, as últimas buscas, o histórico de viagens, os números de uso, o
ritmo de pilotagem e os ajustes, incluindo a chave do TomTom, se houver.

- O app pede acesso **somente** a essa pasta (permissão
  `https://www.googleapis.com/auth/drive.appdata`). Ele não vê nem altera nenhum
  outro arquivo do seu Drive.
- Os dados vão do seu celular direto para a sua conta Google. O desenvolvedor
  não tem acesso a eles.
- Você pode desconectar a conta e apagar a cópia a qualquer momento em
  Ajustes > Conta > Apagar dados da nuvem. Também pode remover o acesso do MUSE
  nas configurações da sua conta Google (Segurança > Apps de terceiros com acesso
  à conta).

O uso dos dados recebidos das APIs do Google segue a
[Política de dados do usuário dos serviços de API do Google](https://developers.google.com/terms/api-services-user-data-policy),
incluindo os requisitos de Uso Limitado.

## Bluetooth

O app envia ao painel da moto, por Bluetooth, os dados que o painel mostra: rota,
velocidade, avisos, hora e tema da tela. Essa conexão é direta entre o celular e
o painel.

## Apagar os seus dados

- Desinstalar o app apaga tudo o que ele guardou no celular.
- Em Ajustes > Números é possível apagar os números e o ritmo; em Ajustes >
  Histórico, as viagens.
- A cópia no Google Drive se apaga pelo app (Ajustes > Conta) ou pela sua conta
  Google.

## Mudanças nesta política

Quando o app mudar o que faz com os dados, esta página é atualizada e a data no
topo muda.

## Contato

Dúvidas sobre esta política podem ser enviadas abrindo uma issue em
<https://github.com/Memphyz/MUSE-releases/issues>.
