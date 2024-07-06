# User-Management-Using-Bash

This script automates the creation of users and the assignment of groups based on input from a file. It logs all operations and generates passwords for the users.

## Usage

```bash
./user_management.sh <input_file>
```

- `<input_file>`: A semicolon-separated file containing usernames and their respective groups. Each line should be in the format `username;group1,group2,...`.

## Script Details

### Key Features

1. **Input Validation**:
   - Ensures a single argument (input file) is provided.
   - Checks for invalid or empty usernames and group names.
   
2. **Logging**:
   - Logs all actions to `/var/log/user_management.log`.

3. **Password Management**:
   - Generates a random password for each user and saves it to `/var/secure/user_passwords.txt`.

4. **Group Management**:
   - Creates groups if they do not exist and adds users to specified groups.

### Functions

- `usage()`: Displays usage information and exits.
- `log()`: Logs messages to the log file.
- `setup_files()`: Sets up the necessary directories and files.
- `create_user()`: Creates a user, sets a password, and assigns groups.
- `manage_group()`: Manages group creation and user group assignments.

### Script Flow

1. **Setup**:
   - Creates necessary directories and files for logging and password storage.
   
2. **User and Group Management**:
   - Reads the input file line by line.
   - For each line, it extracts the username and groups.
   - Validates and processes each user and group.

## Example

### Input File (`users.txt`)

```
john;admin,developers
jane;users
doe;admins,managers
```

### Command

```bash
./user_management.sh users.txt
```

### Output

- Logs actions to `/var/log/user_management.log`.
- Stores generated passwords in `/var/secure/user_passwords.txt`.

### Log File (`/var/log/user_management.log`)

```
User john created
Password for john set
Group admin created
Added john to admin group
Group developers created
Added john to developers group
User jane created
Password for jane set
Group users created
Added jane to users group
User doe created
Password for doe set
Group admins already exists
Added doe to admins group
Group managers created
Added doe to managers group
```

### Password File (`/var/secure/user_passwords.txt`)

```
john,s3cureP@ss1
jane,s3cureP@ss2
doe,s3cureP@ss3
```

## Requirements

- `bash`
- `openssl`

## Notes

- Ensure the script has executable permissions: `chmod +x user_management.sh`.
- The script must be run with sufficient privileges to create users and groups.
- Existing users or groups will not be recreated but will be logged as skipped.
