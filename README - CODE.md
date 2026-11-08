**------------------------------------------------------------------------------------------------------------**

&#x09;				**INSTRUÇÕES PARA O CÓDIGO**

**------------------------------------------------------------------------------------------------------------**



**Versão do código : v0.1 (BETA)**



**--------------------------------------- OBSERVAÇÕES --------------------------------------------------------**



Na estrutura, o arquivo foi colocado como 2 módulos. O módulo 1 apresenta as funções referentes aos componentes e o **ARDUINO** e o módulo 2 apresenta o código específico do **ARDUINO**, como uma IDE.



Aqui, detalho o funcionamento do código e como as conexões funcionam. Para saber da parte "física", olhe o arquivo **"README - INSTRUCTIONS"**.



**-------------------------------------- PRÓXIMAS VERSÕES -----------------------------------------------------**



As funções do **LED** e do **RESISTOR** vão passar por mudanças, no quesito de adaptabilidade, que virão na **v0.2**



Está previsto a chegada de novos componentes **POTENCIÔMETRO, BOTÃO, BUZZER, LDR e PORTAS LÓGICAS NOT, AND e OR** para a **v0.2**



A função **Sub loop()** será implementada na **v0.3**



**-------------------------------------- ARQUITETURA ----------------------------------------------------------**



Ao começar o código no ARDUINO (módulo 2) é recomendado e já vem como base a função de entrada **Sub setup()** | a **Sub loop()** ainda não foi implementada.



Para rodar o código, clique no **BOTÃO DE PLAY VERDE** da interface do **VBA**.



Para chamar cada função use o **Call função(Parênteses se for necessário)**.



Os componentes usados **PRECISAM** de uma função específica para que eles possam ser atualizados | para o led acender, por exemplo



No **VBA**, as células são tradadas com o **Range(Célula)** e para as conexões, os componentes usam **Range(Célula).Value** para ver o valor da célula específica



A ordem do código está completamente ligada ao programador, se ele não colocar os itens na ordem correta, o código não vai funcionar da maneira esperada.



Ex: Para fazer o **ARDUINO** ligar um **LED**, primeiro, faça o **ARDUINO** ligar o pino digital correspondente e somente **DEPOIS**, coloque a função que atualiza o **LED**



**----------------------------------------- FUNÇÕES ESPECÍFICAS ----------------------------------------------**



&#x20;**- ARDUINO** :

&#x09;

&#x09;Para ligar os pinos digitais use **pinoDigital(Célula do pino, Estado do pino)**. Essa função se assemelha ao **pinMode()** do **ARUINO**. A célula deve ser passada como **String** e no valor, o **0** representa o **LOW**, e o **1** representa o **HIGH**.



&#x09;**Exemplo: Call pinoDigital("A1", 1)** | Nesse caso, A célula **A1** recebe o valor 5, que equivale à 5v.



&#x20;**- CHIP 4511** :

&#x09;

&#x09;Para usar o **CHIP 4511** use **chip4511(celula1, celula2, celula3, celula4)**. Essa função pega os valores das 4 células e monta um número binário de 4 bits (**bytes = Array(celula4, celula3, celula2, celula1)**). Depois, decodifica ele para decimal usando um **Array** de "cola" (**cola = Array(8, 4, 2, 1)**). A função roda essa lista e os valores que são iguais a 5 (**If** **Range(bytes(i)).Value = 5 Then**) ele pega o índice **i** correspondente e adiciona a uma variável **num** (**num = num + cola(i)**). O conjunto completo da decodificação é esse:



&#x09;**For i = 0 To 3**

&#x20;       	**If Range(bytes(i)).Value = 5 Then**

&#x20;           		**num = num + cola(i)**

&#x20;       	**End If**

&#x20;       **Next i**



&#x09;Depois disso, ele pega as 10 saídas que estão declaradas no código na variável **saidas**. (Esta parte está no código pois se estivesse na função, teria muitos argumentos para colocar, mas isso será corrigido em versões futuras) Depois coloca o valor **1**  na célula correspondente ao número decodificado e deixa as outras células com o valor **0**.

&#x09;

&#x09;**For i = 0 To 9**

&#x20;       	**Range(saidas(i)).Value = 0**

&#x20;   	**Next i**



&#x09;**Range(saidas(num)).Value = 1**



&#x09;**Exemplo** : **Call chip("O16", "O14", "O12", "O10")** | Nas células citadas, o valor recebido é **1010** que equivale a **5** em decimal, então a 5° célula de **saidas** ficará com o valor **1**, e o resto com **0**



&#x20;**- RESISTOR** :



&#x09;Para usar o **RESISTOR**, use **Resistor(Ohms, entrada, saída)**. Esses argumentos não foram colocados no código de exemplo, mas estão presentes no módulo\*\*.\*\* Nesses argumentos, coloque a posição da célula em que se localiza o **RESISTOR**. Essa função espera que a entrada padrão seja **5v** (será modificado para receber outras tensões em atualizações futuras) e calcula **A = 3 / Ohms**, sendo **A** os **mA** e os retorna na célula de saída.



&#x09;**ohms = Range("F8").Value**

&#x20;   	**imput = Range("G20").Value**



&#x09;**A = 3 / ohms**

&#x20;       **A = A \* 1000**



&#x09;**If imput = 0 Then**

&#x20;       	**A = 0**

&#x20;   	**End If**



&#x09;**Range("E8").Value = imput**

&#x20;   	**Range("G8").Value = A**



&#x09;**Exemplo** : **Call Resistor** | Nesse exemplo, digamos que a célula dos **Ohms** tenha o valor **150**, o valor que aparecerá na célula de saída será **20**.



&#x20;**- LED** :



&#x09;Para usar o **LED**, use **Led(positivo, negativo, brilho)**. Nos argumentos, coloque as células correspondentes. O **LED** faz uma verificação simples, ele verifica se o **Positivo** é **<= 20** (**If positive <= 20 Then**) e se **o NEGATIVO** **é = 0** ajusta a coloração da célula do **brilho** de acordo com o número (**Range("F14").Interior.Color = RGB(cor, 0, 0)**). Se o **LED** está desligado ou queimado, ele troca para a cor padrão **RGB(128, 128, 128)**.



&#x09;**Range("E14").Value = Range("G8").Value   'Essa parte é estética**

&#x20;   	**Range("G14").Value = Range("B12").Value  'Essa também**

&#x20;

&#x20;   	**positive = Range("E14").Value**

&#x20;   	**negative = Range("G14").Value**

&#x20;

&#x20;   	**If positive <= 20 And negative = 0 And positive >= 10 Then**

&#x20;   	    **cor = positive \* 12.5**

&#x20;   	    **Range("F14").Interior.Color = RGB(cor, 0, 0)**

&#x20;   	**Else**

&#x20;   	    **Range("F14").Interior.Color = RGB(128, 128, 128)**

&#x20;   	**End If**



&#x09;**Exemplo** : **Call led** | Se no caso, a célula do **POSITIVO** for 20 e o **NEGATIVO** for 0, ele acende (**Range("F14").Interior.Color = RGB(cor, 0, 0)**).

