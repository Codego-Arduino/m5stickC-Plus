Codigo alterado para Portugues(BR)

#M5Stick-NEMO
Firmware para pegadinhas de alta tecnologia em dispositivos M5Stack ESP32

![Logotipo da matriz M5-Nemo](https://github.com/n0xa/m5stick-nemo/blob/main/NEMOMatrix.png)
Logotipo de @unagironin

## Nome e histórico
NEMO iniciou um projeto pessoal para me ajudar a aprender mais sobre o desenvolvimento do ESP32 com o Arduino IDE. Decidi replicar algumas pegadinhas comuns e populares que estavam recebendo muita atenção da comunidade de tecnologia, como um desafio para mim mesmo, e também para entender melhor esses ataques.
NEMO recebeu o nome do peixe pequeno, inteligente e teimoso de Procurando Nemo. Este projeto contrasta com outro dispositivo de alta tecnologia associado a certas criaturas marinhas. Eu queria provar que há muitas coisas que você pode fazer com um pequeno kit de desenvolvimento e um pouco de curiosidade. Não tenho ilusões de substituir as capacidades de qualquer dispositivo semelhante neste projeto. É apenas para diversão e para minha própria educação.

![M5-Nemo na família M5StickC e M5Cardputer](https://github.com/n0xa/m5stick-nemo/blob/main/M5-Nemo.jpg)

## Características
* Porta [TV B-Gone](http://www.righto.com/2010/11/improved-arduino-tv-b-gone.html) (graças ao [HAKRWATCH](https://github.com) do MrArm /MrARM/hakrwatch)) para desligar muitas TVs, projetores e outros dispositivos controlados por infravermelho
* [AppleJuice](https://github.com/ECTO-1A/AppleJuice) Spam de emparelhamento de dispositivo Bluetooth iOS
* Spam de notificação de dispositivo Bluetooth para SwiftPair (Windows) e Android
* WiFi Spam - SSIDs engraçados, WiFi Rickrolling e um modo aleatório que cria centenas de SSIDs nomeados aleatoriamente por minuto
* Portal NEMO WiFi - Um portal cativo que tenta criar credenciais de e-mail de engenharia social - salva nomes de usuário e senhas no cartão SD (se inserido em um leitor compatível)
* WiFi SSID Scanner - Exiba SSIDs de 2,4 GHz próximos, obtenha informações sobre eles e até mesmo clone os SSIDs no Portal NEMO
* Relógio digital de 24 horas ajustável pelo usuário, apoiado pelo M5 Stick RTC, para manter o tempo relativamente estável, mesmo em modo de suspensão profunda e bateria fraca
* Configurações apoiadas por EEPROM para rotação, brilho, escurecimento automático e SSID do Portal NEMO
* Nível da bateria e créditos no menu de configurações

## Interface de usuário
Existem três controles principais:
* Home - Interrompe o processo atual e retorna ao menu de praticamente qualquer lugar no NEMO
* Próximo – Move o cursor para a próxima opção do menu. Nos modos de função, isso geralmente interrompe o processo e retorna ao menu anterior.
* Selecionar - Ativa a opção de menu atualmente selecionada e ativa a tela esmaecida nos modos de função

* StickC e StickC-Plus
   * Energia: pressione longamente o botão liga/desliga por 6 segundos para desligar a unidade
   * Home: Toque no botão liga / desliga (mais próximo da porta USB)
   * Próximo: Toque no botão lateral
   * Selecione: Toque no botão M5 na frente da unidade

* Computador de cartão
   * Home: Toque na tecla Esc/~/` ou na tecla Seta para Esquerda/,
   * Próximo/Anterior: Toque na seta para baixo/. tecla e seta para cima/; teclas para navegar
   * Selecione: Toque na tecla OK/Enter ou Seta para a direita/? chave

## Portal NEMO
No modo NEMO Portal, o NEMO ativa um Hotspot WiFi aberto chamado "Nemo Free WiFi" (configurável em portal.h) com servidores DNS, DHCP e Web ativados.
* O Portal NEMO exibe uma página de login falsa que afirma fornecer acesso à Internet se você fizer login.
* Este é um ataque de engenharia social e registrará o nome de usuário e as senhas inseridas na página.
* Nos detalhes do Wifi Scan, você pode clonar um SSID existente na lista de varredura. Sair do Portal NEMO limpará o SSID Evil Twin
* Você pode visualizar as credenciais capturadas conectando-se ao portal a partir do seu próprio dispositivo e navegando até http://172.0.0.1/creds
* Você pode definir um SSID personalizado conectando-se ao portal a partir do seu próprio dispositivo e navegando até http://172.0.0.1/ssid
* Se o seu dispositivo suportar EEPROM para configurações, o SSID personalizado inserido será salvo como padrão, mesmo se estiver desligado.
* Se o seu dispositivo tiver um leitor de cartão SD com um cartão formatado em sistema de arquivos FAT inserido, os nomes de usuário e senhas serão registrados em nemo-portal-creds.txt no cartão SD para você ler mais tarde.
* O suporte a cartão SD só está habilitado por padrão na plataforma M5Stack Cardputer. Ele pode ser habilitado em dispositivos M5Stick, mas um leitor de cartão SD deve ser construído e conectado ao pino do painel frontal.
* O Portal NEMO deve ser usado apenas em compromissos profissionais com um escopo de trabalho válido, para fins educacionais ou de demonstração. O armazenamento, venda ou uso de informações pessoais sem consentimento é contra a lei. 🤓

## Instalar a partir do M5Burner
Esta é a maneira mais fácil de obter NEMO
* [Início rápido do M5Stick C Plus](https://docs.m5stack.com/en/quick_start/m5stickc_plus/uiflow) possui links para o aplicativo M5Burner para Linux, MacOS e Windows. Esta é a ferramenta oficial para instalar UIFlow e outros firmware oficiais. Eu forneço binários atualizados para NEMO lá.
* Inicie o M5Burner
* Selecione "StickC" no menu à esquerda (ou StampS3 para Cardputer)
* Use a busca na parte superior do aplicativo para procurar por “NEMO”. Minhas builds oficiais serão enviadas por "4x0nn" e terão fotos.
* Clique em Baixar
* Clique em Gravar

## Instale arquivos .bin manualmente com esptool.py
* Instale as ferramentas ESP-IDF de acordo com o [Guia de primeiros passos do Espressif](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/)
* Abra a ferramenta esp-idf CMD (no Windows) - no Mac ou Linux, esp-idf.py e esptool.py devem estar no caminho do sistema.
* esptool.py --port COMPORT -b 115200 write_flash -z 0x0 M5Nemo-VERSION.bin
   * porta pode ser uma porta COM, por ex. COM4, COM11 no Windows. No Mac e Linux geralmente estará em /dev como /dev/ttyUSB0, /dev/ttyACM0 ou /dev/cu.usbserial-3
   * M5Nemo-VERSION.bin deve ser uma versão que você baixou de uma versão do GitHub – de preferência a mais recente disponível.

## Construindo a partir da fonte
Se quiser personalizar o NEMO ou contribuir com o projeto, você deve estar familiarizado com a construção do NEMO a partir do código-fonte.
* Instale o Arduino IDE. Usei o Arduino 1.8 no Linux e Windows e o Arduino 2.2 no Windows com sucesso.
* Instale as placas M5Stack para Arduino IDE: Em Arquivo -> Preferências, cole esta URL na caixa de texto "URLs do Gerenciador de Placas". Use vírgulas entre URLs se já houver URLs presentes. https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/arduino/package_m5stack_index.json
* Se M5Stack -> M5Stick-C-Plus não aparecer em Ferramentas -> Placas, use Ferramentas -> Placas -> Gerenciador de placas e procure por M5Stack. Isso instalará o suporte para a maioria das placas M5Stack, incluindo o Stick C Plus.
* Certifique-se de que o modelo correto do dispositivo (por exemplo, M5Stick-C, M5Stick-C-Plus ou M5Cardputer) esteja selecionado no menu de placas.
* Instale as bibliotecas necessárias. Em Sketch -> Incluir Biblioteca -> Gerenciador de Biblioteca, procure e instale as seguintes bibliotecas e quaisquer dependências necessárias:
   * M5StickCPlus, M5StickC ou M5Cardputer
   *IRRemotoESP8266
* Remova o comentário da linha `#define` apropriada perto do topo da sua plataforma (STICK_C, STICK_C_PLUS ou CARDPUTER)
* Alternar esquemas de partição. `Ferramentas` -> `Esquema de partição` -> `Sem OTA (APP grande)` - às vezes esta opção é rotulada como `APP enorme`
* Configuração
   * O código deve ser compilado de forma limpa e funcionar em um M5Stick C Plus pronto para uso a partir do branch master ou de uma tag de lançamento.
   * Remova o comentário apenas da opção `#define` apropriada ou ocorrerão erros do compilador.
   * Se por algum motivo a tela saltar de muito escura no nível 0 para quase totalmente brilhante no nível 1 e outros níveis de brilho não afetarem nada, defina a variável pct_brightness como falsa.
* Compile e carregue o projeto

## Solução de problemas
* Vários recursos enviam informações de depuração para o monitor serial. Use o recurso Serial Monitor no Arduino IDE ou M5Burner para coletar essas informações. Pode conter dicas úteis. Ao preencher um relatório de bug, geralmente ajuda incluir a saída do monitor serial.
*Reinicialize a EEPROM. Em modelos com suporte para configurações EEPROM, use "Limpar configurações" no menu de configurações ou segure o botão "Avançar" (tecla lateral nos modelos StickC, Tab ou seta para baixo no Cardputer) enquanto liga.
* O LED IR do TV-B-Gone pode ser observado através da câmera de um smartphone, emitindo um feixe de luz roxo claro. Se parecer estar ligado constantemente ou se nunca piscar durante as operações do TV-B-Gone, algo está errado. Reportar um erro. Há um problema conhecido com o TVBG que não funciona após usar spam de Bluetooth ou spam de Wi-Fi aleatório.
* Tente visualizar listas de Wi-Fi de vários dispositivos diferentes se você suspeitar que o spam de Wi-Fi não está funcionando. Às vezes, o gerenciador de rede Linux pode ver redes que os smartphones não conseguem. Inclua os resultados deste teste se estiver relatando problemas de spam de Wi-Fi.
* A Apple corrigiu muitas coisas do Bluetooth desde o verão de 2023. Se estiver testando o AppleJuice, experimente alguns dos tipos de dispositivos AppleTV, pois eles tendem a ser mais confiáveis ​​porque a Apple não filtra os sinais de Bluetooth mais fracos para essa plataforma.
## Relatando Bugs
Por favor, reporte bugs através do GitHub Issues. Eles são mais fáceis de rastrear do que comentários em postagens de mídia social, entradas do M5Burner, etc. Se algo não estiver funcionando, inclua:
* Versão do firmware
* Como você instalou (M5Burner, compilado você mesmo, esptool.py)
* Ferragens
* Especificamente quais recursos e opções não estão funcionando
* Como você determinou que não está funcionando e quais testes você fez. Inclua modelos de dispositivos e sistemas operacionais com os quais você testou e quaisquer erros ou resultados relevantes do Serial Monitor, se aplicável.
* Se você descobrir como consertar um bug identificado, PRs serão bem-vindos!

## Contribuindo
Contribuições são bem-vindas.
* Por favor, consulte os problemas do GitHub para o projeto. Há sugestões de recursos e bugs relatados lá, e eu apreciaria os PRs que abordassem isso.
* Ao enviar uma solicitação pull, direcione o branch de desenvolvimento. A maneira mais fácil de fazer isso é bifurcar TODAS as ramificações ou simplesmente criar uma ramificação "desenvolver" em sua própria bifurcação e, em seguida, usar o GitHub para sincronizar sua ramificação de desenvolvimento.
* Observe como determinados hardwares (como LED e RTC) são definidos e bloqueados no código e tente seguir esses padrões. Além disso, use as definições para FGCOLOR, BGCOLOR, TEXT_SIZE* e o alias DISP ao enviar coisas para o display integrado.

Coisas nas quais gostaria de ajuda:
* Melhor localização/traduções do menu, não apenas do HTML do Portal NEMO.
   * Provavelmente precisa de um novo arquivo .h
   * Seja configurável nas configurações e use um byte eeprom para salvar a configuração
   * Faça uso gratuito de `const` na implementação para que as strings de localização sejam armazenadas apenas e referenciadas diretamente no armazenamento flash, em vez de usar muita SRAM.
* Infravermelho
   * Uma nova "região" de TV-B-Gone repleta de códigos IR adicionais que podem ligar e desligar faixas de LED RGB, condicionadores de ar, ventiladores, barras de som e similares
   * Uma maneira de converter ou usar códigos IR zero do flipper a partir da base de código do NEMO
* Descubra uma maneira de ler e exibir o nível da bateria nos modelos Cardputer e StickC-Plus2 que não possuem uma PMU AXP192. O [código da bateria na demonstração de fábrica do Cardputer](https://github.com/m5stack/M5Cardputer-UserDemo/tree/main/main/hal/bat) pode ser um bom lugar para começar.
* ALVO Desautenticação somente em um ponto de acesso específico. PRs de spam Deauth serão rejeitados.

Coisas que provavelmente não irei mesclar:
* Spam de desautenticação de wifi em massa
* Spam Bluetooth que potencialmente perturba rastreadores de saúde e condicionamento físico, relógios inteligentes, etc.
