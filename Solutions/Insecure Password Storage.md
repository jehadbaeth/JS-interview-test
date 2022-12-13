```JS


import * as argon2 from "argon2"; // Use more secure hashing algorithm (discuss hash trends)
import * as crypto from "crypto";
import  zxcvbn from "zxcvbn"; // enforce higher password entropy

const hashingConfig = { // based on OWASP cheat sheet recommendations (as of March, 2022)

    parallelism: 1,
    memoryCost: 64000, // 64 mb
    timeCost: 3 // number of itetations
}

async function hashPassword(password) {
    let salt = crypto.randomBytes(16); // use salting and for that use a cryptographically secure random number generator. (discuss salt requierments)
    let result = zxcvbn(password);
    if(result.score < 4)
       throw new Error({'Low Entropy':'Provided Password does not meet the minimum required entropy'});

    return await argon2.hash(password, {
        ...hashingConfig,
        salt,
    })
}

async function verifyPasswordWithHash(password, hash) {
    return await argon2.verify(hash, password, hashingConfig);
}

hashPassword("3xtR3m1yP0werf!!lP@$$0r|)").then(async (hash) => {
    console.log("Hash + salt of the password:", hash)
    console.log("Password verification success:", await verifyPasswordWithHash("somePassword", hash));

});

```