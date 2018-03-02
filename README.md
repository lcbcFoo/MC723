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

É possível ver que o melhor tempo foi obtido com a compilação utilizando `-O1`, embora esperássemos que as flags de maiores otimizações como `-O3` e `-mtune=intel` apresentariam melhores resultados. 

## Compilações com dois arquivos `main.c` e `primo.c`
Foram feitas as seguintes compilações, acompanhadas dos respectivos resultados usando o comando `time` nos computadores da sala cc03 do IC3.
O processo de compilação foi automatizado com o uso de um Makefile.
