**----------------------------------------------------------------------------------------------------------------------------------------**

&#x09;				**INSTRUÇÕES PARA USAR A PLANILHA**

**----------------------------------------------------------------------------------------------------------------------------------------**



**Versão do código : v0.1 (BETA)**



**------------------------------------------------------- OBSERVAÇÕES --------------------------------------------------------------------**



Toda vez que é citado **PINOS**, estou me referindo as células na planilha e todas as conexões são representadas via código e colocadas quando as funções específicas de cada componente são chamadas.



Mais abaixo, eu cito um exemplo, o código desse exemplo e como realizar as conexões está escrito no arquivo **"README - CODE"**, Leia-o para mais instruções do código.



Está previsto a chegada de novos componentes: **POTENCIÔMETRO, BOTÃO, BUZZER, LDR e PORTAS LÓGICAS NOT, AND e OR** para a **v0.2**



**------------------------------------------------------- REQUISITOS ---------------------------------------------------------------------**



Um computador que consegue rodar Excel (mesmo que pareça brincadeira, esse projeto não foi pensado para rodar em celulares e outros);



Excel;



O básico da linguagem VBA e Lógica de programação (esse é opcional);



Saber como editar as células do Excel;



**----------------------------------------------- DAS DISPOSIÇÕES DE COMPONENTES ---------------------------------------------------------**



**TODOS** os componentes **SEM EXCEÇÃO** deverão seguir essas instruções quando colocados na planilha: 



&#x09;Cada componente tem seu número específico de pinos listados no código e que deve ser declarado ao fazer os projetos e ao mexer no **VBA**;



&#x09;O desenho dos componentes é completamente customizável e na realidade, nem é preciso, desde que tenha os pinos necessários;



**------------------------------------------------- PINOS DE COMPONENTES -----------------------------------------------------------------**



**LED** : O led conta com 2 pinos, o **POSITIVO** e o **NEGATIVO** : use 1 célula para ser a parte que brilha;



**RESISTOR** : O resistor conta com 2 pinos : use 1 célula para ser a parte onde é colocada a resistência(Ohms);



**VISOR DE 7 SEGMENTOS COM O CHIP 4511** : Usa no total 4 pinos para o **CHIP 4511** e 10 pinos para o visor de 7 segmentos : use 7 células para a parte que liga no visor de 7 segmentos e mostra os números no **CHIP 4511**. É recomendado que envolva o visor com a parte preta (pode ser alterada no código);



**ARDUINO** : Conta com 10 pinos digitais, 5 pinos analógicos, 2 GND's e 1 5v (será alterado para que o **ARDUINO** tenha a mesma quantidade de pinos que o físico) | A comunicação do **TX** e **RX** ainda não foi implementada | consta no código e o **ARDUINO** **PRECISA** de 1 célula para agir como o monitor serial (mude isso no código | Célula atual : D5);



**CHIP 4511** : Conta com 4 pinos de entrada e 10 pinos de saída (minha representação do chip. As saídas são organizadas assim para melhora no código);



**VISOR DE 7 SEGMENTOS** : Conta com 7 pinos | **PRECISA** de resistor a menos que a corrente não passe dos 20 mA (um resistor de **150 Ohms** para cada pino é o suficiente).



**----------------------------------------------- SOBRE O FUNCIONAMENTO DOS COMPONENTES ---------------------------------------------------**



**LED** : O led acenderá a célula quando o **POSITIVO** atingir o número 20 ou menor, e o **NEGATIVO**, 0;



**RESISTOR** : A entrada será 5v como padrão (será mudado no futuro) e a saída será em mA (perfeito para leds). Ele calcula A = 3 / Ohms, sendo A os mA e Ohms o valor digitado na célula;



**CHIP 4511** : A entrada é representada pelos 4 pinos sendo tradados **DE BAIXO PARA CIMA** no código. Ele recebe por meio desses pinos, um número binário de 4 bits e o transforma em decimal. A saída é representada pelos 10 pinos que recebem energia de acordo com a decodificação do binário. O pino 0 recebe energia quando o resultado é 0 e assim por diante.



**VISOR DE 7 SEGMENTOS** : A entrada é representada pelos 7 pinos e no código, quando um deles recebe energia, o led correspondente acende;



**ARDUINO** : Todos os pinos digitais tem como saída 5v quando ligados | a funcionalidade dos pinos analógicos ainda não foi implementada



**-------------------------------------------- MONTANDO SEU PRIMEIRO CIRCÚITO (UM LED QUE ACENDE) ------------------------------------------**



Siga essas instruções:



&#x09;Escolha as células para o 5v e o GND (Terra) do **ARDUINO**, a entrada e saída do **RESISTOR** (não esqueça da célula para colocar a resistência) e o **POSITIVO** e **NEGATIVO** do **LED** (não esqueça da célula que vai mudar de cor);



&#x09;Mude o **RESISTOR** para **150**;



&#x09;Faça todas as conexões no código.

