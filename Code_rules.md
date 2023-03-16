
# Introduction
Welcome to the PadelMates project! This document contains important information about the coding standards, branching strategy, and guidelines that must be followed in this project. Following these rules will ensure that the code is well-organized, readable, and maintainable. 

# General rules
The following are the rules that must be followed in this project:

- Do not directly push to the master, Prod, or Staging branches. Instead, create new branches from staging and make your changes there.

- Please follow the pattern in the example branch to get an idea of the overall workflow.

- Please check existing packages before installing new ones.

- Use interfaces instead of types as much as possible, unless it is necessary.

- Avoid any type.

# Branching Strategy
The following is the branching strategy that must be followed in this project:

- The branches are Prod (restricted), staging, feature, and (optionally) private branches.

- Make a Pull Request (PR) from the private branch to the feature branch, and squash & merge with a proper commit message.

- Make a PR from the feature branch to the staging branch, and squash & merge with a proper commit message.

- A pre-commit hook is configured to prevent bad commits with syntax or format errors.

- When the code is pulled from the origin, any new packages will now get installed automatically.


# Guidelines
The following are the guidelines that must be followed in this project:

- Discuss with your team members in case of complex functions that need to think in a different way.

- Variable naming should be precise and follow naming conventions. For example, if you’re getting a response from a tournament database, you should declare the variable as tournaments if there are many and tournament if there is only one.

- Functions should be named the same way as variables.

- Don’t pass unnecessary data as function parameters and don’t declare unnecessary variables or functions.

- Always declare a variable with proper naming before using it.

- Reduce nested blocks as much as possible. For example, if you're getting a response from a User Database and you want to check if the data exists or not, you should use this code instead:

```Bash 
if (!user) 
{
    return "Not Found User";
} 
if (user.noOfGroupsJoined !== MAX_NUM_GROUPS_FOR_NON_PRO)
{
    return "He's able to join";
} 
return "He's not permitted to join more";
```



# Code Quality and Formatting:
- Write clean and readable code with proper spacing, indentation and use semi-colons at the end of statements.
- Use proper arithmetic operators and be careful while converting strings to numbers. For example, instead of using const total = 10 + +user.rating, use const total = 10 + parseFloat(user.rating).
- Use loops where necessary, instead of manually counting numbers in arrays. For example, instead of defining an array like const arr = [1, 2, 3, 4, 5, ...100], define a function that acts like Python's range() method.

# Error Handling:
- Implement a global error handling strategy for the project and make sure to handle all errors and exceptions properly.
- Avoid leaving catch blocks empty and always anticipate all possible test cases.
- The error response should be in the following format:

```{"statusCode": 404,
 "message": "Tournament with the given ID is not found",
 "path": "/api/tournaments/userID"}
```

# Response Sending:
- Always send responses with a status code, a success boolean, and a message. The response should be in the following format:

```Bash
{"statusCode": 201,
 "success": true,
 "message": "User is created successfully",
 "user": {
   "_id": "abcdefgh12345",
 }
}
```

# Status code need to be followed (the followings are enough for us)
 - OK: 200 
 - Created: 201
 - Accepted: 202
 - When empty response: 204
 - Found: 302
 - Bad Request: 400
 - Unauthorized: 401
 - When Payment required: 402
 - Forbidden Request: 403
 - Not Found: 404
 - Internal Server Error: 500
 
# File Creating Strategy

- File naming should be in proper way and in proper folder structure. Such as, all user content should be in a user file. In way like, user.schema.tsb.user.dto.tsc.Etc.
 
# Linting:
- Ensure all linters are filled up.
# Pre-Commit and Pre-Push Hooks:
- Run "pre-commit" and "pre-push" scripts before every commit and push.
# Prettier Rules:
- Follow the rules set by the Prettier code formatter.


# Data structure strategy 
- Every data collection should under a schema. Schema less data is not acceptable. 
- Whenever need to store or chances of storing arrays of objects you need to define a separate data schema for that object and also must to map the data. Such as, instead of doing this,


```Bash 
User {
Id string
Email string
Activity Array
}
```


- You must do this:

```Bash 
User {
Id String
Email String
}
Activity {
Id String
Type String
userId String
}
```

- Every object should be under a DTO, and also must use class validator for validating the data. 
- Always check data before it use. Like from a request, want to use body data. So first check req.body exists or not and then use it.
