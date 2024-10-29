import java.util.Random;
import java.util.Scanner;

public class NumberGuessingGame {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        int score = 0;
        int rounds = 0;
        String playAgain;

        System.out.println("Welcome to the Number Guessing Game!");

        do {
            rounds++;
            System.out.println("\n--- Round " + rounds + " ---");

            // Generate a random number between 1 and 100
            int targetNumber = random.nextInt(100) + 1;
            int maxAttempts = 7;
            int attempts = 0;
            boolean guessedCorrectly = false;

            while (attempts < maxAttempts && !guessedCorrectly) {
                System.out.print("Attempt " + (attempts + 1) + "/" + maxAttempts + ". Enter your guess (1-100): ");
                
                // Validate input is an integer
                while (!scanner.hasNextInt()) {
                    System.out.print("Invalid input. Please enter a number between 1 and 100: ");
                    scanner.next();  // Clear invalid input
                }

                int guess = scanner.nextInt();
                attempts++;

                // Check if guess is within range
                if (guess < 1 || guess > 100) {
                    System.out.println("Please guess a number within the range of 1 to 100.");
                    continue;
                }

                // Compare the guess with the target number
                if (guess == targetNumber) {
                    System.out.println("Congratulations! You've guessed the correct number!");
                    guessedCorrectly = true;
                    score += maxAttempts - attempts + 1;  // Higher score for fewer attempts
                } else if (guess < targetNumber) {
                    System.out.println("Your guess is too low. Try again.");
                } else {
                    System.out.println("Your guess is too high. Try again.");
                }
            }

            if (!guessedCorrectly) {
                System.out.println("Sorry, you've used all attempts. The correct number was " + targetNumber + ".");
            }

            // Show the user's current score
            System.out.println("Score after round " + rounds + ": " + score);

            // Ask if they want to play another round
            System.out.print("Do you want to play another round? (y/n): ");
            playAgain = scanner.next();

        } while (playAgain.equalsIgnoreCase("y"));

        // Display the final score and total rounds played
        System.out.println("\nGame Over! You played " + rounds + " round(s) with a final score of " + score + ".");
        System.out.println("Thanks for playing!");

        scanner.close();
    }
}
