# Lab 1 Report

## cd
**1. Share an example of using the command with no arguments.**
- <img width="277" alt="Screenshot 2024-04-02 at 2 44 41 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/9484a49e-af6d-4506-9631-39a92dcbfcc3">
- Absolute path: /Users/kavi
- Explanation of output: When you run `cd` without any arguments, it will take you to your home directory.
**2. Share an example of using the command with a path to a directory as an argument.**
- <img width="274" alt="Screenshot 2024-04-02 at 2 45 46 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/48c5ff43-a552-4489-b838-cea010fd4e4a">
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `cd lecture1` command is used in the terminal to change the current working directory to the `lecture1` directory.
**3. Share an example of using the command with a path to a file as an argument.**
- <img width="326" alt="Screenshot 2024-04-02 at 2 46 04 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/59677382-299f-4013-9b55-a80975f5169f">
- Output is an error. You cannot change the working directory to a file. The `cd` command can only be used with directories.
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `cd` command is used to change directories. However, `Hello.java` is a file, not a directory. Therefore, if you try to run `cd Hello.java`, you will receive an error message stating that `Hello.java` is not a directory.

---

## ls
**1. Share an example of using the command with no arguments.**
- <img width="654" alt="Screenshot 2024-04-02 at 4 19 35 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/4edaab60-31cb-492c-b947-dc9d871fc1da">
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `ls` command is used in the terminal to list files and directories in the current working directory. When you run `ls` without any arguments, it will display the names of all files and directories in the current directory.
**2. Share an example of using the command with a path to a directory as an argument.**
- <img width="364" alt="Screenshot 2024-04-02 at 4 19 54 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/41d045b2-1b99-4b96-ab00-857eaa8eb274">
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `ls lecture1` command is used in the terminal to list files and directories in the `lecture1` directory. Because `lecture1` is a directory that exists in the current working directory, the command displays the names of all files and directories in the `lecture1` directory.
**3. Share an example of using the command with a path to a file as an argument.**
- <img width="287" alt="Screenshot 2024-04-02 at 4 20 15 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/7c7493b2-4eca-4791-b074-b8c3edbcf23c">
- Output is an error. The error occurs because the Java program is trying to read a file specified by the first command-line argument (`args[0]`), but if the file does not exist in the current working directory, the `Files.readString` method will throw an `IOException`.
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `ls Hello.java` command is used in the terminal to list the `Hello.java` file if it exists in the current working directory. Because the `Hello.java` file does not exist in the current working directory, you will receive an error message.

---

## cat
**1. Share an example of using the command with no arguments.**
**2. Share an example of using the command with a path to a directory as an argument.**
**3. Share an example of using the command with a path to a file as an argument.**
