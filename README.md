<h2 p align="center" > Localizar um texto em um diretorio que não sabemos onde esta. </h2></p>

## Passo 1 - Localizando um comando com apropos.
<br><p> - O comando apropos serve para localizar um comando que você não lembra a sintaxe atráves de palavras-chaves que descrevam a funcionalidade que este comando teria. <br> </p>

<p> - Estamos procurando um comando que encontre uma pasta especifica.

![Passo 1](img/Passo_1.png) 

<p> <i> - Dependendo do sistema precisa-se atualizar o cache para o comando apropos funcionar corretamente, o comando é <b>mandb</b></i> <p>

<p> - Procuramos o comando find que localiza arquivos em uma hierarquia de diretórios. <br>
- Mas antes o que significa este <b>(1)</b> a frente do comando find?
</p>

![Passo 3](img/Passo_3.png) 

<p> - Utilizando o comando <b>man man</b> (que seria o manual do próprio manual do linux), encontramos a descrição do tipo de função que determinada palavra teria caso tivesse determinado numero envolto do <b>()</b>.
<p> - Desta forma procuramos comandos executaveis, que correspondem ao número 1, que nosso comando <b>find</b> possui.
<p> - Por exemplo, poderiamos possuir o mesmo comandos derivatidos de find, <i>como find-lib(5) find-ker(9)</i>, mas apenas precisassemos obter comandos executaveis, para isso utilizariamos a seguinte flag abaixo junto com o comando <b>apropos</b>.
<br>
<p><b><i> - Os comandos find-lib e find-ker não existem, apenas os mencionei a titulo ilustrativo.</b></i></p>

![Passo 2](img/Passo_2.png) 
<p> - Utilizaremos a flag -s acompanhada do número da sessão que buscamos, nesse caso a sessão (1) que é destinada para comandos executaveis.</p>
<p> - O comando ficaria: <b>apropos -s 1 search</b>

![Passo 4](img/Passo_4.png) 
<p> - Note que a filtragem ficou relativamente menor, pois agora o apropos só nos passa a sessão que escolhemos. </p>

## Passo 2 - Utilizando o comando <b>find</b> <br>

<p> - Agora que sabemos qual comando utilizar para encontrar um arquivo ou diretorio, vamos entender separadamente como construir um <b>find</b>

<p> Para este exemplo estamos procurando uma pasta chamada <b>arquivos</b>.

<p> Não fazemos ideia onde esta pasta esta, apenas sabemos seu nome e que ela é um diretório. Para localiza-la podemos utilizar o seguinte raciocinio: </p>
<p> - Para se encontrar uma caneta perdida dentro de um quarto, primeiro precisamos entrar neste quarto. O comando find segue esta mesma analogia. </p>
<p> - Em sua sintaxe seria find (diretório de pesquisa), no nosso exemplo pegaremos desde o diretório / + a flag -name que sera onde colocaremos o nome do diretório que estamos buscando, que seria <b>arquivos.</b></p>
<p> - Nosso comando então seria: find / -name "arquivos"</p>


