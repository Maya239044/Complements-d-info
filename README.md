# Complements-d-info
# -*- coding: utf-8 -*-

from MaBase_MIB import *

### Question 1 : quel est l'ensemble des gardiens?
les_gardiens = {gardien.Nom for gardien in BaseGardiens}

### Question 2: Les villes d'origine des agents:
les_villes_agents = {agent.Ville for agent in BaseAgents}

### Question 3: Ensemble des triplets (n° cabine, alien, gardien) pour chaque cabine:
triples = { (alien.NoCabine, alien.Nom, gardien.Nom) for alien in BaseAliens  for gardien in BaseGardiens if gardien.NoCabine == alien.NoCabine}

### Question 4: Ensemble couples (alien, allée) pour chaque alien:
couples = { (alien.Nom, cabine.NoAllee) for alien in BaseAliens for cabine in BaseCabines if alien.NoCabine == cabine.NoCabine}

### Question 5: Ensemble des aliens de l'allée 2:
allée2 = { (alien.Nom, cabine.NoAllee) for alien in BaseAliens for cabine in BaseCabines if alien.NoCabine == cabine.NoCabine and cabine.NoAllee == '2'}

### Question 6: l'ensemble de toutes les planètes dont sont originaires les aliens habitant une cellule de numéro pair:
planetepaire ={(Alien.Planete) for Alien in BaseAliens if Alien.NoCabine == '2'or'4'or'6'or'8'}

### Question 7: L'ensemble des aliens dont les gardiens sont originaires de Terminus:
Terminus = {(Alien.Nom) for Agent in BaseAgents for Gardien in BaseGardiens for Alien in BaseAliens if Agent.Ville == 'Terminus' if Agent.Nom == Gardien.Nom if Gardien.NoCabine == Alien.NoCabine}

### Question 8 : Quel est l'ensemble des gardiens des aliens féminins qui mangent du bortsch?
q8={ (gardien.Nom) for gardien in BaseGardiens for alien in BaseAliens for miam in BaseMiams if miam.Aliment=='Bortsch' and miam.NomAlien==alien.Nom and alien.Sexe=='F' and alien.NoCabine==gardien.NoCabine }


### Question 9 : Quel est l'ensemble des cabines dont les gardiens sont originaires de Terminus ou dont les aliens sont des filles?
q9={ (cabine.NoCabine) for cabine in BaseCabines for gardien in BaseGardiens for alien in BaseAliens for agent in BaseAgents if (gardien.Nom==agent.Nom and agent.Ville=='Terminus' and gardien.NoCabine==cabine.NoCabine) or (alien.Sexe=='F' and alien.NoCabine==cabine.NoCabine) }

### Question 10 : Y a-t-il des aliments qui commencent par la même lettre que le nom du gardien qui surveille l'alien qui les mange ?
q10={ (gardien.Nom,miam.Aliment) for gardien in BaseGardiens for miam in BaseMiams for alien in BaseAliens if miam.NomAlien==alien.Nom and alien.NoCabine==gardien.NoCabine and miam.Aliment[0]==gardien.Nom[0] }

### Question 11 : Y a-t-il des aliens originaires d'Euterpe ?
q11={ (alien.Nom) for alien in BaseAliens if alien.Planete=='Euterpe' }

### Question 12: est-ce que tous les aliments ont un "x" dans leur nom?
#xna = si il y a un x dans tout les noms des aliens

xna = {(Alien.Nom) for Alien in BaseAliens if 'x' in Alien.Nom }
an = 'Alien.Nom'
k = an.count('x')
if (k==9):
    print("12) tout les aliens ont des x dans leur noms",xna)

else :
    print("12) tout les aliens n'ont pas de x dans leur noms, voici ceux qui en ont :", xna)

### Question 13: Est-ce que tous les aliens qui ont un "x" dans leur nom on tun gardien qui vient de Terminus?
#agt = alien qui ont un x dans leur nom et dont le gardien viens de terminus

agt = {(Alien.Nom, Agent.Nom) for Alien in BaseAliens for Gardien in BaseGardiens for Agent in BaseAgents if 'x' in Alien.Nom if Agent.Ville == 'Terminus' if Agent.Nom == Gardien.Nom if Gardien.NoCabine == Alien.NoCabine}

if (xna == agt):
    print("13) tout les aliens qui ont un x dans leur nom ont des gardiens qui viennent de Terminus, les voici :", agt)
else :
    print("13) tout les aliens qui ont un x dans leur nom n'ont pas des gardiens venant de Terminus, les voici :", agt)


### Question 14: Existe-t-il un alien masculin originaire de Trantor qui mange du Bortsch ou dont le gardien vient de Terminus? 
#zy = alien masculin originaire de Trantor qui mange du bortsch
#zz = alien masculin originaire de Trantor qui a un gardien venant de terminus

zy = {(Alien.Nom) for Alien in BaseAliens for Miam in BaseMiams if Alien.Sexe == 'M' if Alien.Planete == 'Trantor' if Alien.Nom == Miam.NomAlien if Miam.Aliment == 'Bortsch'}
zz = {(Alien.Nom) for Alien in BaseAliens for Gardien in BaseGardiens for Agent in BaseAgents if Alien.Sexe == 'M' if Alien.Planete == 'Trantor' if Alien.NoCabine == Gardien.NoCabine if Gardien.Nom == Agent.Nom if Agent.Ville == 'Terminus'}

if (zy == zz) :
    print ("14) il(s) existe(s) un alien(s) masculin originaire de Trantor qui mange du Bortsch ou dont le gardien vient de Termnius, le(s) voici :", zz)
else :
    print ("14) il existe un alien masculin originaire de Trantor qui mange du Bortsch ou dont le gardien vient de Terrminus, le voici :",
    zy, zz)

