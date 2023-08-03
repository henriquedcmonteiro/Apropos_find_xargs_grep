<h3 p align="center" > <i>Forgive me for any grammatical errors, English is not my native language. </i> </h3></p>

<h2 p align="center" > Find a text in a directory that we do not know where it is. </h2></p>

## Step 1 - Finding a command with apropos.

<br><p> - The apropos command serves to locate a command that you do not remember the syntax of, by means of keywords that describe the functionality that this command would have. <br> </p>

<p> - We are looking for a command that finds a specific folder.

![Passo 1](img/Passo_1.png) 

<p> <i> - Depending on the system you need to update the cache for the apropos command work correctly, the command is <b>"mandb"</b></i>. <p>

<p> - We are looking for the "find" command that locates files in a directory hierarchy. <br>
- But first what does this <b>(1)</b> in front of the "find" command mean? </p>

![Passo 3](img/Passo_3.png) 

<p> - Using the <b>"man" command</b> (which would be the linux manual itself), we find the description of the type of function a given word would have if it had a given number wrapped around the <b>()</b>.</p>

<p> - This way we look for executable commands, which correspond to the number 1, that our <b>find</b> command has. </p>

<p> - For example, we could have the same derivative commands as <b>find</b>, such as <i>find-lib(5) find-ker(9)</i>, but we only need to get executable commands, for this we would use the following "flag" below next to the <b>apropos command</b>.</p><br>


<p><b><i> - The commands find-lib and find-ker do not exist, I only mentioned them for illustrative purposes.</i></b></p>

![Passo 2](img/Passo_2.png) 

<p> - We will use the -s flag accompanied by the session number we are looking for, in this case session (1) intended for executable commands.</p>

<p> - The command would be: <b>apropos -s 1 search</b></p>

![Passo 4](img/Passo_4.png) 

<p> - Note that the filtering has become relatively smaller, as now the <b>apropos</b> only passes us the session we have chosen. </p>

## Passo 2 - Utilizando o comando <b>find</b> <br>

<p> - Now that we know which command to use to find a file or directory, let's understand separately how to construct a <b>find command.</b>. </p>

<p> - For this example we are looking for a folder called <b>arquivos</b>.</b>. </p>

<p> - We have no idea where the folder in question is located, we only know its name and that it is a directory. To locate it we can use the following reasoning: </p>

<p> - To find a pen lost in a room, we first need to enter this room. The <b>find</b> command follows this same analogy. </p>

<p> - In its syntax we start with the command b>find</b> (search directory), in our example, we will take from the directory / + the flag b>-name</b> which will be where we will put the name of the directory we are looking for, which in turn is the directory b>arquivos.</b></p>

<p> - Our command would then be: <b>find / -name "arquivos"</b></p>

![Passo 5](img/Passo_5.png) 

<p> - Here we will talk about two distinct points, the first is the character <b>"?"</b> and the second is the output of our command. </p>

<p> - The character <b>?</b>, we can call a wildcard character, it has the function of finding or not any character <b>only</b> in that position. For example, if we were in doubt whether the folder is called <b>"arquivos"</b> or <b>"arquivo"</b> in singular, we could use the wildcard character that would give us any character or none after the word b>arquivo</b>. </p>

<p> - The second point is the output of the command, we notice that we have two results, but why is that? Because we should specify the type of file we want to find, otherwise we can either have regular, special or directory files output. </p>

<p> - To solve this is simple, just pass the flag <b>-type</b> followed by the <b>parameter d</b> of "directory". </p>

<p> - We have finally found our directory, but what if now we still need to find a piece of code text inside this directory that could, for example, be an error? </p>

## Passo 3 - Using the <b>grep command</b> <br>

<p> - The grep command is the key to this search, it alone could solve our task through both absolute and relative path. </p>

<p> <i> - Absolute path is the one that is declared from the root of the system identified by / to the place where you want to go. </i> </p>
<p> <i> - The relative path is the one that starts from the directory we are currently in. </i> </p>

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
