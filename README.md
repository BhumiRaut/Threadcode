# Threadcode
package P11;

import java.util.Scanner;

public class SimpleChat {

    
    private static String lastMessage = "";
    private static boolean running = true;

    public static void main(String[] args) {
    
        Thread userThread = new Thread(new UserInput());
        Thread botThread = new Thread(new ChatBot());

        userThread.start();
        botThread.start();
    }

    static class UserInput implements Runnable {
        Scanner scanner = new Scanner(System.in);

        public void run() {
            while (running) {
                System.out.print("You: ");
                String input = scanner.nextLine();
                lastMessage = input;

                if (input.equalsIgnoreCase("exit")) {
                    running = false;
                }
            }
        }
    }


    static class ChatBot implements Runnable {
        public void run() {
            String previousMessage = "";
            while (running) {
                if (!lastMessage.equals(previousMessage)) {
                    
                    previousMessage = lastMessage;

                    
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                    if (lastMessage.equalsIgnoreCase("exit")) {
                        System.out.println("ChatBot: Goodbye!");
                        break;
                    } else if (lastMessage.toLowerCase().contains("hello")) {
                        System.out.println("ChatBot: Hi there!");
                    } else if (lastMessage.toLowerCase().contains("how are you")) {
                        System.out.println("ChatBot: I'm just a program, but I'm doing fine!");
                    } else {
                        System.out.println("ChatBot: I didn't understand that.");
                    }
                }

    
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
