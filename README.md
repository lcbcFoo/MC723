# Relatório exercício 1

## Compilações com apenas um arquivo primo.c
Foram feitas as seguintes compilações, acompanhadas dos respectivos resultados usando o comando `time` nos computadores da sala cc03 do IC3.
* `gcc primo.c -o primo`
```
real	0m0.293s
user	0m0.292s
sys	0m0.000s
```
* `gcc primo.c -o primo -O0`
```
real	0m0.298s
user	0m0.296s
sys	0m0.001s
```
* `gcc primo.c -o primo -O1`
```
real	0m0.265s
user	0m0.263s
sys	0m0.001s
```
* `gcc primo.c -o primo -O2`
```
real	0m0.297s
user	0m0.297s
sys	0m0.000s
```
* `gcc primo.c -o primo -O3`
```
real	0m0.295s
user	0m0.291s
sys	0m0.003s
```
* `gcc primo.c -o primo -mtune=intel`
```
real	0m0.295s
user	0m0.291s
sys	0m0.003s
```

É possível ver que o melhor tempo foi obtido com a compilação utilizando `-O1`, embora esperássemos que as flags de maiores otimizações como `-O3` e `-mtune=intel` apresentariam melhores resultados. Isso provavelmente se deve as características do código que não tornam as otimizações do gcc tão eficientes quanto deveriam. 

## Compilações com dois arquivos `main.c` e `primo.c`
Foram feitas as seguintes compilações, acompanhadas dos respectivos resultados usando o comando `time` nos computadores da sala cc03 do IC3.
O processo de compilação foi automatizado com o uso de um Makefile.
* Flag `-O0`
```
real	0m0.285s
user	0m0.285s
sys	0m0.000s
```
* Flag `-O1`
```
real	0m0.255s
user	0m0.255s
sys	0m0.000s
```
* Flag `-O2`
```
real	0m0.260s
user	0m0.258s
sys	0m0.001s
```
* Flag `-O3`
```
real	0m0.259s
user	0m0.258s
sys	0m0.001s
```
* Flag `-mtune=intel -01` (melhor resultado com mtune)
```
real	0m0.279s
user	0m0.278s
sys	0m0.001s
```
Novamente, o melhor resultado foi obtido com a flag `-O1`, embora esperássemos que fosse com o conjunto `-O3 -mtune=intel`. Por outro lado, a diferença de desempenho para as diferentes flags caiu em relação a quando tínhamos apenas um arquivo, isso indica que a separação das funções pode ter influenciado na otimização do gcc.

## Utilizando o mesmo algoritmo para calcular quantos primos existem entre 1 e n, testando de 1 em 1 (testes com n = 100000)
- Utilizando 2 arquivos, `main.c` e `calc_primo.c`, foram obtidos os resultados:
* Flag `-O0`
```
real	0m1.217s
user	0m1.215s
sys	0m0.001s
```
* Flag `-O1`
```
real	0m1.094s
user	0m1.092s
sys	0m0.001s
```
* Flag `-O2`
```
real	0m1.096s
user	0m1.093s
sys	0m0.002s
```
* Flag `-O3`
```
real	0m1.093s
user	0m1.092s
sys	0m0.000s
```
* Flag `-mtune=intel -00` (melhor resultado com mtune)
```
real	0m1.225s
user	0m1.222s
sys	0m0.001s
```

- Utilizando apenas 1 arquivo, `main.c`, foram obtidos os resultados:
* Flag `-O0`
```
real	0m1.215s
user	0m1.213s
sys	0m0.001s
```
* Flag `-O1`
```
real	0m1.096s
user	0m1.092s
sys	0m0.001s
```
* Flag `-O2`
```
real	0m1.096s
user	0m1.093s
sys	0m0.002s
```
* Flag `-O3`
```
real	0m1.096s
user	0m1.094s
sys	0m0.001s
```
* Flag `-mtune=intel -00` (melhor resultado com mtune)
```
real	0m1.218s
user	0m1.215s
sys	0m0.001s
```
Nesse conjunto de testes, vemos que os reultados obtidos com as flags `-O3` foram o melhores, porém as demais flags `-O1` e `-O2`conseguiram resultados bem parecidos. A flag `-mtune`, por outro lado, novamente piorou os resultados. Em relação aos arquivos estarem separados ou não, desta vez os resultados foram próximos o suficiente para supormos que isto não afetou significativamente o desempenho. 
