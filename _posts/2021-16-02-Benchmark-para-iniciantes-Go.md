---
layout: post
title:  Benchmark para iniciantes - Go
date:   2021-02-16 15:01:35 +0300
image:  '../images/post-benchmark.jpeg'
tags:   [Go, Tecnologia]
author: 
    name: Bella Souzas
    image: '../images/bella-perfil.jpeg'
---
Eu sempre ouvi sobre benchmark nos meetups, nas lives, nas discussões, mas eu achava que seria algo tão dificil que só poderia estudar quando eu estivesse bem mais avançada na linguagem. Sim, estudar testes tem sido um desafio grande, mas lendo alguns artigos, documentação da linguagem me surpreendeu sobre a implementação.

O benchmark é uma ferramenta incrível que o pacote testing oferece aos gophers. O benchmark é uma ferramenta de analise do desempenho do seu código em GO.

Para implementar uma função benchmark não tem mistério e pode orientar a você sobre como seu código vai performando ainda em execução.

ok, ok, chega de teoria e vamos para a prática…

Para implementar o benchmark vou usar como base a função Repeat que está salva no arquivo repeat.go.

~~~golang
package interation
 
const repeatCount = 5
 
// Repeat returns character repeated 5 times.
func Repeat(character string) string {
  var repeated string
  for i := 0; i < repeatCount; i++ {
     repeated += character
  }
  return repeated
}
 ~~~


No arquivo repeat_test.go eu implemento o teste da função e o  benchmark usando o pacote  [“testing”](https://golang.org/pkg/testing/ ).

~~~golang 
package interation
 
import (
  "testing"
 
)
 
func TestRepeat(t *testing.T) {
  repeated := Repeat("a")
  expected := "aaaaa"
 
  if repeated != expected {
     t.Errorf("expected %q but got %q", expected, repeated)
  }
}
 
func BenchmarkRepeat(b *testing.B) {
  for i := 0; i < b.N; i++ {
     Repeat("a")
  }
}
 
~~~
`

Para “rodar” o test benchmark basta chamar em seu terminal ` go test -bench=` ou ‘go test -bench="." ’ , caso voce esteja usando o windowns powershell.

No meu computador o resultado foi :

~~~
goarch: amd64
pkg: github.com/bellasouza/GOWithTest/interations
BenchmarkRepeat
BenchmarkRepeat-4   	 4988276	       211 ns/op
PASS

Process finished with exit code 0
~~~ 

Esse resultado significa que a minha função leva em média 211 nanosegundos para rodar 4988276 vezes a função.


---


### Considerações: <h3>
Esses são os materiais valiosíssimos que me ajudaram a entender melhor sobre benchmark.
Super indico a leitura:

* https://golang.org/pkg/testing/
* https://quii.gitbook.io/learn-go-with-tests/go-fundamentals/iteration
* https://dave.cheney.net/2013/06/30/how-to-write-benchmarks-in-go


