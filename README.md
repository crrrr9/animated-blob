HERE'S HOW IT LOOKS
https://github.com/user-attachments/assets/b649a8d5-d7ec-4c89-a636-9a6115421fb7
import java.util.Scanner;

public class LargestOfTwo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter first number: ");
        int a = sc.nextInt();
        System.out.print("Enter second number: ");
        int b = sc.nextInt();

        if (a > b)
            System.out.println(a + " is larger");
        else if (b > a)
            System.out.println(b + " is larger");
        else
            System.out.println("Both numbers are equal");
    }
}
