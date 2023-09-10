## User Authentication in Node.js using `bcrypt` & `salt`

### Bcrypt & Salt ?

`bcrypt` is an algorithm for securely hashing passwords, and `salt` is a randomly generated value that is combined with the password before hashing to enhance security.

Together, they help protect user passwords from various types of attacks and ensure that even if two users have the same password, their hashed passwords will be different. 

This makes it significantly more challenging for attackers to compromise user accounts.

### Use bcrypt to hash and verify passwords with a salt :

- Install the bcrypt library if you haven't already:

    `npm install bcrypt`

- Require the bcrypt library in your Node.js application :

    `const bcrypt = require('bcrypt');`

- Hashing a password with a salt :

    ```
    const plaintextPassword = 'user_password'; // Replace with the actual user's password

    // Generate a salt (usually a random value)
    const saltRounds = 10; // Recommended number of rounds
    bcrypt.genSalt(saltRounds, (err, salt) => {
        if (err) {
            // Handle error
            return;
        }

        // Hash the password with the generated salt
        bcrypt.hash(plaintextPassword, salt, (err, hash) => {
            if (err) {
            // Handle error
            return;
            }

            // Store `hash` in your database for this user
        });
    });

    ```
- Verifying a password during user login :

    ```
    const enteredPassword = 'user_password'; // Replace with the password entered by the user
    const hashedPassword = 'hashed_password_from_database'; // Retrieve the stored hashed password from your database

    bcrypt.compare(enteredPassword, hashedPassword, (err, result) => {
        if (err) {
            // Handle error
            return;
        }

        if (result === true) {
            // Passwords match, user is authenticated
            console.log('Authentication successful');
        } else {
            // Passwords do not match, authentication failed
            console.log('Authentication failed');
        }
    });

    ```