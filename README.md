# Relatório exercício 1
Todas as medias de tempo foram feitas utilizando o comando `time` nos computadores da sala cc03 do IC3.
## Compilações com apenas um arquivo primo.c
Foram feitas compilações com as flags:
```
* Flag -O0
real	0m0.298s
* Flag -O1
real	0m0.265s
* Flag -O2
real	0m0.297s
* Flag -O3
real	0m0.295s
* Flag -mtune=intel
real	0m0.295s
```
É possível ver que o melhor tempo foi obtido com a compilação utilizando `-O1`, embora esperássemos que as flags de maiores otimizações como `-O3` e `-mtune=intel` apresentariam melhores resultados. Isso provavelmente se deve as características do código que não tornam as otimizações do gcc tão eficientes quanto deveriam. 

## Compilações com dois arquivos `main.c` e `primo.c`
O processo de compilação foi automatizado com o uso de um Makefile. Foram feitas compilações com as flags:
```
* Flag `-O0`
real	0m0.285s
* Flag `-O1`
real	0m0.255s
* Flag `-O2`
real	0m0.260s
* Flag `-O3`
real	0m0.259s
* Flag `-mtune=intel -01` (melhor resultado com mtune)
real	0m0.279s
```
Novamente, o melhor resultado foi obtido com a flag `-O1`, embora esperássemos que fosse com o conjunto `-O3 -mtune=intel`. Por outro lado, a diferença de desempenho para as diferentes flags caiu em relação a quando tínhamos apenas um arquivo, isso indica que a separação das funções pode ter influenciado na otimização do gcc.

## Utilizando o mesmo algoritmo para calcular quantos primos existem entre 1 e n, testando de 1 em 1 (testes com n = 100000)
- Em relação aos arquivos estarem separados ou não, desta vez os resultados foram próximos o suficiente para supormos que isto não afetou significativamente o desempenho, de forma que aqui estão representados apenas os resultados utilizando 2 arquivos, `main.c` e `calc_primo.c`:
```
* Flag `-O0`
real	0m1.217s
* Flag `-O1`
real	0m1.094s
* Flag `-O2`
real	0m1.096s
* Flag `-O3`
real	0m1.093s
* Flag `-mtune=intel -00` (melhor resultado com mtune)
real	0m1.225s
```
Nesse conjunto de testes, vemos que os reultados obtidos com as flags `-O3` foram o melhores, porém as demais flags `-O1` e `-O2` conseguiram resultados bem parecidos. A flag `-mtune`, por outro lado, novamente piorou os resultados, indicando que esta otimização não é boa para esse tipo de algoritmo. 

## Utilizando o mesmo algoritmo para calcular quantos primos existem entre 1 e n, testando apenas ímpares (testes com n = 100000)
- Em relação aos arquivos estarem separados ou não, desta vez os resultados foram próximos o suficiente para supormos que isto não afetou significativamente o desempenho, de forma que aqui estão representados apenas os resultados utilizando 2 arquivos, `main.c` e `calc_primo.c`:
```
* Flag `-O0`
real	0m0.836s
* Flag `-O1`
real	0m0.782s
* Flag `-O2`
real	0m0.787s
* Flag `-O3`
real	0m0.785s
* Flag `-mtune=intel -00` (melhor resultado com mtune)
real	0m0.819s
```
Novamente, as flags `-O1`, `-O2` e `-O3` obtiveram os melhores desempenhos ao passo que `-mtune=intel` não foi tão efetiva.

## Análise
Utilizando o gprof, foi possível notar que, em média, 96.2% do tempo de execução do programa da etapa anterior (contar primos de 1 a n, contando apenas ímpares) é gasto na função que verifica se o número é primo. Dessa forma, essa é a melhor parte do código a ser paralelizada e otimizada. Mesmo com diversas otimizações de paralelização e de compilação, o desempenho desse programa ainda será limitado pelo algoritmo imprementado, que é extremamente ineficiente. 
Podemos concluir, então, que o desempenho de um programa é afetado por ferramentas de compilação e paralelismo, mas ainda é essencial que o algoritmo implementado seja eficiente, já que este determinará a ordem de grandeza da quantidade de instruções a serem executadas enquanto que as demais otimizações são capazes apenas de diminuir algumas constantes da ordem de grandeza do algoritmo.
