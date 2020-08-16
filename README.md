# GuiaHTML

#TAREA NUMERO 3
#Paulina Aguilera Madrid
######################Letra A##################################
#La diferencia de este tag "img" con los demas, es que este no necesita un cierre.


#######################Letra B#################################
#Borrar variables

rm(list=ls())

#Cargar librerias
library(rvest)
library(xml2)

readHtml <- read_html("tarea_3_guiahtml.html")
print(readHtml)

#Extraccion de la noticia

extraccionNoticia <- html_nodes(readHtml,".justificado")
print(extraccionNoticia)
extraccionNoticia <- html_text(extraccionNoticia)
print(extraccionNoticia)

#Eliminacion de caracteres raros

extraccionNoticia <- gsub("\r\n","",extraccionNoticia)
extraccionNoticia <- gsub("\r\n\r\n","",extraccionNoticia)
extraccionNoticia <- gsub("\\n","",extraccionNoticia)
extraccionNoticia <- gsub("\\r","",extraccionNoticia)
extraccionNoticia <- gsub("[.]","",extraccionNoticia)
extraccionNoticia <- gsub("[,]","",extraccionNoticia)
extraccionNoticia <- gsub("[-]","",extraccionNoticia)
extraccionNoticia <- gsub("[()]","",extraccionNoticia)

print(extraccionNoticia)

#Llevar todas las palabras a minuscula

extraccionNoticia <- tolower(extraccionNoticia)
print(extraccionNoticia)

#Separar palabras y almacenarlas en una lista

separarPalabras <- strsplit(extraccionNoticia," "[[1]])
print(separarPalabras)

listaDePalabras <- as.list(separarPalabras)
print(listaDePalabras)

#Calcular repeticion de cada palabra con FOR

repeticionDePalabras <- table(listaDePalabras)
print(repeticionDePalabras)
View(repeticionDePalabras)

#######################Letra C################################

#Extraer datos de la tabla

tablaEditor <-html_nodes(readHtml,".tabla > table")
print(tablaEditor)
tablaLimpia <- html_table(tablaEditor)
print(tablaLimpia)
tablaLimpia <- tablaLimpia[[1]]
print(tablaLimpia)

View(tablaLimpia)

#Extraer datos de precios de la tabla

print(tablaLimpia[[2]])
precios <- gsub("[.]","",tablaLimpia[[2]])
print(precios)
precios <- gsub("\\$","",precios)
print(precios)
precios <- as.numeric(precios)
print(precios)

#Calculo de promedio y mediana a traves de FOR

contarPrecios <- 0

for(preciosTabla in 1:length(precios)){
  contarPrecios <- contarPrecios + precios[preciosTabla]
}

promedioPrecios <- contarPrecios/length(contarPrecios)
print(paste("El promedio de los precios de la lista de compras es:", promedioPrecios))
medianaPrecios <- median(precios)
print(paste("La mediana de los precios de la lista de compras es:", medianaPrecios))

