import java.util.Random;
import java.util.Scanner;

public class GuessTheNumber {
    public static void main(String[] args) {
        final int MIN_NUMBER = 1;
        final int MAX_NUMBER = 100;
        final int MAX_ATTEMPTS = 5; // You can adjust this as needed
        
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        
        int generatedNumber = random.nextInt(MAX_NUMBER - MIN_NUMBER + 1) + MIN_NUMBER;
        int attempts = 0;
        int score = 0;
        boolean isGameOver = false;
        
        System.out.println("Welcome to Guess the Number Game!");
        System.out.println("I have generated a number between " + MIN_NUMBER + " and " + MAX_NUMBER + ".");
        
        while (!isGameOver) {
            System.out.println("Enter your guess:");
            int userGuess = scanner.nextInt();
            
            if (userGuess < MIN_NUMBER || userGuess > MAX_NUMBER) {
                System.out.println("Please enter a number between " + MIN_NUMBER + " and " + MAX_NUMBER + ".");
                continue;
            }
            
            attempts++;
            
            if (userGuess == generatedNumber) {
                System.out.println("Congratulations! You guessed the number in " + attempts + " attempts.");
                score += MAX_NUMBER - attempts + 1; // Add points based on attempts
                System.out.println("Your score: " + score);
                
                System.out.println("Do you want to play again? (yes/no)");
                String playAgain = scanner.next();
                if (playAgain.equalsIgnoreCase("yes")) {
                    generatedNumber = random.nextInt(MAX_NUMBER - MIN_NUMBER + 1) + MIN_NUMBER;
                    attempts = 0;
                } else {
                    System.out.println("Thanks for playing! Your final score is: " + score);
                    isGameOver = true;
                }
            } else if (userGuess < generatedNumber) {
                System.out.println("Too low! Try again.");
            } else {
                System.out.println("Too high! Try again.");
            }
            
            if (attempts >= MAX_ATTEMPTS) {
                System.out.println("Sorry, you've reached the maximum number of attempts.");
                System.out.println("The correct number was: " + generatedNumber);
                System.out.println("Do you want to play again? (yes/no)");
                String playAgain = scanner.next();
                if (playAgain.equalsIgnoreCase("yes")) {
                    generatedNumber = random.nextInt(MAX_NUMBER - MIN_NUMBER + 1) + MIN_NUMBER;
                    attempts = 0;
                } else {
                    System.out.println("Thanks for playing! Your final score is: " + score);
                    isGameOver = true;
                }
            }
        }
        
        scanner.close();
    }
}
