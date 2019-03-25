>  ***Links Úteis:***
> 1. [MIPS  quick tutorial](http://logos.cs.uic.edu/366/notes/mips%20quick%20tutorial.htm)
> 2. [MIPS Assembly Language Examples](https://courses.cs.washington.edu/courses/cse378/03wi/lectures/mips-asm-examples.html)

>  ***Lista de Referências:***
> 1. https://www.youtube.com/playlist?list=PLylNWPMX1lPlmEeeMdbEFQo20eHAJL8hx
> 2. https://www.youtube.com/playlist?list=PLylNWPMX1lPnipZzKdCWRj2-un5xvLLdK

# 1. Estrutura do Código MIPS
```
  .data
  .align 0
nome: .tipo-de-dado valor(es)  

  .text
  .globl main
main: 
  opcode x, y, z
```

# 2. Instruções MIPS
## Formato geral de 3 operandos
A maioria dos códigos possuem a seguinte aparência:
```
op dest, src1, src2
```
Sendo que *dest, src1 e src2* são registradores. Podemos representar isso da seguinte maneira:
```
dest <- src1 op src2
```
Na linguagem, possuímos 5 tipos de instrução:
1. aritmética
2. lógica
3. transferência de dados
4. *branch* condicional
5. *jump* incondicional
Confira abaixo a tabela completa:
![Tabela completa de instruções](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/mipsasmtable.jpg)

## Register File
Aqui, temos **32 registradores de propósito geral**:
- R0...R31 (cada um tem 32 bits)
- valores de instruções precisam vir dos registradores
Temos alguns registradores especiais:
- R0 é sempre zero
- R29/R31 são usados para chamada de funções
- Hi & Lo guardam resultados de multiplicação

![Representação - Register file](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/autodraw15_03_201922_55_07.png)

# 3. Memória MIPS
MIPS é uma máquina *Register File* de *LOAD/STORE* (carregar/armazenar).

![Representação](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/autodraw15_03_201923_01_45.png)
Cada local na Memória MIPS tem largura de 8 bits (1 byte).

A Memória MIPS é indexada por seu endereço. Uma memória de 4GB por exemplo possui 2^32 locais.

![Representação](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/autodraw15_03_201923_11_09.png)

Ou seja:
- No **endereçamento bit-a-bit**, contamos 0, 1, 2, 3, ...
- No **endereçamento por palavra** contamos 0, 4, 8, 12, ...

# 4. PEM & PSM
- **Processor execution model**: sequencial (em ordem) e atômico (termina tarefa atual antes de continuar)
- **Processor storage model**: instruções e dados são guardados na memória (sem diferenças)

# 5. Detalhes das instruções MIPS 
## Operações de Dados
Seguem o ciclo de execução como base (já explicado anteriormente em [Introdução OAC.)](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/introducao-oac.md)
## Operações de Desvios
Temos o desvio **condicional** ` bne, beq ` e **incondicional** ` j LABEL `. Tais operações mudam o fluxo do programa (ou seja, alteram o **Program Counter**).
> Lembre-se: ` bne/beq ` só comparam registradores com registradores. Ou seja, se queremos comparar um valor com algum número, devemos primeiramente carregar esse número em outro registrador usando ` addi `.

## Codificação das Instruções em Assembly
### Tipo R - Operações comuns

![Representação](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/autodraw15_03_201923_28_05.png)

### Tipo I - Operações Aritméticas com imediato ou Desvio Condicional

![Representação](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/autodraw15_03_201923_31_12.png)

### Tipo J - Jump (Desvio incondicional)

![Representação](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/autodraw15_03_201923_32_46.png)

# 6. Procedimentos
Em resumo, quando mais de um trecho de código correm o risco de usar os mesmos registradores, surge a necessidade de padronizarmos este uso. E é assim que regras e convenções surgem quando falamos de procedimentos em Assembly.
Basicamente, precisamos:
- conhecer onde estarão os valores de **argumentos** e de **retorno**
- **guardar na Memória principal** informações que seriam substituídas caso ficassem nos registradores
E para que tudo isso dê certo, precisamos dos seguintes fatores.
## A) Convenções para os *donos* de cada registrador
Aqui vemos os 4 principais grupos de registradores: os *argumentos, retornos, registradores do "caller" e registradores do "callee"*.
![Representação](https://github.com/felipemnds/computer-science-notebook/blob/master/organizacao-arquitetura-computadores/whosaveswhat.png)
## B) Salvar na Memória Stack o que precisa ser salvo
Ao entrar e sair de um procedimento precisamos **alocar e desalocar o espaço necessário na stack**, respectivamente. E o processo funciona mais ou menos assim:
```
addi $sp, $sp, -4 # alocar uma palavra na Stack
sw $t0, 0($sp) # 'store' $t0 na memoria
lw $t0, 0($sp) # 'load' $t0 da memoria
addi $sp, $sp, 4 # desaloca a palavra alocada anteriormente
```
> Perceba: a Stack cresce de cima para baixo
## C) Usar *jal* e *jr $ra* para entrar e sair dos procedimentos
Ao usar o desvio incondicional ` jump `para ir até um procedimento, devemos usar os comandos corretos:
```
jal NomeProcedimento # desvia para o procedimento e guarda o endereço inicial $ra, para o retorno
jr $ra # já dentro do procedimento, vai diretamente para o endereço de $ra (endereço inicial do "Caller")
```
