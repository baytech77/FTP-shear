# FTP-shear
1. **Imports**:
   - The script starts by importing necessary modules and classes from the `pyftpdlib` library, which is used for creating the FTP server.
   - `os` module is imported to interact with the operating system for creating directories.

2. **Define FTP Root Directory**:
   - The script sets the root directory for the FTP server to `/srv/ftp`.

3. **Create FTP Root Directory**:
   - Using `os.makedirs()`, the script ensures that the FTP root directory exists. If the directory doesn't exist, it creates it. The `exist_ok=True` parameter allows the function to ignore errors if the directory already exists.

4. **Create Authorizer**:
   - An instance of `DummyAuthorizer` is created, which is responsible for managing 'virtual' users.

5. **Define Permissions**:
   - Two permission strings are defined:
     - `super_user_perm`: Grants full permissions (`elradfmwMT`) to the super user.
     - `normal_user_perm`: Grants read and list permissions (`elr`) to normal users.

6. **Set to Store Existing Usernames**:
   - A set named `existing_usernames` is created to store the usernames of registered users. This will help ensure unique usernames during registration.

7. **User Registration Function**:
   - A function called `register_user()` is defined to handle the registration of users.
   - Inside the function:
     - It prompts the user to enter a new username using `input()`.
     - It checks if the entered username already exists in the `existing_usernames` set.
     - If the username is already taken, it prints a message asking the user to choose a different username.
     - If the username is unique, it adds the username to the `existing_usernames` set.
     - It then prompts the user to enter a password for the user.
     - If the username is "superuser", it adds the user to the authorizer with full permissions using `authorizer.add_user()`.
     - If the username is not "superuser", it adds the user with normal permissions.
     - Finally, it prints a success message indicating that the user has been registered successfully.

8. **Allow Multiple User Registration**:
   - The script prompts the user to enter the number of users they want to register.
   - It then calls the `register_user()` function the specified number of times to register the desired number of users.

9. **Create FTP Handler and Assign Authorizer**:
   - An instance of `FTPHandler` is created and assigned the authorizer.

10. **Define Server Address and Port**:
    - The server is set to listen on all available network interfaces (`"0.0.0.0"`) on port 21 (the default FTP port).

11. **Create and Start FTP Server**:
    - An instance of `FTPServer` is created using the server address, handler, and authorizer.
    - The `serve_forever()` method is called to start the FTP server and keep it running indefinitely.

12. **Print Server Start Message**:
    - Finally, a message is printed to indicate that the FTP server has started and is listening on the specified address and port.
