[< MENU](https://github.com/felipemnds/computer-science-notebook/blob/master/README.md)
>  ***Lista de Referências:***
> 1. https://www.youtube.com/watch?v=jFDMZpkUWCw

# A) Visão Geral
Um **Sistema Computacional** é o nome dado à junção de *Hardware + Software*, nosso objeto de estudo nos próximos resumos.
E para entrarmos de vez em Organização e Arquitetura de Computadores, precisamos entender qual é o real significado de cada um desses termos:
1. **Arquitetura** - são os atributos do sistema computacional (como *Multiplicação* por exemplo)
2. **Organização** - são as implementações destes atributos (como *Somas Sucessivas* no caso de uma *Multiplicação*)

# B) Arquitetura de Von Neumann
É divididad em 4 partes:
1. Memória Principal
2. CPU (Unidade Central de Processamento)
3. ULA (Unidade Lógica Aritmética)
4. UC (Unidade de Controle)

![enter image description here](https://lh3.googleusercontent.com/y0w24tNfdIknjIgZG4-5JnMBEVvltgYt7WEnLa-pVgTEKnVmvXlYYPMcLQJxB_mpq084i3PGYaYD "Foto da Arquitetura de Von Neumann")

## 1. Memória Principal
"Caixa" com vários compartimentos acessados pelo **ENDEREÇO** (buscados pela CPU através dos *barramentos*).
## 2. CPU
Responsável por buscar operação na *memória*, executar e armazenar novamente na *memória*. Armazena ULA, Registradores e UC (como a figura acima mostra).
## 3. ULA 
Circuitos lógicos que realizam operações básicas.
## 4. Registradores
São posições de memória construídas na CPU, porém contam com um acesso mais rápido.
**Curiosidade: Os registradores são os responsáveis por definir se uma arquitetura é de 32 bits ou 64 bits.**
## 5. UC
Controla várias funções na CPU (como busca de dados na memória, controle ULA<>Registradores)

# C) Ciclo de Von Neumann (ou 'Fetch Decode Execute Cycle')
> Vídeo que ilustra o ciclo: https://www.youtube.com/watch?v=jFDMZpkUWCw&t=1s

Vamos considerar a seguinte instrução:
```
// alto nível
z = x + y
```
ou
```
// baixo nível (assembly)
LOAD [10]
ADD [11]
STORE [12]
```
Agora representaremos a CPU e seus componentes interagindo com a Memória, a saber:
- o ACUMULADOR faz parte da ULA
- o endereçamento acontece crescente de baixo para cima na MEMÓRIA
- as instruções na MEMÓRIA são formatadas como CÓDIGO DE MÁQUINA
![enter image description here](https://lh3.googleusercontent.com/F6tsiBKGILEkLuquHWygt3UzD9YSSgm49mpZkvDQbqnpPzYoj9KhnsvxeSe4-ky8tQZUGUJs0Plx)

## Busca - 1. PC (Program Counter)
Armazena o endereço da próxima instrução a ser buscada
## Busca - 2. MAR (Memory Address Register)
Recebe o endereço de PC
## Busca - 3. MDR (Memorey Data Register)
Armazena o conteúdo que está no [MAR]
## Busca - 4. IR (Instruction Register)
Recebe [MDR], uma instrução.
## ++[PC]
Antes de executar a instrução atual, PC aponta para o próximo endereço.
## Decodificação/Execução - 5. UC (Unidade de Controle)
Recebe [IR], instrução a ser executada
## Execução - 6. MAR (Memory Address Register)
Recebe o **endereço** da memória que a instrução precisa 
## Execução - 7. MDR (Memorey Data Register)
Recebe o **conteúdo** da memória que a instrução precisa 
## Execução - 8. AC (Acumulator)
Recebe os conteúdo que serão usados dentro da ULA
## OBS.: Caminho de Dados
> MAR -> MEMÓRIA PRINCIPAL
> MBR <-> MEMÓRIA PRINCIPAL
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc4Njg5MzMwNywtNTI0MTYxNDQ0LDExOD
cxNzQ2MjNdfQ==
-->