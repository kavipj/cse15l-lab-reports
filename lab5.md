# Lab Report 5

## Part 1 - Debugging Scenario

### 1. Original post from student

Hi,

I'm working on a Java project for our class, and I've run into an issue. My program compiles fine, but when I run it using my bash script, it doesn't seem to work correctly. Instead of displaying the expected output, it shows some unexpected behavior.

Here's what I'm seeing: 

![Screenshot 2024-06-10 at 3 30 34 AM](https://github.com/kavipj/cse15l-lab-reports/assets/146383794/e5d8a24a-a5d2-4047-92ba-a4eb3d49233e)

From what I can tell, the issue might be related to the input I'm providing through the script. The script should read a file, process it, and print some results. Any pointers on what might be going wrong?

---

### 2. Response from TA

Hi,

Thanks for providing the screenshot. It looks like there might be an issue with how the input file is being read or processed. Could you try adding some debug statements to your Java code to print out the contents of the file as it reads it? Also, can you share the output of running the `cat input.txt` command in your terminal?

This will help us understand if the file contents are being read correctly.

---

### 3. Information student got from trying command

Thanks for the suggestion. I added some debug statements and ran the command you mentioned. Here's what I got: ![Screenshot 2024-06-10 at 3 31 46 AM](https://github.com/kavipj/cse15l-lab-reports/assets/146383794/94f44101-62e3-43c6-a3cc-bae31e0ce77c)

It seems like the file is being read correctly, but my program is still not processing it as expected. Any ideas?

---

### 4.

**- The file & directory structure needed**

```
project/
├── input.txt
├── Main.java
└── run.sh
```

**- The contents of each file before fixing the bug**

`input.txt`:

```
123
abc
456
```

`Main.java`:

```
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        String fileName = "input.txt";
        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println("Read line: " + line); // Debug statement
                int number = Integer.parseInt(line);
                System.out.println("Processed number: " + number);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } catch (NumberFormatException e) {
            System.out.println("Invalid number format: " + e.getMessage());
        }
    }
}
```

`run.sh`:

```
javac Main.java
java Main
```

**- The full command line (or lines) you ran to trigger the bug**

`bash run.sh`

**- A description of what to edit to fix the bug**

The bug is in the Main.java file. The program attempts to parse every line as an integer, which fails for non-numeric lines like "abc". To fix this, we should add a check to skip non-numeric lines.

Fixed  `Main.java` file:

```
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        String fileName = "input.txt";
        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println("Read line: " + line); // Debug statement
                try {
                    int number = Integer.parseInt(line);
                    System.out.println("Processed number: " + number);
                } catch (NumberFormatException e) {
                    System.out.println("Skipping invalid line: " + line);
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Part 2 - Reflection

One thing that I learned in the second half of the quarter was how to creat my own autograder. This was interesting because I learned how our own work gets graded and the wha the process is to get an autograder set up. It was also fun to experiment with my own autograder to add different grading functions or improve the usability of the program. 
