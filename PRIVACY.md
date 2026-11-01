# Política de privacidade do MUSE

Última atualização: 31 de outubro de 2026

O MUSE é um aplicativo de navegação para motociclistas que conversa com um
painel instalado na moto. É um projeto pessoal, sem fins comerciais. Esta página
explica que dados o app usa, onde eles ficam e com quem eles são trocados.

## Resumo

- O MUSE **não guarda o que você faz no app**. O único servidor dele existe só
  para a **viagem ao vivo** e o **rolê em grupo**, e só recebe algo quando você
  compartilha uma viagem ou entra num rolê (veja abaixo). Ele guarda apenas a
  última posição e apaga tudo quando a viagem ou o rolê acaba.
- Não há anúncios, rastreamento nem venda de dados. A única medição de uso é
  a do leitor de texto do Google (ML Kit), sobre a própria ferramenta, quando
  você importa a CNH (veja "Documentos do veículo e CNH").
- Seus dados ficam no seu celular e, se você quiser, numa pasta escondida do
  **seu próprio** Google Drive.

## O que fica guardado no celular

- Locais salvos (como Casa e Trabalho), rotas salvas e as últimas buscas.
- O histórico das últimas viagens, com o trajeto percorrido.
- Números de uso acumulados (quilômetros, tempo, recordes) e o seu ritmo de
  pilotagem, usado para estimar a hora de chegada.
- Ajustes do app e, se você informar, a sua chave de acesso ao TomTom.
- Seus veículos (apelido, placa, estado, moto ou carro e, se você informar ou
  importar, o Renavam) e os dias de pedágio sem cancela já pagos.
- O licenciamento e o IPVA que você marcou como pagos e, se você informar ou
  importar, a validade e a categoria da sua CNH.
- Mapas e alertas baixados para usar sem internet, e os catálogos dos
  monumentos da Rota Biker e da Faixa Azul.
- O seu passaporte da Rota Biker, se você o preencher: a identificação (cidade,
  estado, país, piloto, garupa e telefone), os monumentos que você marcou como
  carimbados e, se escolher uma, a foto.
- O pareamento com o painel da moto.
- O link da viagem ao vivo que estiver em uso e, se você ligar, o seu link
  fixo (veja abaixo).
- O rolê em grupo em que você estiver (o código e a chave de membro) e o último
  apelido que você usou nele.

Esses dados ficam no armazenamento do próprio app. O Android pode copiá-los para
um celular novo na transferência entre aparelhos; o pareamento com o painel, os
links da viagem ao vivo e o rolê em grupo nunca são copiados.

## Localização

O app usa a localização do celular para mostrar a sua posição, calcular rotas,
avisar de radares e lombadas e gravar o histórico de viagens. A localização é
usada no próprio celular e só sai dele nas consultas aos serviços descritos
abaixo e, se você compartilhar uma viagem ou entrar num rolê em grupo, para o
servidor do MUSE.

## Microfone

O app só usa o microfone nos comandos de voz, se você os ligar, e só por
alguns segundos depois de cada chamado (veja "Comandos de voz").

## Serviços externos que o app consulta

Para funcionar, o app faz consultas a serviços de mapa, rota e clima. Em cada
consulta vai apenas o necessário para a resposta (por exemplo, a sua posição e
o destino para calcular uma rota, ou o texto que você digitou numa busca).
Nenhuma delas leva seu nome, e-mail ou identificação da conta.

| Serviço | Para quê |
|---|---|
| OpenFreeMap | As imagens do mapa (a área que aparece na tela) |
| OpenStreetMap (Nominatim e Overpass) | Busca de endereços, limites de velocidade, radares e dados das vias; nos comandos de voz, os lugares à frente na rota (posto, borracharia, oficina) e o bairro e o lugar conhecido de onde você está |
| Reconhecimento de voz do Android | Nos comandos de voz, entender o pedido falado. Usa o reconhecimento do próprio celular, sem internet, quando ele tem o idioma; senão, o do sistema, que pode usar a internet (no Brasil, quase sempre o do Google) |
| OSRM (e o servidor do FOSSGIS, a pé) | Cálculo de rotas |
| TomTom | Trânsito no mapa e rotas com trânsito, para todos, com a chave do MUSE (vão a área do mapa, a partida e o destino); busca de endereços só com a sua própria chave |
| Open-Meteo | Previsão do tempo ao longo da rota |
| INMET | Avisos meteorológicos oficiais na região da rota |
| Mapillary | Foto da rua ao escolher um destino no mapa (vai a posição do ponto escolhido) |
| ViaCEP | Busca de endereço pelo CEP |
| GitHub | Download dos mapas offline, dos catálogos (Rota Biker, Faixa Azul) e das atualizações do app e do painel |
| Google (ML Kit) | Só ao importar a CNH: métricas de uso e desempenho do leitor de texto (aparelho, versão do app, tempo de leitura). **A imagem e o texto lido não são enviados** |
| Sites do Detran, da Secretaria da Fazenda e do Pedágio Digital | Abertos no navegador quando você toca nos atalhos de Débitos e documentos; o app não envia nada a eles (a placa vai no endereço do Pedágio Digital, e o Renavam fica copiado para você colar) |

Cada serviço tem a própria política de privacidade.

## Viagem ao vivo (opcional)

Durante a navegação, você pode compartilhar a viagem: o app cria um link que
mostra a moto no mapa a quem você mandar. **Nada disso acontece se você não
compartilhar.**

O servidor é um Cloudflare Worker do MUSE. Enquanto a viagem está compartilhada,
o app manda a ele:

- a posição da moto, o rumo e a velocidade;
- o trecho da rota logo à frente (até cerca de 800 m) e o trânsito nele, que
  **para 300 m antes do destino**: o destino não é enviado;
- o que falta até o destino, a hora prevista de chegada e o congestionamento
  mais próximo;
- se a moto está andando, parada num semáforo ou no trânsito;
- a bateria do celular;
- o recado que você escolher ou escrever, se houver.

O servidor **guarda só o último envio**, nunca o trajeto, e não sabe quem é
você. **Só manda a posição com alguém olhando**: se ninguém estiver com o
link aberto, o app não envia posição nenhuma. Quem tem o link vê a moto andar
no mapa (o caminho já percorrido fica só no navegador de quem acompanha) e pode
abrir a posição no MUSE para ir até lá. O link não aparece em buscadores.

O link de uma viagem para de funcionar quando você toca em Parar, 30 minutos
depois da chegada, ou depois de 8 horas sem posição (celular desligado, estrada
sem sinal). Nesses casos, tudo o que estava no servidor é apagado.

**Link fixo (opcional):** se você ligar "Mesmo link em toda viagem", o mesmo
link mostra todas as suas navegações, sem você precisar compartilhar de novo.
Entre uma viagem e outra o servidor não guarda nenhuma posição, e o link mostra
"sem viagem agora". Os **primeiros 300 m de cada saída não são enviados**, para
não mostrar onde você mora. Você pode trocar ou desligar o link a qualquer
momento, e o antigo para de funcionar para todo mundo. Um link fixo sem
nenhuma viagem por 90 dias é apagado sozinho.

## Rolê em grupo (opcional)

Você pode criar um rolê e chamar outros pilotos do MUSE por um código ou link,
ou entrar no rolê de alguém. Quem cria é o líder e escolhe o destino e as
paradas; cada membro aparece para os outros como uma bolinha colorida no mapa
do app e no painel da moto. **Nada disso acontece se você não criar nem entrar
num rolê.**

Enquanto você está no rolê, o app manda ao mesmo servidor do MUSE, que repassa
aos outros membros daquele rolê:

- o apelido que você escolher (até 12 letras) e a sua cor;
- a posição da moto, o rumo, a velocidade e se ela está andando ou parada;
- o trecho da rota logo à frente (até cerca de 3 km);
- se você for o líder, o destino e as paradas do rolê (nome e coordenada);
- os recados que você mandar pelos comandos de voz, que o servidor repassa na
  hora aos membros conectados e **não guarda**.

O app só manda a posição quando **outro membro está conectado**, e só quando
ela muda de um jeito que os outros não conseguiriam prever (por exemplo, ao
mudar de velocidade ou sair do caminho). A pé, nada é enviado.

O servidor **não grava a posição**: ela fica só na memória dele, enquanto o
rolê está em uso, e nunca forma um trajeto. Ficam guardados apenas o apelido, a
cor e o destino com as paradas, e tudo é apagado quando o líder encerra o rolê,
quando o último membro sai, depois de 8 horas sem nenhuma posição ou depois de
24 horas. Quem sai do rolê deixa de receber e de mandar na hora. O código do
rolê é o que dá acesso a ele: quem tiver o código pode entrar, até o limite de
8 membros, e a página do convite não mostra posição nenhuma.

## Comandos de voz (opcional)

Durante a navegação, você pode chamar o MUSE pelo gesto de assistente do seu
intercomunicador e fazer um pedido falado, como "quanto falta" ou "posto mais
próximo". Para isso, o app pede a permissão do microfone e precisa ser
escolhido como app de assistente do celular. **Nada disso acontece se você não
ligar os comandos de voz** (Ajustes > Som), e eles vêm desligados.

- O microfone **só abre por alguns segundos depois do seu chamado**, para ouvir
  o pedido; ele não fica escutando o tempo todo.
- O que você fala vai ao reconhecimento de voz do Android (veja a tabela
  acima), que devolve o texto ao app. O MUSE **não grava nem guarda o áudio**
  nem o texto do pedido.
- O que o pedido precisar sai pelos mesmos caminhos de sempre: a busca de um
  endereço ou de um lugar à frente vai aos serviços de mapa; um recado vai à
  viagem ao vivo e ao rolê em grupo, se estiverem ligados.
- Fora da navegação, o chamado é passado ao outro assistente do celular, que
  segue a política dele.

## Documentos do veículo e CNH (opcional)

Em Ajustes > Débitos e documentos, o app mostra quando vencem o licenciamento e
o IPVA de cada veículo e a validade da CNH. As datas vêm do calendário oficial
de cada estado, que já vai dentro do app: **o app não consulta débitos** em
nenhum órgão e não sabe o que você pagou; quem marca como pago é você.

Você pode importar o **CRLV digital** e a **CNH digital** em PDF, da Carteira
Digital de Trânsito, escolhendo o arquivo ou compartilhando-o de lá para o
MUSE.

- A leitura é feita **no celular**, e **o arquivo não é guardado** nem enviado
  ao servidor do MUSE.
- Do CRLV ficam só a placa, o Renavam, o estado, o tipo do veículo, o modelo
  (como apelido) e o ano do licenciamento. Nome, CPF, chassi e o resto do
  documento são descartados.
- Da CNH ficam só a validade e a categoria. Nome, CPF, filiação e foto são
  descartados.
- A CNH digital traz o cartão como imagem, e quem lê o texto dela é o ML Kit,
  do Google, que roda no próprio celular. Ele **não envia a imagem nem o texto
  lido**, mas envia ao Google métricas de uso e desempenho da ferramenta (como o
  modelo do aparelho, a versão do app e o tempo da leitura), segundo os
  [termos do ML Kit](https://developers.google.com/ml-kit/terms).

## Sincronização com a conta Google (opcional)

Se você conectar uma conta Google em Ajustes > Conta, o app guarda uma cópia dos
seus dados numa **pasta escondida do seu Google Drive** (a pasta de dados do
aplicativo), para você recuperá-los em outro celular. Vão para lá os locais e
rotas salvas, as últimas buscas, o histórico de viagens, os números de uso, o
ritmo de pilotagem, os ajustes, incluindo a chave do TomTom, se houver, os seus
veículos com a placa, o estado e o Renavam, os dias de pedágio pagos, o
licenciamento e o IPVA marcados como pagos, a validade e a categoria da CNH e o
passaporte da Rota Biker (a identificação, os carimbos e a foto, para ela
aparecer nos seus outros celulares).

Os links da viagem ao vivo e o rolê em grupo não vão para a conta Google.

O catálogo dos monumentos da Rota Biker é montado uma vez por dia, fora do
app, a partir da página pública do movimento (monumentobikers.com.br) e do mapa
público dela, e publicado no GitHub como os mapas offline. O app só baixa esse
arquivo; ele nunca consulta o site do movimento nem o Google, e nada do que
você faz no passaporte sai do seu celular ou da sua conta Google.

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
  Histórico, as viagens; em Ajustes > Veículos, um veículo com tudo o que é
  dele; em Ajustes > Débitos e documentos, a validade e a categoria da CNH.
- A cópia no Google Drive se apaga pelo app (Ajustes > Conta) ou pela sua conta
  Google.
- A viagem ao vivo se apaga sozinha no fim da viagem; tocar em Parar apaga na
  hora. O link fixo se apaga ao desligá-lo ou trocá-lo.
- No rolê em grupo, sair tira você do rolê na hora; o rolê inteiro se apaga
  quando o líder o encerra ou o último membro sai.

## Mudanças nesta política

Quando o app mudar o que faz com os dados, esta página é atualizada e a data no
topo muda. Na próxima vez que você abrir o app, ele avisa que a política mudou
e pede que você a aceite para continuar.

## Contato

Dúvidas sobre esta política podem ser enviadas abrindo uma issue em
<https://github.com/Memphyz/MUSE-releases/issues>.
