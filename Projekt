import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Random;
import java.util.Scanner;
import java.util.Set;

public class Main {
    private static List<Expense> expenseList = new ArrayList();
    private static Map<String, Double> categoryTotals = new HashMap();
    private static Set<String> categories = new HashSet(Arrays.asList(

            "Jedzenie", "Transport", "Opłata parkingowa", "Usługi komunalne", "Inne", "Rozrywka",
            "Zdrowie", "Edukacja", "Zakupy", "Podróże", "Sport", "Prezenty", "Subskrypcje", "Hobby", "Naprawy"));

    public Main() {
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean running = true;

        while(running) {
            System.out.println("\ncopywriter: Kamil Gruchot");
            System.out.println("\nMenu śledzenia wydatków:");
            System.out.println("1. Dodaj wydatek");
            System.out.println("2. Zobacz wszystkie wydatki");
            System.out.println("3. Wyświetl sumę według kategorii");
            System.out.println("4. Generowanie losowych wydatków");
            System.out.println("5. Wyjście");
            System.out.print("Wybierz opcję: ");
            int choice = scanner.nextInt();
            scanner.nextLine();
            switch (choice) {
                case 1:
                    addExpense(scanner);
                    break;
                case 2:
                    viewExpenses();
                    break;
                case 3:
                    viewCategoryTotals();
                    break;
                case 4:
                    generateRandomExpenses();
                    break;
                case 5:
                    running = false;
                    break;
                default:
                    System.out.println("Nieprawidłowy wybór. Spróbuj ponownie.");
            }
        }

        System.out.println("Dziękuje za wybór mojej aplikacji!");
    }

    private static void addExpense(Scanner scanner) {
        System.out.print("Wprowadź datę (YYYY-MM-DD): ");
        String dateInput = scanner.nextLine();
        LocalDate date = LocalDate.parse(dateInput);
        System.out.print("Wprowadź kwotę: ");
        double amount = scanner.nextDouble();
        scanner.nextLine();
        System.out.print("Wprowadź kategorię (" + String.join(", ", categories) + "): ");
        String category = scanner.nextLine();
        if (!categories.contains(category)) {
            System.out.println("Nieprawidłowa kategoria. Wydatek nie został dodany.");
        } else {
            Expense expense = new Expense(date, amount, category);
            expenseList.add(expense);
            categoryTotals.put(category, (Double)categoryTotals.getOrDefault(category, (double)0.0F) + amount);
            System.out.println("\n--------------------------------------");
            System.out.println("Wydatek dodany poprawnie!");
            System.out.println("Twój nowy wydatek to:\n" + String.valueOf(expense));
            System.out.println("--------------------------------------");
        }
    }

    private static void viewExpenses() {
        if (expenseList.isEmpty()) {
            System.out.println("Nie odnotowano żadnych wydatków.");
        } else {
            System.out.println("\nWszystkie wydatki:");

            for(Expense expense : expenseList) {
                System.out.println(expense);
            }

        }
    }

    private static void viewCategoryTotals() {
        if (categoryTotals.isEmpty()) {
            System.out.println("Nie odnotowano żadnych wydatków.");
        } else {
            System.out.println("\nŁącznie według kategorii:");

            for(Map.Entry<String, Double> entry : categoryTotals.entrySet()) {
                System.out.printf("%s: %.2f\n", entry.getKey(), entry.getValue());
            }

        }
    }

    private static void generateRandomExpenses() {
        Random random = new Random();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");

        for(int i = 0; i < 5; ++i) {
            LocalDate randomDate = LocalDate.now().minusDays((long)random.nextInt(30));
            double randomAmount = (double)10.0F + (double)90.0F * random.nextDouble();
            String randomCategory = (String)(new ArrayList(categories)).get(random.nextInt(categories.size()));
            Expense expense = new Expense(randomDate, randomAmount, randomCategory);
            expenseList.add(expense);
            categoryTotals.put(randomCategory, (Double)categoryTotals.getOrDefault(randomCategory, (double)0.0F) + randomAmount);
        }

        System.out.println("5 losowych wydatków wygenerowanych pomyślnie!");
    }

    static class Expense {
        private LocalDate date;
        private double amount;
        private String category;

        public Expense(LocalDate date, double amount, String category) {
            this.date = date;
            this.amount = amount;
            this.category = category;
        }

        public String toString() {
            return String.format("Data: %s, Kwota: %.2f, Kategoria: %s", this.date, this.amount, this.category);
        }
    }
}
