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

A aplicação deve permitir fazer pesquisas a **planetas** e **estrelas**.

_Em construção_

<!--Usar programação por objetos, com lista de estrelas e lista de planetas e ligadas entre eles

Abrir ficheiro
Procura de planetas | Procura de estrelas
Menu de procura em cima, procura atualizada em tempo real em baixo
String contains: pl_name
Optional and student chose how to: method
Others: All numbers, require min and max, differentiate between float and int
No value == dont use in search

Lista atualizada é percorrível e scrolável, deve permitir ver detalhes do
planeta ou estrela ao carregar enter

Quando no menu planeta ou estrela, deve ser possível ver a estrela ou planetas
associados, scrolando

Isto dito em cima podem ser layers de avaliação

A aplicação deve mostrar ao utilizador um menu de pesquisa de títulos, e caso
implementem a [Fase 4], um menu de pesquisa de pessoas. Em qualquer dos casos,
deve ser possível usar como critérios de pesquisa os campos indicados em cada
uma das [fases de desenvolvimento]. Deve também ser possível usar qualquer um
destes campos como critério de ordenação, exceto se existir indicação em
contrário.

Os resultados devem aparecer na forma de uma lista, mostrando para cada item
dois ou três campos que consideram importantes. Por exemplo, no caso dos
títulos deve aparecer o seu tipo, o título principal e o ano de lançamento.
Se o projeto for desenvolvido em consola, podem ser apresentados 20 ou 30 itens
de cada vez, sendo necessário que o utilizador pressione uma tecla para ver os
próximos 20/30 itens. Por outro lado, se se tratar de um projeto Unity, a lista
de jogos deve ser *scrollable* ("rolável") para cima e para baixo. Também é
possível ter uma lista "rolável" em modo consola, como implementado na solução
do [2º projeto de LP1 2018/19].

Deve ser possível clicar ou selecionar um dos resultados da lista, caso no qual
aparecerá uma nova tela/janela mostrando os detalhes do item em questão. Estes
detalhes sao exatamente aqueles pelos quais é possível pesquisar. Nas fases
[3][Fase 3] e [4][Fase 4] existem possibilidades adicionais de interação quando
se chega a esta tela, como referido adiante.



No caso do **Discovery method**, serão valorizadas soluções que permitam
ao utilizador escolher apenas entre os tipos e/ou géneros existentes na base de
dados.

Ordenar os resultados das pesquisas

Adicionalmente, o utilizador deve ter a opção de ver diretamente a tela de
informação do título pai.

Na tela de informação de um título pai, deve existir a opção adicional de
fazer uma pesquisa automática pelos respetivos títulos filho. Na lista
"rolável" que aparecerá depois com os resultados desta procura, o utilizador
poderá naturalmente clicar/selecionar um destes títulos filho, aparecendo então
uma tela de informação sobre o título filho selecionado (que por sua vez tem a
opção de ver a diretamente a tela de informação do título pai, e por ai fora).

### Fase avançada: pesquisa em várias tabelas

Misturar pesquisa de planetas com dados de estrelas e vice-versa.

Além disso, não
incluí código importante a nível do LINQ para fases posteriores, nomeadamente o
método [Join()] (também disponível na forma de [expressão de *query*][join]).-->

## Ficheiro de dados

### Como obter

O ficheiro com os dados sobre os exoplanetas deve ser obtido [neste
link][NASAexoData], no menu "Download Table", selecionando as opções "CSV
Format", "Download Currently Checked Columns", "Download Checked (and Filtered)
Rows", "Values Only (no errors, limits, etc.)" e clicando na opção "Download
Table".

Está também incluído outro [ficheiro de teste](teste.csv) neste repositório,
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
* `st_age`- Idade da estrela (em Giga-anos, ou seja, por milhar de milhão de anos).
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

## Organização do projeto e estrutura de classes

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
* O código exemplo é disponibilizado através da licença
  [Mozilla Public License 2.0][MPL2].

## Metadados

* Autor: [Nuno Fachada]
* Curso:  [Licenciatura em Videojogos][lamv]
* Instituição: [Universidade Lusófona de Humanidades e Tecnologias][ULHT]

[LINQ]:https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries
[CC BY-NC-SA 4.0]:https://creativecommons.org/licenses/by-nc-sa/4.0/
[MPL2]:https://www.mozilla.org/en-US/MPL/2.0/
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
[`Process`]:https://docs.microsoft.com/dotnet/api/system.diagnostics.process
[`Environment`]:https://docs.microsoft.com/dotnet/api/system.environment
[`Path`]:https://docs.microsoft.com/dotnet/api/system.io.path
[Rainbow CSV]:https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv
[GZipStream]:https://docs.microsoft.com/dotnet/api/system.io.compression.gzipstream
[StreamReader]:https://docs.microsoft.com/dotnet/api/system.io.streamreader
[ListSizeCtor]:https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1.-ctor#System_Collections_Generic_List_1__ctor_System_Int32_
[Join()]:https://docs.microsoft.com/dotnet/api/system.linq.enumerable.join
[join]:https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/join-clause
[2º projeto de LP1 2018/19]:https://github.com/VideojogosLusofona/lp1_2018_p2_solucao
[fases de desenvolvimento]:#fases-de-desenvolvimento
[Fase 1]:#fase-1-pesquisa-de-títulos-básica
[Fase 2]:#fase-2-pesquisa-de-títulos-com-classificação
[Fase 3]:#fase-3-ligação-entre-séries-e-os-respetivos-episódios
[Fase 4]:#fase-4-pesquisa-de-pessoas
[orgclasses]:#organização-do-projeto-e-estrutura-de-classes
[objetivos]:#objetivos-e-critério-de-avaliação
[NASAexo]:https://exoplanetarchive.ipac.caltech.edu/
[NASAexoData]:https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=PS&constraint=default_flag=1
[CSV Rainbow]:https://marketplace.visualstudio.com/items?itemName=mechatroner.rainbow-csv
[LibreOffice Calc]:https://www.libreoffice.org/download/download
