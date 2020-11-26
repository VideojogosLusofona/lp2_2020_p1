<!--
1º Projeto de Linguagens de Programação II 2020/2021 (c) by Nuno Fachada

1º Projeto de Linguagens de Programação II 2020/2021 is licensed under a
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.

You should have received a copy of the license along with this
work. If not, see <http://creativecommons.org/licenses/by-nc-sa/4.0/>.
-->

# 1º Projeto de Linguagens de Programação II 2020/2021

## Introdução

Os grupos devem implementar uma aplicação em C# que realize pesquisas na [base
de dados de exoplanetas da NASA][NASAexo], disponível sob a forma de um
ficheiro [CSV].

A aplicação pode ser desenvolvida numa das seguintes plataformas, sem qualquer
benefício ou limitação em termos de nota:

1. Console App .NET Core
2. Unity 2020.1.\*

No entanto, é requisito obrigatório deste projeto que a aplicação utilize
[LINQ] (sintaxe fluente ou expressões de *query*) para realizar as pesquisas.
É necessário ir mais além do que foi lecionado nas aulas sobre [LINQ], e a
discussão do projeto incidirá essencialmente na forma como construíram as
*queries*.

## Funcionamento da aplicação

A versão standard da aplicação deve permitir fazer pesquisas a **planetas** e
**estrelas**, separadamente, e terá uma nota máxima de 2.5 valores (em 3
possíveis). A [versão avançada](#versão-avançada) requer que as pesquisas possam
ser feitas com campos de planetas e estrelas ao mesmo tempo (por exemplo, listar
todos os planetas que orbitam uma estrela 10x maior que o sol).

A aplicação pode ser implementada de forma interativa (Unity ou consola) ou
não-interativa (apenas consola), tal como descrito em [Formas de
implementação](#formas-de-implementação). Em qualquer dos casos, a aplicação
standard (não avançada) deve ter as seguintes funcionalidades:

* Abrir o ficheiro de dados e criar uma lista de planetas e uma lista de
  estrelas. Os dados de cada estrela devem ser obtidos no ficheiro de dados a
  partir dos planetas que as orbitam (ver secção [Campos de
  interesse](#campos-de-interesse)).
* Fazer pesquisas por planetas usando os campos específicos de planeta.
  * Na [versão avançada](#versão-avançada) deve ser possível também incluir
    campos de estrela na pesquisa de planetas.
* Fazer pesquisas por estrelas usando os campos específicos de estrela.
  * Na [versão avançada](#versão-avançada) deve ser possível também incluir
    campos de planeta na pesquisa de estrelas.
* Os campos numéricos devem permitir especificar um valor de pesquisa mínimo e
  um valor de pesquisa máximo.
* Os campos de texto devem verificar se o valor de pesquisa é uma _substring_
  do campo em questão dos planetas ou estrelas, e esta pesquisa deve ser
  independente de maiúsculas ou minúsculas.
* Caso um utilizador não indique qualquer um dos campos de pesquisa, a aplicação
  deve assumir que não existe qualquer restrição (sendo possível, por exemplo,
  especificar apenas um valor mínimo para dado campo e não o máximo).
* Deve ser possível ordenar os resultados da pesquisa por qualquer um dos
  campos utilizados, tanto de forma ascendente como de forma descendente.
  * Serão valorizadas soluções que permitam aplicar um critério de ordenação
    secundário (usado quando existe um empate no critério primário).
* Ver informação detalhada sobre um planeta.
* Ver informação detalhada sobre uma estrela.
* Não _crashar_ com exceções, mas sim mostrar ao utilizador, de forma elegante,
  possíveis erros que possam ocorrer (por exemplo, na leitura do ficheiro).

### Formas de implementação

A aplicação pode ser implementada de forma interativa (Unity ou consola) **ou**
não-interativa (apenas consola), tal como descrito nas secções seguintes.

#### Aplicação interativa

Na implementação interativa (em Unity ou consola), deve aparecer inicialmente
uma caixa de diálogo na qual o utilizador pode especificar o ficheiro a abrir.
Uma vez aberto com sucesso o ficheiro, devem aparecer as opções de pesquisar
planetas e pesquisar estrelas. Selecionando uma das opções de pesquisa, deve
então aparecer um UI que permita especificar os vários campos a filtrar, bem
como indicar o(s) critério(s) de ordenação. Idealmente este UI terá espaço para
a apresentação dos resultados, sendo possível alterar critérios de pesquisa
e de ordenação

Os resultados devem aparecer na forma de uma lista, mostrando todos os campos de
cada item. No caso dos planetas, a informação sobre a estrela deve resumir-se ao
seu nome. No caso de estrelas, a informação sobre os seus planetas deve
resumir-se ao seu número. Se o projeto for desenvolvido em consola, podem ser
apresentados 20 ou 30 itens de cada vez, sendo necessário que o utilizador
pressione uma tecla para ver os próximos 20/30 itens. Por outro lado, se se
tratar de um projeto Unity, a lista de jogos deve ser *scrollable* ("rolável")
para cima e para baixo. Também é possível ter uma lista "rolável" em modo
consola, como implementado na solução do [2º projeto de LP1 2018/19].

Deve ser possível clicar ou selecionar um dos resultados da lista, caso no qual
aparecerá uma nova tela/janela mostrando os detalhes (campos) do item em
questão, mas por extenso e mostrando as unidades (e.g. km/s) no caso de campos
numéricos. No caso da tela/janela de informação sobre um planeta, deve também
aparecer agora a informação completa sobre a estrela que orbita. No caso da
tela/janela de informação sobre uma estrela, deve aparecer uma lista dos nomes
dos planetas que a orbitam.

A qualquer momento deve ser possível voltar atrás (incluíndo abrir um novo
ficheiro), bem como sair da aplicação.

#### Aplicação não-interativa em consola

Nesta versão a aplicação não tem qualquer UI, funcionando inteiramente com as
opções passadas na linha de comandos. Deve ter toda a funcionalidade indicada
em [Funcionamento da aplicação](#funcionamento-da-aplicação), escrevendo todo o
seu _output_ no terminal, de seguida e sem paragens. Alguns exemplos (o nome
exato das opções fica à escolha do aluno, mas convém serem óbvios):

```bash
# Procura por planetas com temperatura entre 150 e 400 Kelvin e mais pequenos
# que a Terra
dotnet run -p AstroFinder -- search-planets --eqt-min 150 --eqt-max 400 --rade-max 1.0

# Procura por estrelas com pelo menos 2 mil milhões de anos e a uma distância
# máxima de 5 parsecs do sistema solar
dotnet run -p AstroFinder -- search-stars --age-min 2.0 --dist-max 5.0

# Procura por planetas descobertos com o método de transito até ao ano 2010
dotnet run -p AstroFinder -- search-planets --method "transit" --year-max 2010

# Mostra informação detalhada sobre planeta Proxima Cen b (exoplaneta conhecido
# mais próximo da Terra)
dotnet run -p AstroFinder -- planet-info "proxima cen b"
```

Por omissão, o _output_ deve ser aparecer formatado e fácil de ler, em forma de
lista (mesmo que se pretenda apenas a informação sobre um planeta ou estrela,
caso no qual a lista a apresentar terá tamanho 1). No caso do último comando, o
_output_ poderia ser algo do género:


```
Planet name     Star name      Disc. method     Year    Orbital         Radius      Mass        Eq. Temp.
                                                        Period (days)   (vs Earth)  (vs Earth)   (Kelvin)
---------------------------------------------------------------------------------------------------------
Proxima Cen b   Proxima Cen    Radial Veloc...  2016           11.186          N/A        1.27        234
```

Deve ainda existir uma opção (por exemplo, `--csv`) para formatar os dados
exatamente de acordo com o formato dos ficheiros de entrada. No caso anterior
seria:

```
pl_name,hostname,discoverymethod,disc_year,pl_orbper,pl_rade,pl_masse,pl_eqt
Proxima Cen b,Proxima Cen,Radial Velocity,2016,11.186,,1.27,234
```

Atenção que não é necessário gravar este _output_ para um ficheiro. Para isso
bastaria executar a aplicação da seguinte forma (repetindo o exemplo anterior):

```bash
dotnet run -p AstroFinder -- planet-info "proxima cen b" --csv >  output.csv
```

Deve ser possível voltar a abrir o ficheiro criado com a aplicação, exceto no
caso da procura de estrelas, que geraria um ficheiro incompatível.

Caso o grupo opte pela implementação não-interativa, deve existir um _help_ por
omissão que descreva todas as opções possíveis. Além disso, o relatório deve
conter uma tabela com a descrição de todas as opções.

Uma abordagem flexível para tratamento de opções de linha de comando está
disponível no [2º projeto de LP1 2018/19]. Uma opção mais avançada, mas muito
mais rápida após a curva de aprendizagem, é usar a biblioteca [Command Line
Parser][CLParserLib], que funciona com atributos. Para fazerem uso desta
biblioteca basta executarem o seguinte comando na pasta do vosso projeto (ou
seja, na pasta que contém o ficheiro `.csproj`):

```bash
dotnet add package CommandLineParser --version 2.8.0
```

A partir desse momento podem fazer `using` dos _namespaces_ da biblioteca.

### Versão avançada

_Em construção_

<!--

Fase avançada: pesquisa em várias tabelas

Permite ultrapassar a limitação de 2.5 valores.

Misturar pesquisa de planetas com dados de estrelas e vice-versa.

Além disso, não
incluí código importante a nível do LINQ para fases posteriores, nomeadamente o
método [Join()] (também disponível na forma de [expressão de *query*][join]).


No caso de planetas, deve existir a opção de ver os detalhes da
estrela associada. No caso da estrela, deve existir a opção de ver uma lista
dos planetas associados (na prática é realizada uma procura de planetas)


Adicionalmente, o utilizador deve ter a opção de ver diretamente a estrela
associada a um planeta, ou os planetas associados a uma estrela.

Na tela de informação de uma estrela, deve existir a opção adicional de
fazer uma pesquisa automática pelos respetivos planetas. Na lista
"rolável" que aparecerá depois com os resultados desta procura, o utilizador
poderá naturalmente clicar/selecionar um destes planetas, aparecendo então
uma tela de informação sobre o planeta selecionado (que por sua vez tem a
opção de ver a diretamente a tela de informação da sua estrela, e por ai fora).


-->

### Compatibilidade

Caso seja implementada em consola, a aplicação deve funcionar em Windows, macOS
e Linux. A melhor estratégia para garantir que assim seja é testar a aplicação
em Linux (e.g., numa máquina virtual). Algumas instruções incompatíveis com
macOS e Linux são, por exemplo:

* [Console.Beep()](https://docs.microsoft.com/dotnet/api/system.console.beep)
* [Console.SetBufferSize()](https://docs.microsoft.com/dotnet/api/system.console.setbuffersize)
* [Console.SetWindowPosition()](https://docs.microsoft.com/dotnet/api/system.console.setwindowposition)
* [Console.SetWindowSize()](https://docs.microsoft.com/dotnet/api/system.console.setwindowsize)
* Entre outras.

As instruções que só funcionam em Windows têm a seguinte indicação na sua
documentação:

![The current operating system is not Windows.](img/notsupported.png "The current operating system is not Windows.")

Os projetos Unity geralmente funcionam bem em Linux e macOS, mesmo que sejam
desenvolvidos em Windows.

## Ficheiro de dados

### Como obter

O ficheiro com os dados sobre os exoplanetas deve ser obtido [neste
link][NASAexoData], no menu "Download Table", selecionando as opções "CSV
Format", "Download Currently Checked Columns", "Download Checked (and Filtered)
Rows", "Values Only (no errors, limits, etc.)" e clicando na opção "Download
Table".

Está também incluído outro [ficheiro de teste](test.csv) neste repositório,
igualmente válido (ver secção seguinte).

### Formato do ficheiro

O ficheiro pode ter comentários (linhas que começam com um cardinal, `#`) e
linhas em branco. Tanto uns como outros devem ser ignorados.

A primeira linha de dados (que não seja comentário ou linha em branco) contém o
cabeçalho, ou seja, o nome das colunas/campos, separados por vírgulas. As
linhas de dados seguintes contêm os dados de cada exoplaneta individual e da sua
estrela, dados esses que estão separados por vírgulas. Os campos/colunas podem
aparecer em qualquer ordem, ordem essa definida pelo nome dos campos no
cabeçalho.

### Campos de interesse

A aplicação deve considerar apenas os seguintes campos/colunas, ignorando os
restantes:

* `pl_name` - Nome do planeta.
* `hostname` - Nome da estrela que o planeta orbita.
* `discoverymethod` - Método de descoberta.
* `disc_year` - Ano de descoberta.
* `pl_orbper`- Período orbital (em dias).
* `pl_rade` - Raio do planeta (em comparação com a Terra).
* `pl_masse` - Massa do planeta (em comparação com a Terra).
* `pl_eqt` - Temperatura de equilíbrio do planeta (em Kelvins).
* `st_teff` - Temperatura efetiva da estrela (em Kelvins).
* `st_rad` - Raio da estrela (em comparação com o Sol).
* `st_mass` - Massa da estrela (em comparação com o Sol).
* `st_age`- Idade da estrela (em Giga-anos, ou seja, por milhar de milhão de
  anos).
* `st_vsin` - Velocidade de rotação da estrela (em km/s).
* `st_rotp` - Período de rotação da estrela (em dias).
* `sy_dist` - Distância entre a Terra e a estrela (em Parsecs, sendo 1 Parsec ≈
  3,26 anos-luz).

Os campos relativos à estrela referem-se à estrela que o planeta orbita. Esta
informação pode aparecer repetida, pois vários planetas podem orbitar a mesma
estrela. Existem situações em que:

1. A informação sobre a estrela é contraditória (temperaturas ligeiramente
   diferentes, etc).
2. Alguns campos da estrela aparecem associados a um dos seus planetas mas não
   a outros.

No primeiro caso, a aplicação pode optar por usar a primeira informação válida
que encontrar ou ir substituíndo a mesma à medida que novos planetas
pertencentes à mesma estrela vão aparecendo. No segundo caso, a aplicação deve
tentar compor o máximo de informação sobre a estrela, mesmo que esta informação
venha de diferentes planetas que a orbitam.

### Como abrir para visualização

O ficheiro pode ser aberto (apenas para visualização) no Visual Studio Code com
a extensão [CSV Rainbow], configurada da seguinte forma
(_"File => Preferences => Settings"_):

* Editor: Large File Optimizations => OFF
* Rainbow_csv: Comment_prefix => #

Com o ficheiro aberto, podemos clicar em baixo na barra azul onde diz "Align"
para alinhar as colunas, facilitando a visualização (e depois "Shrink" para
voltar ao formato original).

Também é possível abrir o ficheiro para visualização no  [LibreOffice Calc],
escolhendo apenas "Comma" (ou "Vírgula") como separador.

O ficheiro não deve ser alterado, nem pelo projeto a desenvolver, nem
manualmente. O ficheiro **não deve ser incluído na entrega do projeto**, **nem
de alguma forma adicionado ao repositório Git**. Projetos que não cumpram esta
regra não serão avaliados.

### Como abrir os ficheiros na aplicação a desenvolver

* A aplicação deve ignorar os comentários (linhas começadas com `#`), bem como
  linhas em branco.
* A aplicação deve ser capaz de abrir ficheiros com menos ou mais colunas, tendo
  apenas em conta as [colunas de interesse](#campos-de-interesse).
* A aplicação deve ignorar colunas que não sejam do seu interesse.
* A aplicação deve conseguir abrir o ficheiro seja qual for a ordem das colunas.
  Ou seja, a aplicação não deve esperar que as colunas estejam numa certa ordem.
* A informação mínima obrigatória para o ficheiro ser considerado válido é a
  dada pelas seguintes colunas:
  * `pl_name`: Nome do planeta.
  * `hostname`: Nome da estrela que contém o planeta.

  O ficheiro deve ser considerado inválido senão tiver estas duas colunas.
* Se o ficheiro tiver alguma coluna de interesse em falta, a aplicação deve
  considerar que essa informação não existe para todos os planetas e/ou
  estrelas.
* Se algum campo não estiver vazio para dado planeta/estrela, a aplicação
  deve considerar que essa informação não existe para esse planeta (ou estrela)
  em particular.
* Cada campo de interesse que estiver disponível deve ser convertível para o seu
  tipo esperado (por exemplo, se o ano de descoberta for representado por letras
  e não dígitos). Caso contrário o ficheiro deve ser considerado inválido.
* O ficheiro também deve ser considerado inválido se o número de campos em
  alguma das linhas não corresponder ao número de colunas indicado no cabeçalho
  (cabeçalho esse que contém o nome dos campos).
* Se o ficheiro indicado tiver um formato inválido, a aplicação deve mostrar uma
  mensagem de erro apropriada.

## Organização do projeto e estrutura de classes

<!--

Usar programação por objetos, com lista de estrelas e lista de planetas e ligadas entre eles

single responsibility: classe controladora, classe GUI/UI, classe que abre
o ficheiro e produz as listas, classe que faz as queries

-->

_Em construção_


O projeto deve estar devidamente organizado, fazendo uso de classes, `struct`s
e/ou enumerações, conforme seja mais apropriado. Cada tipo (i.e., classe,
`struct` ou enumeração) deve ser colocado num ficheiro com o mesmo nome. Por
exemplo, uma classe chamada `Star` deve ser colocada no ficheiro `Star.cs`.
Por sua vez, a escolha da coleção ou coleções a usar também deve ser adequada
ao problema.

A estrutura de classes deve ser bem pensada e organizada de forma lógica,
fazendo uso de *design patterns* quando e se apropriado. Em particular, o
projeto deve ser desenvolvido tendo em conta os princípios de programação
orientada a objetos, como é o caso, entre outros, dos princípios [SOLID].

Estes princípios devem ser balanceados com o princípio [KISS], crucial no
desenvolvimento de qualquer aplicação.

É de realçar que o uso de LINQ, Lambdas e *nullables* é essencial neste
projeto.

### Sugestões de otimização

O ficheiro de dados pode ser grande, pelo que pode ser útil fazer algumas
otimizações. Existem várias técnicas que podem e devem ser utilizadas para este
fim, nomeadamente:

* Os campos existentes em cada linha não necessários devem ser ignorados.
* Devem ser utilizados tipos apropriados e o mais "pequenos" possível para cada
  um dos campos. Por exemplo, para representar o ano de lançamento é mesmo
  preciso um `int`? Para representar a letra de um planeta será mesmo preciso
  uma `string`?
* As coleções usadas para guardar os dados devem ser pré-alocadas com o tamanho
  exato necessário. Por exemplo, as listas têm um [construtor][ListSizeCtor] que
  aceita como parâmetro o tamanho inicial da lista, e os _arrays_ são sempre
  pré-alocados.
* No Unity, ao apresentarem os resultados de dada pesquisa, tenham cuidado com
  a quantidade de resultados que injetam no UI. Demasiados resultados podem
  prejudicar o desempenho e até *crashar* a aplicação. O [LINQ] tem formas de
  devolver apenas alguns resultados de cada vez, evitando esta situação.



## Objetivos e critério de avaliação

Este projeto tem os seguintes objetivos:

* **O1** - Programa deve funcionar como especificado.
* **O2** - Projeto e código bem organizados, nomeadamente:
  * Estrutura de classes bem pensada (ver secção
    [Organização do projeto e estrutura de classes][orgclasses].
  * Código devidamente comentado e indentado.
  * Inexistência de código "morto", que não faz nada, como por exemplo
    variáveis, propriedades ou métodos nunca usados.
  * Projeto compila e executa sem erros e/ou *warnings*.
* **O3** - Projeto adequadamente documentado. Documentação deve ser feita com
  [comentários de documentação XML][XML], e a documentação (gerada em formato
  HTML ou CHM com [Doxygen], [DocFX] ou ferramenta similar) deve estar
  incluída no ZIP do projeto, mas **não** integrada no repositório Git.
* **O4** - Repositório Git deve refletir boa utilização do mesmo, com
  *commits* de todos os elementos do grupo e mensagens de *commit* que sigam
  as melhores práticas para o efeito (como indicado
  [aqui](https://chris.beams.io/posts/git-commit/),
  [aqui](https://gist.github.com/robertpainsi/b632364184e70900af4ab688decf6f53),
  [aqui](https://github.com/erlang/otp/wiki/writing-good-commit-messages) e
  [aqui](https://stackoverflow.com/questions/2290016/git-commit-messages-50-72-formatting)).
  Quaisquer *assets* binários, tais como imagens, devem ser integrados
  no repositório em modo Git LFS.
* **O5** - Relatório em formato [Markdown] (ficheiro `README.md`),
  organizado da seguinte forma:
  * Título do projeto.
  * Autoria:
    * Nome dos autores (primeiro e último) e respetivos números de aluno.
    * Informação de quem fez o quê no projeto. Esta informação é
      **obrigatória** e deve refletir os *commits* feitos no Git.
    * Indicação do repositório público Git utilizado. Esta indicação é
      opcional, pois podem preferir desenvolver o projeto num repositório
      privado.
  * Arquitetura da solução:
    * Indicação da forma de implementação (interativo Unity/consola ou
      não-interativo consola).
    * Descrição da solução, com breve explicação de como o programa foi
      organizado, indicação das coleções usadas e porquê, bem como dos
      algoritmos utilizados (e.g., para fazer *parsing* do ficheiro CSV),
      as principais *queries* que construíram, bem como as otimizações
      específicas que implementaram.
    * Um diagrama UML de classes simples (i.e., sem indicação dos
      membros da classe) descrevendo a estrutura de classes.
  * Referências, incluindo trocas de ideias com colegas, código aberto
    reutilizado (e.g., do StackOverflow) e bibliotecas de terceiros
    utilizadas. Devem ser o mais detalhados possível.
  * **Nota:** o relatório deve ser simples e breve, com informação mínima e
    suficiente para que seja possível ter uma boa ideia do que foi feito.
    Atenção aos erros ortográficos e à correta formatação [Markdown], pois
    ambos serão tidos em conta na nota final.

O projeto tem um peso de 3 valores na nota final da disciplina e será avaliado
de forma qualitativa. Isto significa que todos os objetivos têm de ser
parcialmente ou totalmente cumpridos. A cada objetivo, O1 a O5, será atribuída
uma nota entre 0 e 1. A nota do projeto será dada pela seguinte fórmula:

*N = 3 x O1 x O2 x O3 x O4 x O5 x D*

Em que *D* corresponde à nota da discussão e percentagem equitativa de
realização do projeto, também entre 0 e 1. Isto significa que se os alunos
ignorarem completamente um dos objetivos, não tenham feito nada no projeto ou
não comparecerem na discussão, a nota final será zero.

## Entrega

O projeto deve ser entregue por **grupos de 2 a 3 alunos** via Moodle até às
23h de 8 de dezembro de 2020. Deve ser submetido um ficheiro `zip` com a
solução completa do projeto, nomeadamente:

* Pasta escondida `.git` com o repositório Git local do projeto.
* Documentação HTML ou CHM gerada com [Doxygen], [DocFX] ou ferramenta
  similar.
* Ficheiro `README.md` contendo o relatório do projeto em formato [Markdown].
* Ficheiros de imagens, contendo o diagrama UML de classes e outras figuras
  que considerem úteis. Estes ficheiros devem ser incluídos no repositório em
  modo Git LFS.

## Honestidade académica

Nesta disciplina, espera-se que cada aluno siga os mais altos padrões de
honestidade académica. Isto significa que cada ideia que não seja do
aluno deve ser claramente indicada, com devida referência ao respetivo
autor. O não cumprimento desta regra constitui plágio.

O plágio inclui a utilização de ideias, código ou conjuntos de soluções
de outros alunos ou indivíduos, ou quaisquer outras fontes para além
dos textos de apoio à disciplina, sem dar o respetivo crédito a essas
fontes. Os alunos são encorajados a discutir os problemas com outros
alunos e devem mencionar essa discussão quando submetem os projetos.
Essa menção **não** influenciará a nota. Os alunos não deverão, no
entanto, copiar códigos, documentação e relatórios de outros alunos, ou dar os
seus próprios códigos, documentação e relatórios a outros em qualquer
circunstância. De facto, não devem sequer deixar códigos, documentação e
relatórios em computadores de uso partilhado.

Nesta disciplina, a desonestidade académica é considerada fraude, com
todas as consequências legais que daí advêm. Qualquer fraude terá como
consequência imediata a anulação dos projetos de todos os alunos envolvidos
(incluindo os que possibilitaram a ocorrência). Qualquer suspeita de
desonestidade académica será relatada aos órgãos superiores da escola
para possível instauração de um processo disciplinar. Este poderá
resultar em reprovação à disciplina, reprovação de ano ou mesmo suspensão
temporária ou definitiva da ULHT.

*Texto adaptado da disciplina de [Algoritmos e
Estruturas de Dados][aed] do [Instituto Superior Técnico][ist]*

## Referências

* \[1\] Whitaker, R. B. (2016). **The C# Player's Guide** (3rd Edition).
  Starbound Software.
* \[2\] Albahari, J. (2017). **C# 7.0 in a Nutshell**. O’Reilly Media.
* \[3\] NASA (2020). **NASA Exoplanet Archive**. Retrieved from
  <https://exoplanetarchive.ipac.caltech.edu/index.html>.
* \[4\] Freeman, E., Robson, E., Bates, B., & Sierra, K. (2004). **Head First
  Design Patterns**. O'Reilly Media.
* \[5\] Dorsey, T. (2017). **Doing Visual Studio and .NET Code Documentation
  Right**. Visual Studio Magazine. Retrieved from
  <https://visualstudiomagazine.com/articles/2017/02/21/vs-dotnet-code-documentation-tools-roundup.aspx>.

## Licenças

* Este enunciado é disponibilizado através da licença [CC BY-NC-SA 4.0].

## Metadados

* Autor: [Nuno Fachada]
* Curso:  [Licenciatura em Videojogos][lamv]
* Instituição: [Universidade Lusófona de Humanidades e Tecnologias][ULHT]

[LINQ]:https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries
[CC BY-NC-SA 4.0]:https://creativecommons.org/licenses/by-nc-sa/4.0/
[lamv]:https://www.ulusofona.pt/licenciatura/videojogos
[Nuno Fachada]:https://github.com/fakenmc
[ULHT]:https://www.ulusofona.pt/
[aed]:https://fenix.tecnico.ulisboa.pt/disciplinas/AED-2/2009-2010/2-semestre/honestidade-academica
[ist]:https://tecnico.ulisboa.pt/pt/
[Markdown]:https://guides.github.com/features/mastering-markdown/
[Doxygen]:https://www.stack.nl/~dimitri/doxygen/
[DocFX]:https://dotnet.github.io/docfx/
[SOLID]:https://en.wikipedia.org/wiki/SOLID
[KISS]:https://en.wikipedia.org/wiki/KISS_principle
[CSV]:https://en.wikipedia.org/wiki/Comma-separated_values
[XML]:https://docs.microsoft.com/dotnet/csharp/codedoc
[Rainbow CSV]:https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv
[ListSizeCtor]:https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1.-ctor#System_Collections_Generic_List_1__ctor_System_Int32_
[Join()]:https://docs.microsoft.com/dotnet/api/system.linq.enumerable.join
[join]:https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/join-clause
[2º projeto de LP1 2018/19]:https://github.com/VideojogosLusofona/lp1_2018_p2_solucao
[orgclasses]:#organização-do-projeto-e-estrutura-de-classes
[objetivos]:#objetivos-e-critério-de-avaliação
[NASAexo]:https://exoplanetarchive.ipac.caltech.edu/
[NASAexoData]:https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=PS&constraint=default_flag=1
[CSV Rainbow]:https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv
[LibreOffice Calc]:https://www.libreoffice.org/download/download
[CLParserLib]:https://github.com/commandlineparser/commandline
