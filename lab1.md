# Lab 1 Report

## cd
1. **Share an example of using the command with no arguments.**
- <img width="277" alt="Screenshot 2024-04-02 at 2 44 41 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/9484a49e-af6d-4506-9631-39a92dcbfcc3">
- Output is not an error.
- Absolute path: /Users/kavi/lecture1
- Explanation of output: When you run `cd` without any arguments, it will take you to your home directory.
2. **Share an example of using the command with a path to a directory as an argument.**
- <img width="274" alt="Screenshot 2024-04-02 at 2 45 46 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/48c5ff43-a552-4489-b838-cea010fd4e4a">
- Output is not an error.
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `cd lecture1` command is used in the terminal to change the current working directory to the `lecture1` directory.
3. **Share an example of using the command with a path to a file as an argument.**
- <img width="326" alt="Screenshot 2024-04-02 at 2 46 04 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/59677382-299f-4013-9b55-a80975f5169f">
- Output is an error. You cannot change the working directory to a file. The `cd` command can only be used with directories.
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `cd` command is used to change directories. However, `Hello.java` is a file, not a directory. Therefore, if you try to run `cd Hello.java`, you will receive an error message stating that `Hello.java` is not a directory.

---

## ls
1. **Share an example of using the command with no arguments.**
- <img width="654" alt="Screenshot 2024-04-02 at 4 19 35 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/1c01bbf4-2b21-41ed-981a-90f8f2f20a40">
- Output is not an error.
- Absolute path: /Users/kavi
- Explanation of output: The `ls` command is used in the terminal to list files and directories in the current working directory. When you run `ls` without any arguments, it will display the names of all files and directories in the current directory.
2. **Share an example of using the command with a path to a directory as an argument.**
- <img width="364" alt="Screenshot 2024-04-02 at 4 19 54 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/dd81cecc-d85b-44f5-98f9-86c2414cb8a8">
- Output is not an error.
- Absolute path: /Users/kavi
- Explanation of output: The `ls lecture1` command is used in the terminal to list files and directories in the `lecture1` directory. Because `lecture1` is a directory that exists in the current working directory, the command displays the names of all files and directories in the `lecture1` directory.
3. **Share an example of using the command with a path to a file as an argument.**
- <img width="325" alt="Screenshot 2024-04-03 at 8 51 23 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/96127a72-d81d-4d86-bf41-e96a6a1ae9c1">
- Output is not an error.
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `ls Hello.java` command is used in the terminal to list the `Hello.java` file if it exists in the current working directory. Because `Hello.java` is a file that exists in the current working directory, the command will simply print `Hello.java` to the terminal.

---

## cat
1. **Share an example of using the command with no arguments.**
- <img width="271" alt="Screenshot 2024-04-02 at 4 40 05 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/4b0fd25b-7d38-4254-bc29-25f698bdd1bc">
- Output is not an error.
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `cat` command without any arguments is used to read from standard input and write to standard output. When you run `cat` with no arguments, it waits for you to enter text from the keyboard. Whatever you type will be echoed back to the terminal when you press Enter. This continues until you signal the end of the input by pressing `Ctrl+D`.
2. **Share an example of using the command with a path to a directory as an argument.**
- <img width="283" alt="Screenshot 2024-04-03 at 8 57 20 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/f2f73dc9-e5d6-4d2e-9145-4014d2213788">
- Output is an error. Because `lecture1` is a directory, you will receive an error message because `cat` cannot display the content of a directory.
- Absolute path: /Users/kavi
- Explanation of output: The  `cat` command is used in the terminal to display the content of a file. Because `lecture1` is a directory and not a file, there is an error.
3. **Share an example of using the command with a path to a file as an argument.**
- <img width="510" alt="Screenshot 2024-04-02 at 4 39 47 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/4b456a59-4fd1-4b82-89bc-7771405baa8b">
- Output is not an error.
- Absolute path: /Users/kavi/lecture1
- Explanation of output: The `cat Hello.java` command is used in the terminal to display the content of the `Hello.java` file. Because `Hello.java` is a file that exists in the current working directory, the command will print the content of `Hello.java` to the terminal.
