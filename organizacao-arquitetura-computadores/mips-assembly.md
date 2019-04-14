[< MENU](https://github.com/felipemnds/computer-science-notebook/blob/master/README.md)
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
![enter image description here](https://lh3.googleusercontent.com/qm3xYxQlMIhJHKeVMPeSA0yy7JuHxFBhy9iCdJlc3RX1EQJsCnNYA8SuT_jgCPTxbmfU1gvg9dZM)

## Register File
Aqui, temos **32 registradores de propósito geral**:
- R0...R31 (cada um tem 32 bits)
- valores de instruções precisam vir dos registradores
Temos alguns registradores especiais:
- R0 é sempre zero
- R29/R31 são usados para chamada de funções
- Hi & Lo guardam resultados de multiplicação

![enter image description here](https://lh3.googleusercontent.com/X3bCiqey-3vaEcBLt1T-83cNs2nWtNLR-WE_uvJGPNwuEopmO5gvOk8DYL1xoD8JourhI4nfMRIB)

# 3. Memória MIPS
MIPS é uma máquina *Register File* de *LOAD/STORE* (carregar/armazenar).
![enter image description here](https://lh3.googleusercontent.com/3zePqjPuqRXektIVAcl1egs-YD9PCDsAfSjcgnIDFW8W3_A3sCA24m3fVagf3gsFFi0PycfQsgGh)
Cada local na Memória MIPS tem largura de 8 bits (1 byte).

A Memória MIPS é indexada por seu endereço. Uma memória de 4GB por exemplo possui 2^32 locais.

![enter image description here](https://lh3.googleusercontent.com/6s8LE7m-9H6nv_gS3p6JsNwgPZIXMsmBK5trBVMYmQIxF3qtetT9YDhbiscucCgz5sgl-cPupwfy)

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

![enter image description here](https://lh3.googleusercontent.com/qG4GVQsos0FuZMNvGgh10Ash0HQkPoS4I5CfzDjYQIb-xzexU9T_DhOMDd6IbCLSbj4TBvsNt1aR)

### Tipo I - Operações Aritméticas com imediato ou Desvio Condicional

![enter image description here](https://lh3.googleusercontent.com/akYUT4yQPFVPxTDnxupZTq32QBKnJXN5R8D7j4nBSBy39sAS9aQpgEVGW0MYag5J-gV4qayILWN5)

### Tipo J - Jump (Desvio incondicional)

![enter image description here](https://lh3.googleusercontent.com/QpQyQgIPfDWyTbGUynEhCxAn5z2zocumj3l7EzaaRcB_p7gMAOOO3RpXC7USCJzFQrgzNnj72Mly)

# 6. Procedimentos
Em resumo, quando mais de um trecho de código correm o risco de usar os mesmos registradores, surge a necessidade de padronizarmos este uso. E é assim que regras e convenções surgem quando falamos de procedimentos em Assembly.
Basicamente, precisamos:
- conhecer onde estarão os valores de **argumentos** e de **retorno**
- **guardar na Memória principal** informações que seriam substituídas caso ficassem nos registradores
E para que tudo isso dê certo, precisamos dos seguintes fatores.
## A) Convenções para os *donos* de cada registrador
Aqui vemos os 4 principais grupos de registradores: os *argumentos, retornos, registradores do "caller" e registradores do "callee"*.
![enter image description here](https://lh3.googleusercontent.com/EwVqLeX93KYeu3_8RF6iOsEAhZst2f7QBzG4k08fS1s8ogUTqPKmZAM1Dg3ur1dYbX2vP95ldIgp)
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTQzMDg4NjA4LC0xMzk2ODIyNjY1XX0=
-->