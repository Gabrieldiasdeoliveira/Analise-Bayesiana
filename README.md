# Analise-Bayesiana
Simulação Estocástica com R

install.packages("expm")
install.packages("markovchain")
install.packages("diagram")
install.packages("pracma")

library("expm")
library("markovchain")
library("diagram")
library("pracma")

# Matriz de transição

nomes <- c("Centro","Orla","Parque")
byrow <- TRUE
matrizTransicao <- matrix(data = c(0.95, 0.03, 0.02,
                                   0.02, 0.90, 0.08,
                                   0.05, 0.05, 0.90), byrow = byrow, nrow = 3,
                          dimnames = list(nomes, nomes))
matrizTransicao

estadosIniciais <- c(0.5, 0.3, 0.2)
estadosIniciais                         

# Diagrama
plotmat(
  A = matrizTransicao, 
  pos = c(1, 2), 
  lwd = 1, 
  box.lwd = 2, 
  cex.txt = 0.8, 
  box.size = 0.1, 
  box.type = "circle", 
  box.prop = 0.5,
  box.col = "light yellow",
  arr.length = 0.1,
  arr.width = 0.1,
  self.cex = 0.4,
  self.shifty = -0.01,
  self.shiftx = 0.13,
  main = "Retiradas e Devoluções"
)

# Cadeia de Markov
cadeiaMarkov <-new("markovchain", states = nomes, byrow = byrow, transitionMatrix = matrizTransicao, name = "Modelo:")
cadeiaMarkov

defaultMc <- new("markovchain")
defaultMc

mcList <- new("markovchainList", markovchains = list(cadeiaMarkov, defaultMc), name = "Lista da Cadeia de Markov")
mcList

# Executando a cadeia de Markov
apos2Dias <- estadosIniciais * (cadeiaMarkov^2)
apos3Dias <- estadosIniciais * (cadeiaMarkov^3)
apos4Dias <- estadosIniciais * (cadeiaMarkov^4)
apos5Dias <- estadosIniciais * (cadeiaMarkov^5)
apos6Dias <- estadosIniciais * (cadeiaMarkov^6)
apos7Dias <- estadosIniciais * (cadeiaMarkov^7)

semana <- c("D2","D3","D4","D5","D6","D7")
Prob <- matrix(data = c(apos2Dias,apos3Dias,apos4Dias,apos5Dias,apos6Dias,apos7Dias), byrow = byrow, nrow = 6,dimnames = list(semana,nomes))
Prob

