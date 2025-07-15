import java.util.HashMap;
import java.util.Scanner;

public class BankingSystem {
   static Scanner sc;
   static HashMap<String, Customer> customers;

   public BankingSystem() {
   }

   public static void main(String[] var0) {
      while(true) {
         System.out.println("\n===== Banking System =====");
         System.out.println("1. Create customer");
         System.out.println("2. Deposit");
         System.out.println("3. Withdraw");
         System.out.println("4. Transfer");
         System.out.println("5. View balance");
         System.out.println("6. View transactions");
         System.out.println("7. Exit");
         System.out.print("Choose option: ");
         int var1 = sc.nextInt();
         sc.nextLine();
         switch (var1) {
            case 1:
               createCustomer();
               break;
            case 2:
               depositMoney();
               break;
            case 3:
               withdrawMoney();
               break;
            case 4:
               transferMoney();
               break;
            case 5:
               viewBalance();
               break;
            case 6:
               viewTransactions();
               break;
            case 7:
               System.out.println("Thank you for using the banking system.");
               return;
            default:
               System.out.println("Invalid option.");
         }
      }
   }

   static void createCustomer() {
      System.out.print("Enter customer ID: ");
      String var0 = sc.nextLine();
      System.out.print("Enter customer name: ");
      String var1 = sc.nextLine();
      System.out.print("Enter account number: ");
      String var2 = sc.nextLine();
      Customer var3 = new Customer(var1, var0, var2);
      customers.put(var0, var3);
      System.out.println("Customer created successfully!");
   }

   static Customer getCustomer() {
      System.out.print("Enter customer ID: ");
      String var0 = sc.nextLine();
      if (customers.containsKey(var0)) {
         return (Customer)customers.get(var0);
      } else {
         System.out.println("Customer not found.");
         return null;
      }
   }

   static void depositMoney() {
      Customer var0 = getCustomer();
      if (var0 != null) {
         System.out.print("Enter amount to deposit: ₹");
         double var1 = sc.nextDouble();
         sc.nextLine();
         var0.account.deposit(var1);
         System.out.println("Amount deposited successfully.");
      }

   }

   static void withdrawMoney() {
      Customer var0 = getCustomer();
      if (var0 != null) {
         System.out.print("Enter amount to withdraw: ₹");
         double var1 = sc.nextDouble();
         sc.nextLine();
         if (var0.account.withdraw(var1)) {
            System.out.println("Amount withdrawn successfully.");
         } else {
            System.out.println("Insufficient balance.");
         }
      }

   }

   static void transferMoney() {
      System.out.println("Sender details:");
      Customer var0 = getCustomer();
      if (var0 != null) {
         System.out.println("Receiver details:");
         Customer var1 = getCustomer();
         if (var1 != null) {
            System.out.print("Enter amount to transfer: ₹");
            double var2 = sc.nextDouble();
            sc.nextLine();
            if (var0.account.transfer(var1.account, var2)) {
               System.out.println("Transfer successful.");
            } else {
               System.out.println("Transfer failed due to insufficient balance.");
            }

         }
      }
   }

   static void viewBalance() {
      Customer var0 = getCustomer();
      if (var0 != null) {
         var0.displayInfo();
      }

   }

   static void viewTransactions() {
      Customer var0 = getCustomer();
      if (var0 != null) {
         var0.account.showTransactions();
      }

   }

   static {
      sc = new Scanner(System.in);
      customers = new HashMap();
   }
}
