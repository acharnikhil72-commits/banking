# banking
trying to do something in 1st sem
import java.util.Scanner;

class Account {
    String holderName;
    int accNumber;
    float balance;
    String accType; // SB, CURRENT, RD, FD
}

public class Banking {

    // Create account
    public static Account createAccount() {
        Scanner sc = new Scanner(System.in);
        Account acc = new Account();

        System.out.print("Enter Holder Name: ");
        acc.holderName = sc.nextLine();

        System.out.print("Enter Account Number: ");
        acc.accNumber = sc.nextInt();

        System.out.print("Enter Initial Balance: ");
        acc.balance = sc.nextFloat();
        sc.nextLine(); // consume newline

        System.out.print("Enter Account Type (SB/CURRENT/RD/FD): ");
        acc.accType = sc.nextLine();

        return acc;
    }

    // Display account details
    public static void displayAccount(Account acc) {
        System.out.println("Holder Name: " + acc.holderName);
        System.out.println("Account Number: " + acc.accNumber);
        System.out.println("Balance: " + acc.balance);
        System.out.println("Account Type: " + acc.accType);
    }

    // Credit amount
    public static Account creditAmount(Account acc, float amount) {
        acc.balance += amount;
        System.out.printf("Amount credited successfully! New Balance: %.2f\n", acc.balance);
        return acc;
    }

    // Debit amount
    public static Account debitAmount(Account acc, float amount) {
        if (acc.balance >= amount) {
            acc.balance -= amount;
            System.out.printf("Amount debited successfully! Remaining Balance: %.2f\n", acc.balance);
        } else {
            System.out.println("Insufficient funds!");
        }
        return acc;
    }

    // Recursive FD interest calculation
    public static float fdInterest(float amount, int years) {
        if (years == 0) return amount;
        return fdInterest(amount + (amount * 0.065f), years - 1);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Account acc = createAccount();
        int choice;

        do {
            System.out.println("\n--- Banking Menu ---");
            System.out.println("1. Display Account");
            System.out.println("2. Credit Amount");
            System.out.println("3. Debit Amount");
            System.out.println("4. FD Interest Calculation");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    displayAccount(acc);
                    break;
                case 2:
                    System.out.print("Enter amount to credit: ");
                    float creditAmt = sc.nextFloat();
                    acc = creditAmount(acc, creditAmt);
                    break;
                case 3:
                    System.out.print("Enter amount to debit: ");
                    float debitAmt = sc.nextFloat();
                    acc = debitAmount(acc, debitAmt);
                    break;
                case 4:
                    if (acc.accType.equalsIgnoreCase("FD")) {
                        System.out.print("Enter number of years: ");
                        int years = sc.nextInt();
                        float finalAmount = fdInterest(acc.balance, years);
                        System.out.printf("Final amount after %d years with 6.5%% interest: %.2f\n", years, finalAmount);
                    } else {
                        System.out.println("Interest calculation only for FD accounts!");
                    }
                    break;
                case 5:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice!");
            }
        } while (choice != 5);
    }
}
