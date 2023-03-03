## In this repository i will try to solve the problems you might face while going through building your organization / your personal project while using appwrite as your backend service.

> Huge shout out to appwrite it is just brilliant 

### Setting up your frontend 

1. you can choose your favourite tech stack as your frontend but in this repository i will walk you through react.
2. assuming you know how to set up the basic react project.
3. now...now let me explain two situations to you the first one is preparing a database such that for every user the same database is used to handle/fetch and query.
4. now for the above situation you just need a client appwrite sdk and follow the below steps.
5. just create a appwriteConfig file with these specifications in your src directory
6. remember eerything in appwrite returns a promise.

```

import { Client , Databases , Account } from "appwrite";

const client = new Client();
client.setEndpoint("http://localhost/v1").setProject("somerandomid")

export const databases = new Databases(client);

export const account = new Account(client);

```

> Note : If you use https in the 3rd line of code you might face a network error

6. please refer to the official docs for further information about things we have used in the config file.

### Authentications 

1. you can authenticate/create new users using the account object that we have previously created in the config file

```
   const user = account.create(
        uuidv4(),
        user.email,
        user.password,
        user.name
    );
```

2. you can authenticate already existing users using the below method which will create a session igf the entered creds are already present.

```
  const login = account.createEmailSession(user.email, user.password)
```

3 . you can verify whether an user is logged in or not by using the below method which returns the promise which resolves to data about the particular user if he/she already logged in 

```
  const data = account.get()
```

4. you can loggout an user using the below method 

```
const logout = account.deleteSession("current")
```

5. you can add to the database by using the databases object we have created previously in the config section

```
const datacreation = databases.createDocument("databaseid", collectionid you can generate your own using uuidv4(), {
            the data
        })
```

6. you can retrieve the database using the below methods

```
const getTodos = databases.listDocuments("collection id from which you want to retrieve the documents")
```



