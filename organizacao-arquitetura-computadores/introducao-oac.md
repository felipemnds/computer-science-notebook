>  ***Lista de Referências:***
> 1. https://www.youtube.com/watch?v=jFDMZpkUWCw
> 2. https://www.youtube.com/watch?v=qzSdglU0SBc&list=PLylNWPMX1lPnipZzKdCWRj2-un5xvLLdK

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

![Foto da Arquitetura de Von Neumann](https://computerscience.gcse.guru/wp-content/uploads/2016/04/Von-Neumann-Architecture-Diagram.jpg)

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
![Imagem do Ciclo de Execucao](https://lh3.googleusercontent.com/78ycBSxJqGW85Dh4JuDed_nR20BBKXUnkptgKudNnSoF8oUp260dYuZ5h3bpNCfojk3rcp2UOJX3xzGOYa_4G7i_K3uPa14uXY-Mdd6yKvdMuR6nR77reHR_NSAcB_HceYobdhm1Fx3mgOIwXACb_VqefXVyzo8CekK1LUYeuUhPfJ_toBaTIgsUxFc5f-0z4zSBxmBHZ-E-LzwdOWvAyeUQaGDtcQhQZVyztKhd95-sphaUYUIZ1c_8AjeSO0WlLKfhQ7VYzTpIfEmBnzLC2jRG4vphvI0ecmAhemI_A0qUKP4x6KT_umPugGVFU88O0Ov6YtzMP1Fa1xZlZsTSBuLp_PJnWJ0VIu3Bna5qC1WEUIo5cQSKcUXKXGeafTWCDNU-a2V5h7NIC4JB45wOafAjSSO4pTN1Pa8k1DZc18YLmj7do8CVvlHie8lutindmlokpbde8gPzrnrd7ewOQByZ25_4LJuG_XW5DtA3cGoQ5TbvBf53-qNyFyBzH2gNhKWf2pHGxJH0mmQsBBiM2Z62mCGPev2U2b8njJiJnifsVsRczCjQeJoBjRzhwAHflVDjZrLlX-CSwPnXoYaqqw58cXnVCSclHqHhZGWJEiyHweL8sIMp3GAcNwYgYZb6DbbakPxZqLBYNaUuzMn4ra5V=w900-h600-no)
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
