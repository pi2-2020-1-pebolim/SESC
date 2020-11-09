# SESC
Sistema Eletrônico de Simulação e Controle

O comportamento geral do SESC (Sistema Eletrônico de Simulação e Controle), nele inclui a integração com a IA, motores e o sistema de validação. O software foi escrito em Python e é composto por 4 arquivos, que será executado pela Raspberry, onde se comunicará com a IA e o Arduino. Como explicado anteriormente, a Raspberry irá controlar o Arduino com a biblioteca do pyfirmata. 

O arquivo SESCevent.py é a a parte do sistema que é integrada a IA, ela é responsável por receber e enviar os eventos via PUDM e tirar a foto da mesa. Ela é iniciado por meio do evento ActionEvent, onde contém a posição futura de determinado jogador e se é para chutar ou não. Esse evento é enviado para o arquivo SESCcontrol.py que retornará os estados atuais de cada jogador e enviará o evento StatusUpdateEvent.

No arquivo SESCcontrol.py, ele recebe o ActionEvent e primeiro é verificado se a mesa já foi inicializada, caso não, o programa habilita as entradas e saídas do Arduino, seta as configurações iniciais da mesa, coletadas previamente, e envia RegisterEvent para a IA. Para iniciar a simulação, dados aleatórios sobre a posição de cada jogador é gerado e depois sincronizado com a mesa física a partir do mapeamento. Depois de inicializar a mesa, é preciso mostrar o campo do jogo com os dados iniciados. 

Ainda na inicialização, o mapeamento eletrônico da mesa é feito, e para isso, é necessário fazer com que todos os jogadores estejam em pé e indo para os pontos máximos da mesa, até que os sensores de fim de curso sejam ativados, isso será realizado para cada haste, ainda nessa parte, a simulação é sincronizada com a mesa física.

Agora, o programa coloca todos os jogadores nos pontos mínimos contando a quantidade de passos que foram dados. 

Os jogadores são centralizados usando a quantidade de passos que deram e por fim é feito o primeiro evento que a IA enviou. A locomoção dos motores físicos e simulados é realizado no mesmo momento.

O arquivo SESCdraw.py é o programa responsável por virtualizar o campo e os jogadores e ele é chamado toda vez que acontece um movimento nos motores. 
