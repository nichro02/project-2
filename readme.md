# EXPRESS AUTH BOILERPLATE
* Set up Express app and entry point JS
* Initialize git
* Install and require ejs and express-ejs-layouts
* Touch a .gitignore file (echo "node_modules" >> .gitignore)
* Create views and controllers folders
* Create signup and login forms, test corresponding post routes
* Install and initialize sequelize
    * npm i sequelize pg
    * sequelize init

# SEQUELIZE HOOKS
* Used in model to hash a password
# SEQUELIZE VALIDATIONS
* Done at the model level
# BCRYPT
* What is bcrypt?
    * Password-hashing function
    * Adaptive function that resists brute-force attacks
    * Incorporates a salt as means to hash and safeguard passwords against things such as rainbow tables
    * Based on blowfish cipher
    * There are four parts:
        * Algorithm - prefix that identifies
        * Cost - number of rounds
        * Salt - randomly generated data
        * Hash - algorithm that maps data of arbitrary size to bit array of fixed size

* How does it work?
    * Install it with npm i bcrypt
    * Require it in entry point file (const bcrypt = require('bcrypt'))
    * Define salt rounds (const saltRounds = 10)
    * Define plain text password (const myPlaintextPassword = 'password')
    * Invoke function to generate salt and hash
        * bcrypt.genSalt(saltRounds, function(err, salt) {
            bcrypt.hash(myPlaintextPassword, salt, function(err, hash) {
                //store hash in your password database
            })
        })
    * Check a password
        * //load hash from password db
        bcrypt.compare(myPlaintextPassword, hash, function(err, result) {
            //result == true
        })
    * Sample codeblock:
    const bcrypt = require('bcrypt');
    const saltRounds = 10;
    const myPlaintextPassword = 'hunter2';
    const someOtherPlaintextPassword = 'not_bacon';
    let myhash;
​
​
    //async way
    bcrypt.genSalt(saltRounds, function(err, salt) {
        bcrypt.hash(myPlaintextPassword, salt, function(err, hash) {
         // store in database
         console.log('myPlaintextPassword', myPlaintextPassword)
         console.log("hash",hash)
         myhash = hash
         bcrypt.compare(myPlaintextPassword, myhash, function(err, result) {
             // result == true
             console.log(result)
         });
        })
    });

        

* How does bcrypt work with node?
    * Need to install and require