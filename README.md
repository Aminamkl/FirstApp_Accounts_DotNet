# Partie 1 : Gestion des Comptes
 
## Introduction

Dans cette partie nous allons implementer une application DotNet Core de type console qui permet gérer des comptes, et nous allons essentiellement : 
   - Créer la classe Account(id, curency, balance)
   - Créer l'interface AccountService avec les opérations :
         . AddNewAccount
         . GetAllAccounts
         . GetAccountById
         . GetDebitedAccounts
         . GetBalanceAVG()
   - Créer une implémentation de cette interface utilisant une collection de type Dictionary
   - Tester l'application
   
 ## Création du projet
     + dotnet new console -o FirstApp 
 ![1](https://user-images.githubusercontent.com/52087288/206786169-f1486f07-6e40-48f8-beaa-242949c1e0bd.PNG)

## Structure du projet
![image](https://user-images.githubusercontent.com/52087288/206785955-af633a87-5683-4a9a-a5a0-45800923193a.png)


   
  
