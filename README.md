# Desafio 02
---
title: "Desafio 02"
author: "Manuella Kauany da S. D. Pereira, GRR20241403"
date: "2024-10-14"
output: html_document
---

# Gráfico Escolhido
## Grafico de Cascata ( Waterfall )

# Seção Explicativa
  O Gráfico de Cascata normalmente pode ser descrito como uma variação do gráfico de barras, sendo uma ferramenta ao qual demonstra atravéz do gráfico transições relacionadas ao conjunto de dados ultilizado, exibindo no final o resultado final dos dados.
  Sua formulação geral é composta por barras paralelas, em sua origem é apresentado uma barra com o valor base continuado por barras ao qual podem representar resultados positivos (subindo) ou resultados negativos (descendo). A representação visual deixa explicíto o processo,seja ele o aumento ou redução de valores,em que sucedeu o resultado final apresentado.
  A aplicação desse gráfico pode ser ultilizado em diversos setores, como na área de análise financeira ou relacionado a supervisão e tomada de decisões de projetos, estruturando demonstrações financeiras, realizando análises detalhadas de variações orçamentárias e na avaliação de despesas do projeto.

# Criar um gráfico com um conjunto de dados aleatórios
#### Um exemplo de Gráfico Cascata com um conjunto aleatório de dados, representando figuramente Vendas ao longo do 1 semestre.

![](https://drive.google.com/uc?id=17rfK2Cd1VbYubtabmsD2bO8NTYZGnikE)

## Nomeando Variáveis
categorias <- c("Janeiro", "Fevereiro", "Março", "Abril", "Maio", "Junho", "Total")
valores <- c(50, 30, -20, 40, -15, 35)

## Criar um vetor para armazenar os valores acumulados
### Cria vetor de zeros com comprimento igual ao número de valores + 1
valores_acumulados <- numeric(length(valores) + 1)
### Inicia em 0, para representar o ponto de partida
valores_acumulados[1] <- 0 

## Calculando os valores acumulados
for (i in 1:length(valores))
{valores_acumulados[i + 1] <-
  valores_acumulados[i] + valores[i]}

## Criando o gráfico de cascata
### Ajusta as margens do gráfico
par(mar = c(5, 4, 2, 2) + 0.1) 
### Ajusta o fundo do gráfico como cinza claro
par(bg = "lightgrey") 
### Cria o plot
#### type = "n"  cria um gráfico sem plotar os pontos ou as linhas,
#### xlab e ylab = adiciona os títulos dos eixos,
#### main = adiciona título principal
#### ylim = defini intervalo de valor que desejo que apareça
#### xaxt e yaxt = "n" deixa o eixo x sem nenhuma plotagem p´re estabelecida
plot(c(1:length(categorias)), valores_acumulados, 
     type = "n", xlab = "", ylab = "Vendas",
     main = "Gráfico de Cascata", ylim = c(min(valores_acumulados) - 20, max(valores_acumulados) + 20),
     xaxt = "n", yaxt = "n") 

## Adicionando as barras com alinhamento correto
for (i in 1:length(valores)) {
  if (i == 1) {
    # Para o primeiro mês, janeiro, a barra é azul
    rect(i - 0.5, valores_acumulados[i], i + 0.5, valores_acumulados[i + 1], 
         col = "blue", border = "black")}
  else {
    if (valores[i] >= 0) {
      # Para meses com valores positivos, as barras são verdes
      rect(i - 0.5, valores_acumulados[i], i + 0.5, valores_acumulados[i + 1], 
           col = "green", border = "black")}
    else {
      # Para meses com valores negativos, as barras são vermelhas
      rect(i - 0.5, valores_acumulados[i + 1], i + 0.5, valores_acumulados[i], 
           col = "red", border = "black") }}}

## Adicionando a barra total
### A barra total é azul e representa a soma total
rect(length(valores) + 0.5, 0, length(valores) + 1.5, valores_acumulados[length(valores_acumulados)], 
     col = "blue", border = "black") 

## Adicionando rótulos mostrados acima das barras
text(x = 1:length(categorias), y = valores_acumulados, 
     labels = ifelse(valores_acumulados != 0, valores_acumulados, ""), pos = 3, cex = 0.8) 

## Adicionando os nomes das categorias no eixo x
axis(1, at = 1:length(categorias), labels = categorias) 

## Adicionando o valor 0 colado na interseção dos eixos x e y
text(x = 0.5, y = -3, labels = "0", pos = 1, cex = 0.8)  

## Adicionando marcas no eixo y
axis(2, at = seq(min(valores_acumulados) - 20, max(valores_acumulados) + 20, by = 10)) 

## Desenha uma linha horizontal no valor 0
abline(h = 0, col = "black")  


*Referencias*
https://www.jaspersoft.com/pt-br/articles/what-is-a-waterfall-chart
