# LINUX SHELL SCRIPTING
# Table of Contents

1. **Project Overview**
2. **Project Steps and Commands**
   - 2.1 [Create Project Directory](#21-create-project-directory)
   - 2.2 [Initialize Git Repository](#22-initialize-git-repository)
   - 2.3 [Create the Bash Script File (.sh)](#23-create-the-bash-script-file-sh)
   - 2.4 [Make the Script Executable](#24-make-the-script-executable)
   - 2.5 [Set Up GitHub Repository and Link Remote](#25-set-up-github-repository-and-link-remote)
3. **Script Implementation Steps**
   - 3.1 [Prompt for User Input](#31-prompt-for-user-input)
   - 3.2 [Ask for Table Type (Full or Partial)](#32-ask-for-table-type-full-or-partial)
   - 3.3 [Full Multiplication Table](#33-full-multiplication-table)
   - 3.4 [Partial Multiplication Table](#34-partial-multiplication-table)
   - 3.5 [Validate Input Range for Partial Table](#35-validate-input-range-for-partial-table)
   - 3.6 [Handle Invalid Options](#36-handle-invalid-options)
4. **Troubleshooting (Common Issues and Solutions)**
   - 4.1 [Script Permission Denied](#41-script-permission-denied)
   - 4.2 [Invalid Input for Number](#42-invalid-input-for-number)
   - 4.3 [Invalid Range in Partial Table](#43-invalid-range-in-partial-table)
   - 4.4 [Git Remote Connection Issues](#44-git-remote-connection-issues)


## 1. Project Overview
This project involves creating a Bash script that generates a multiplication table for a given number using both list-style and C-style for loops. The script provides an option to display the table either in ascending or descending order, and the user can choose to view a full table (from 1 to 10) or a partial table with a custom range. The project is managed with Git, including initializing a local repository, committing changes, and pushing updates to GitHub.

## 2. Project Steps and Commands

### 2.1. Create Project Directory
- First, create a project directory where all files for the project will be stored.

    ![Project Directory](./images/01.directory.png)

### 2.2 Initialize Git Repository
- Initialize a Git repository in the project directory to track changes.
- Command: 
```sh 
git init
```
![Git Init](./images/02.git_init.png)

### 2.3. Create the Bash Script File (.sh)
- Create a shell script file named multiplication_table.sh where the Bash code will be written.
- Command: `touch multiplication-table.sh`
    ![Create file](./images/03.create_file.png)

### 2.4. Make the Script Executable
- Change the file permissions to make the script executable.
- Command: `chmod +x multiplication-table.sh`
![File executable](./images/04.file_executable.png)

### 2.5. Set Up GitHub Repository and Link Remote
- Create a new repository on GitHub, then add the remote link to your local Git repository.
 ![Create github repo](./images/05.create_github_repo.png)


## 3. Script Implementation Steps

### 3.1. Prompt for User Input
- Use read to prompt the user to enter a number for which the multiplication table will be generated.
```sh
echo "Enter a number:"
read number
```

### 3.2. Ask for Table Type (Full or Partial)
- Ask the user if they want a full multiplication table (1 to 10) or a partial one within a specific range.
```sh
echo "Do you want a full table or partial table? (Enter 'f' for full, 'p' for partial)"
read table_type
```

### 3.3. Full Multiplication Table
- If the user selects the full table option (f), display the multiplication table from 1 to 10 in ascending order.
```sh
if [ "$table_type" == "f" ]; then
    # Generate the full multiplication table in ascending order
    echo "Multiplication table for $number (Ascending):"
    for i in {1..10}
    do
        result=$((number * i))
        echo "$number x $i = $result"
    done
```

### 3.4. Partial Multiplication Table
- If the user chooses the partial option (p), prompt for a custom range (start and end numbers).
```sh
elif [ "$table_type" == "p" ]; then
    # Prompt for the start and end numbers of the range
    echo "Enter the start number of the range:"
    read start
    echo "Enter the end number of the range:"
    read end
```

### 3.5. Validate Input Range for Partial Table
- Check if the start and end numbers form a valid range. If valid, display the multiplication table within the specified range; otherwise, show an error message.
```sh
# Validate the range
if [ $start -le $end ]; then
    echo "Multiplication table for $number from $start to $end:"
    for i in $(seq $start $end)
    do
        result=$((number * i))
        echo "$number x $i = $result"
    done
else
    echo "Invalid range. The start number must be less than or equal to the end number."
fi
```

### 3.6. Handle Invalid Options
- Provide feedback if the user enters an invalid option for the table type.
```sh
 echo "Invalid option. Please enter 'f' for full table or 'p' for partial table."
fi
```

![implementation](./images/06.implementation.PNG)

## 4. Troubleshooting (Common Issues and Solutions)
### 4.1. Script Permission Denied
    - If you encounter a “Permission Denied” error when running the script, ensure the script has executable permissions.
    - Solution: Run chmod +x multiplication_table.sh to make the script executable.
### 4.2. Invalid Input for Number
    - If the user enters a non-numeric value, the script may behave unexpectedly as it expects a number for multiplication.
    - Solution: Add input validation to ensure that only numbers are accepted. For example:

    ```sh 
    if ! [[ "$number" =~ ^[0-9]+$ ]]; then
    echo "Invalid input. Please enter a valid number."
    exit 1
    fi
    ```

### 4.3. Invalid Range in Partial Table
    - If the user inputs a start number greater than the end number, the script will display an "Invalid range" error.
    - Solution: Make sure the start number is less than or equal to the end number, as shown in the range validation code.

### 4.4. Git Remote Connection Issues
    - If you have trouble pushing code to the GitHub repository, verify that the remote URL is correct and that you have the necessary permissions.
    - Solution: Run git remote -v to check the remote URL and verify access. If there are issues, re-add the remote with the correct URL using git remote add origin <repository_url>.
