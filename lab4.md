# Lab 4 Report

**1. Log into ieng6**

- Screenshot:

<img width="943" alt="Screenshot 2024-05-20 at 6 16 21 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/953aecd5-678c-473d-991d-3766d775d694">

- Keys pressed: `ssh<space>kpateljhawar@ieng6.ucsd.edu<enter>`

- Summary of command run and effects of keypresses: This command establishes an SSH connection to the ieng6 server using the specified username. The `<enter>` key executes the SSH login command after typing the complete command.

**2. Clone your fork of the repository from your Github account (using the SSH URL)**

- Screenshot:

<img width="866" alt="Screenshot 2024-05-20 at 6 21 30 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/a858f604-93cf-49fc-9f8a-d28536f4ce9d">

- Keys pressed: `git<space>clone<space>git@github.com:kavipj/lab7.git<enter>`

- Summary of command run and effects of keypresses: The  `git clone` command followed by the repository URL, separated by `<space>`, and `<enter>` to execute, clones the specified GitHub repository to the local machine using SSH.

**3. Run the tests, demonstrating that they fail**

- Screenshot:

<img width="612" alt="Screenshot 2024-05-21 at 3 33 28 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/680eb435-2be1-4367-bdf0-9c4ff7bc2a23">

- Keys pressed: `cd<space>lab7<enter>ls<enter>bash<space>test.sh<enter>`

- Summary of command run and effects of keypresses: Changes the current directory to 'lab7', lists the directory contents, and executes 'test.sh' via bash. Each command is followed by `<enter>` to run it immediately.

**4. Edit the code file to fix the failing test**

- Screenshot:

<img width="428" alt="Screenshot 2024-05-21 at 3 49 28 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/4e01ebc6-9565-48d6-8c24-bb60b3683ae7">

- Keys pressed: `vim<space>ListExamples.java<enter><down><down><down><down><down><down><down><down><down><down><down><down><down>i<right><right><right><right><right><right><right><right><right><right><right>x<space>i<space>2<esc>:wq<enter>`

- Summary of command run and effects of keypresses: Opens 'ListExamples.java' in Vim, navigates to the appropriate line, deletes a character, and inserts '2' to fix a bug. The sequence ends with saving the changes and exiting Vim.

**5. Run the tests, demonstrating that they now succeed**

- Screenshot:

<img width="342" alt="Screenshot 2024-05-21 at 3 50 33 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/dd1e0df5-2e06-4ada-8001-270269e6729a">

- Keys pressed: `<up><up><enter>`

- Summary of command run and effects of keypresses: Uses the up arrow key twice to navigate to the previous command that runs the tests, then `<enter>` to execute it again. This confirms that the tests now pass with the fixes applied.

**6. Commit and push the resulting change to your Github account (you can pick any commit message!)**

- Screenshot: 

<img width="728" alt="Screenshot 2024-05-21 at 3 56 35 PM" src="https://github.com/kavipj/cse15l-lab-reports/assets/146383794/d3097af1-c14f-4996-a018-5260c0ab7526">

- Keys pressed: `git<space>add<space>ListExamples.java<enter>git<space>commit<space>-m<space>"Fixed code"<enter>git<space>push<space>origin<space>main<enter>`

- Summary of command run and effects of keypresses: Adds changes to staging with `git add`, commits them with a message using `git commit`, and pushes to the 'main' branch of the remote repository with `git push`. Each command segment is separated by `<space>` and executed with `<enter>`, ensuring the repository on GitHub is updated with the latest code changes.
