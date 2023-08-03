<h2 p align="center" > Localizar um texto em um diretório que não sabemos onde esta. </h2></p>

## Passo 1 - Localizando um comando com apropos.
<br><p> - O comando apropos serve para localizar um comando que você não lembra a sintaxe por meio de palavras-chave que descrevam a funcionalidade que este comando teria. <br> </p>

<p> - Estamos procurando um comando que encontre uma pasta especifica.

![Passo 1](img/Passo_1.png) 

<p> <i> - Dependendo do sistema precisa-se atualizar o cache para o comando apropos funcionar corretamente, o comando é <b>"mandb"</b></i>. <p>

<p> - Procuramos o comando find que localiza arquivos em uma hierarquia de diretórios. <br>
- Mas antes o que significa este <b>(1)</b> a frente do comando find?
</p>

![Passo 3](img/Passo_3.png) 

<p> - Utilizando o comando <b>man man</b> (que seria o manual do próprio manual do linux), encontramos a descrição do tipo de função que determinada palavra teria caso tivesse determinado numero envolto do <b>()</b>.
<p> - Desta forma procuramos comandos executáveis, que correspondem ao número 1, que nosso comando <b>find</b> possui.
<p> - Por exemplo, poderíamos possuir os mesmos comandos derivativos do <b>find</b>, como <i>find-lib(5) find-ker(9)</i>, mas apenas precisamos obter comandos executáveis, para isso utilizaríamos a seguinte flag abaixo junto ao comando <b>apropos</b>.
<br>
<p><b><i> - Os comandos find-lib e find-ker não existem, apenas os mencionei a título ilustrativo.</b></i></p>

![Passo 2](img/Passo_2.png) 
<p> - Utilizaremos a flag -s acompanhada do número da sessão que buscamos, nesse caso a sessão (1) destinada para comandos executáveis.</p>
<p> - O comando ficaria: <b>apropos -s 1 search</b>

![Passo 4](img/Passo_4.png) 
<p> - Note que a filtragem ficou relativamente menor, pois agora o <b>apropos</b> só nos passa a sessão que escolhemos. </p>

## Passo 2 - Utilizando o comando <b>find</b> <br>

<p> - Agora que sabemos qual comando utilizar para encontrar um arquivo ou diretório, vamos entender separadamente como construir um comando <b>find</b>.

<p> - Para este exemplo estamos procurando uma pasta chamada <b>arquivos</b>.

<p> - Não fazemos ideia de onde se localiza a pasta em questão, apenas sabemos seu nome e que ela é um diretório. Para localizá-la podemos utilizar o seguinte raciocínio: </p>
<p> - Para se encontrar uma caneta perdida em um quarto, primeiro precisamos entrar neste quarto. O comando <b>find</b> segue esta mesma analogia. </p>
<p> - Em sua sintaxe começamos com o comando <b>find</b> (diretório de pesquisa), no nosso exemplo, pegaremos desde o diretório / + a flag <b>-name</b> que será onde colocaremos o nome do diretório que estamos buscando, que por sua vez é o diretório <b>arquivos.</b></p>
<p> - Nosso comando então seria: <b>find / -name "arquivos"</b></p>

![Passo 5](img/Passo_5.png) 

<p> - Aqui falaremos de dois pontos distintos, o primeiro é o caractere <b>"?"</b> e o segundo é a saída do nosso comando. </p>

<p> - O caractere </b>?</b>, podemos chamar de caractere coringa, ele tem a função de encontrar ou não qualquer caractere <b>somente</b> naquela posição. Por exemplo, caso tivéssemos a dúvida se a pasta se chama <b>"arquivos"</b> ou <b>"arquivo"</b> no singular, poderíamos utilizar o caractere coringa que nos daria qualquer carácter ou nenhum após a palavra <b>arquivo</b>. </p>

<p> - O segundo ponto é a saída do comando, notamos que temos dois resultados, mas por que isso? Porque deveríamos especificar o tipo de arquivo que queremos encontrar, caso contrário podemos tanto ter a saída de arquivos regulares, especiais ou diretórios. </p>

<p> - Para resolver isso é simples, basta passar a flag <b>-type</b> seguido do <b>parâmetro d</b> de "directory". </p>

<p> - Encontramos finalmente o nosso diretório, mas e se agora precisa-se ainda achar um trecho de texto de código dentro deste diretório que pudesse, por exemplo, ser um erro? </p>

## Passo 3 - Utilizando o comando <b>grep</b> <br>

<p> - O comando grep é a chave para esta busca, ele sozinho poderia resolver a nossa tarefa tanto através do caminho absoluto quanto do relativo. </p>

<p> <i> - Caminho absoluto é aquele que é declarado desde a raiz do sistema identificado pelo / até o local a onde deseja-se ir. </i> </p>
<p> <i> - Já o caminho relativo é aquele que parte do diretório que nos encontramos atualmente. </i> </p>

<p> - Neste exemplo criamos várias pastas e arquivos, e cada arquivo com seus textos dentro do diretório "/tmp/arquivos". Para localizar o arquivo em questão, escrevi em um desses documentos a palavra "<b>achou</b>". </p>

<p> - Podemos resolver este problema da seguinte forma: utilizando o comando <b>grep</b> + a flag -r (recursivo) + a palavra em questão "achou" + o caminho do diretório, absoluto ou relativo. </p>

<p> - Desta forma o nosso comando seria: <b>grep -r "achou" /tmp/arquivos/</b></p>

<p> - Poderíamos ter a solução desta forma, entretanto, usaríamos dois comandos diferentes quando podemos usar apenas uma linha de código.</p>

## Passo 4 - Utilizando o comando <b>grep</b>, <b>xargs</b> e <b>pipes</b> <br>

<p> - Utilizaremos o nosso comando find, utilizando a saída dele como um argumento para um novo input. </p>

![Passo 7](img/Passo_7.png) 

<p> - Vamos falar a partir do nosso pipe representado pelo "<b>|</b>". O que estamos querendo passar com o nosso comando, é mais simples do que aparenta.</p>
<p> - Nós pegaremos o output do primeiro comando que é find / -type -name arquivo? Concatenando esta saída em um novo argumento com as junções da | + o comando <b>xargs</b>. O resto do comando grep segue a mesma lógica descrita acima. </p>

<p> - Desta forma o nosso comando fica: <b>find / -d -name arquivo ? | xargs grep -r "achou"</b> </p>

<p> - Em um resumo mais simplificado, estamos pegando a saída do comando <b>find</b> que seria o caminho <b>/tmp/arquivos/</b> e estamos concatenando com o comando grep, e quem faz esta ponte entre ambos os comandos transformando a saída em um argumento é a junção da barra pipe | com o comando xargs. </p>

<p> - Este comando procuraria recursivamente a partir do diretório /tmp/arquivos/ todos os arquivos existentes dentro dele que contem a palavra "achou". Sendo a nossa saída: <b>"/tmp/arquivos/pasta3/achou.txt:achou"</b>. </p>

## Passo 5 - Resumo <br>

<p> - Com o comando apropos, podemos achar um comando que não conhecemos por meio de palavras-chave, utilizar o comando find para encontrar um arquivo ou diretório e juntamente com o grep podemos achar dentro deste diretório, trechos de códigos que nos interessem. </p>
