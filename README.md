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
     dotnet new console -o FirstApp 
 ![1](https://user-images.githubusercontent.com/52087288/206786169-f1486f07-6e40-48f8-beaa-242949c1e0bd.PNG)

## Structure du projet
![image](https://user-images.githubusercontent.com/52087288/206785955-af633a87-5683-4a9a-a5a0-45800923193a.png)

## La création des classes
+ Account
  ```java
  public class Account
    {
        public int id { get; set; }
        public string? currency { get; set; }
        public double balance { get; set; }

        public Account(){}

        public Account(int id, string currency, double balance)
        {
            this.id = id;
            this.currency = currency;
            this.balance = balance;
        }

        public override string ToString()
        {
            return JsonSerializer.Serialize(this);
        }
    }
  ```
+ AccountService
  ```java
  public interface AccountService
    {
        Account GetAccountById(int id);
        void AddNewAccount(Account account1);
        List<Account> GetAllAccounts();
        Account UpdateAccount(Account account1);
        void DeleteAccount(int id);

        List<Account> GetDebitedAccounts();
        double balanceAVG();

     
    }
  ```
+ AccountServiceImpl
  ```java
  class AccountServiceImpl : AccountService
    {
        private Dictionary<int,Account> accounts = new Dictionary<int, Account>() ;

        public void DeleteAccount(int id)
        {
            Account account = GetAccount(id);
            accounts.Remove(account.id);
        }

        public List<Account> GetAllAccounts()
        {
            return accounts.Values.ToList();
        }

        public Account GetAccount(int id)
        {
            //return accounts.Find(account => account.id == id);
            return this.accounts[id];
    
        }

        public Account UpdateAccount(Account account1)
        {
            Account account = GetAccount(account1.id);
            account.balance = account1.balance;
            account.currency = account1.currency;
            return account;
        }

        public List<Account> GetDebitedAccounts()
        {
            return this.accounts.Values.Where(account => account.balance < 0).ToList();
        }

        public double balanceAVG()
        {
            return this.accounts.Values.Average(account => account.balance);
        }

        public Account GetAccountById(int id)
        {
            return accounts.Values.ToList().Find(account => account.id == id);
        }

        public void AddNewAccount(Account account1)
        {
            accounts.Add(account1.id,account1);
        }
    }
  ```

## Le test du programme
+ Main
 ```java
Console.WriteLine("Hello, World!");
Console.WriteLine("Test Dot Net core!");
Console.WriteLine("your name :");
String name = Console.ReadLine();
Console.WriteLine("Hello, " + name);

Account account = new Account(1, "USD", 18374);

Console.WriteLine(account.ToString());

AccountService accountService = new AccountServiceImpl();
accountService.AddNewAccount(account);
accountService.AddNewAccount(new Account(2, "EUR", 2000));
accountService.AddNewAccount(new Account(3, "MAD", 3276));
accountService.AddNewAccount(new Account(4, "MAD", 87976));
accountService.AddNewAccount(new Account(5, "USD", 62444));
accountService.AddNewAccount(new Account(6, "USD", 56456));
accountService.GetAllAccounts().ForEach(account => Console.WriteLine(account.ToString()));

accountService.GetDebitedAccounts().ForEach(account => Console.WriteLine(account.ToString()));

Console.WriteLine(accountService.balanceAVG());

Console.WriteLine(accountService.GetAccountById(1).ToString());

accountService.DeleteAccount(1);
accountService.GetAllAccounts().ForEach(account => Console.WriteLine(account.ToString()));
  ```
+ L'exécution

   ![image](https://user-images.githubusercontent.com/52087288/206788845-0162e208-eb86-400d-bf52-1c5439180bc4.png)

  
