OnlineBankingSystem
===================

An Online Banking System created using multithreading where multiple transaction takes place in a synchronized way.

InternateBankingSystem Class
============================
package internatebankingsystem;

  public class InternateBankingSystem
   {
      public static void main(String[] args) 
      {
          Account accountObj; 
          accountObject = new Account(100);
             new Thread(new DepositThread(accountObj,130)).start();
             new Thread(new DepositThread(accountObj,210)).start();
             new Thread(new DepositThread(accountObj,310)).start();
             new Thread(new WithdrawThread(accountObj,130)).start();
             new Thread(new WithdrawThread(accountObj,150)).start();
             new Thread(new WithdrawThread(accountObj,120)).start();
      }
  }


Account Class
==============
package internatebankingsystem;
     public class Account 
     {
         private double balance = 0;
         public Account(double balance)
           {
               this.balance = balance;
           }
         // if the keyword ‘synchronized’ is removed, the outcome will be  unpredictable
     
         public synchronized void deposit(double amount) 
         {
           if (amount < 0) 
             {
               throw new IllegalArgumentException("Can’t deposit.");
             }
              this. balance += amount;
              System.out.println(" Deposit " + amount + " in thread  " + Thread.currentThread().getId() + ", balance is               "+balance);
         }
         // if the keyword ‘synchronized’ is removed, the outcome will be  unpredictable
         public synchronized void withdraw(double amount) 
         {
           if (amount < 0 || amount > this.balance) 
             {
                throw new IllegalArgumentException("Can’t withdraw.");
             }
               this.balance -= amount;
               System.out.println(" Withdraw  " + amount +" in thread " + Thread.currentThread().getId() + ", balance is                "+balance);
         }
     }//End of Account class


DepositeThread Class
====================
package internatebankingsystem;
     public class DepositThread implements Runnable 
     {
         private Account account;
         private double amount;
         public DepositThread(Account account, double amount) 
         {
             this.account = account;
             this.amount = amount;
         }
         public void run()
         {
         //make a deposit
              account.deposit(amount);
         }
     }//End of DepositeThread Class

WithdrawThread Class
====================
package internatebankingsystem;
     public class WithdrawThread implements Runnable 
     {
         private Account account;
         private double amount;
         public WithdrawThread(Account account, double amount) 
           {
             this.account = account;
             this.amount = amount;
           }
         public void run() 
           {
           //make a withdraw 
             account.withdraw(amount);
           }
     }//End of  WithdrawThread class



