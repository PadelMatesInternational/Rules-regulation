
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



# Coding Standard Frontend
## Javascript
- Use only the const and let while defining variables.
- Use camelCases while writing Javascript variables, functions, objects, etc.
- Use only the ES6 import/export statements unless there are any compatibility issues in some projects.
- If any newly created logic or function has the potential of being able to be reused multiple amounts times, then always move them to the helper folder so they can be reused across the projects. In case the function or logic is specifically reusable in only the project where it is created, then move them to the lib folder.
- Further, follow these ES standards while writing the Javascript code: https://github.com/airbnb/javascript .
- Always handle any possible errors when working with the codes which are prone to errors such as API calls, Promises etc. using .catch, try /catch etc.
- Always use arrow functions instead of pre-ES6 function expressions defined with the function keyword.
## React:
- Use only PascalCases while naming the Components.
- When naming a component, use the Parent Folder Name + Filename.
- Use only the Functional components while writing React components. Use Class components only in cases where a specific feature cannot be implemented in functional components.
- Use only the arrow functions while writing the React Functional Components.
- Whenever a component gets bigger to an extent where it gets harder to read or maintain, split them into multiple smaller parts wherever possible.
- Whenever a component gets bigger to an extent where it gets harder to read or maintain, split them into multiple smaller parts wherever possible.
- Example:
```Bash
import React, { FormEvent } from 'react'
import { Helmet } from 'react-helmet'
import { RegisterOptions, SubmitHandler, FieldErrors } from 'react-hook-form'
import ButtonMain from '../../../../Components/Button/Main'
import FormMain, { FormMainGroup } from '../../../../Components/Form/Main'
import Recaptcha from '../../../../Components/Security/Recaptcha'
import BannerMain from '../../../Widget/Banner/Main'

```
- If any React component with the logic and view can be reusable across the projects then always move them to the Components folder so that they can be used anywhere by just importing them into the file.
- If any React component with only the view(JSX/HTML) can be reusable across the projects then always move them to the View /Widgets Folder.
- Use React’s regular and children props wherever necessary to make better reusable components. While using the props in the child component, always destructure them in the function parameter. Example:

```Bash 
const DataPricingTable = ({
  pricingData,
  tabMode,
  pricingPlan,
  setPricingPlan,
  handleSubscription,
  subscriptionError,
  accessToken,
  subscriptionModal,
  handleShowModal,
}) => { ...
return (
<View> ...
</View> )}
```
- Always check if any code or component is previously written or not in either the Component folder or the View/Widget folder instead of writing everything from scratch or in a different method. For example, If you come across a need to implement a button/tooltip in a part of the project, Instead of writing everything from scratch or using external libraries again and duplicating the code, you can just use the button component that has been previously created. This will along with reducing code duplication and saving time also improve consistency across the project.
- While writing logic inside a React component, always categorize and organize the code in the following order:
  * UseState Hooks
  * Hook Declarations
  * UseSelectors (If present)
  * Variable Declarations (* Could vary based on the requirements) Function Statements
  * useEffect Hooks
- An Ideal example:
```Bash
// useState Hooks
const [usersId, setUsersId] = useState('')
const [isEdit, setIsEdit] = useState<boolean>(false)
const [filter, setFilter] = useState<Filter>({})
const [loading, setLoading] = useState(true)
// Hook Declarations
const history = useHistory()
const dispatch = useDispatch()
const { register, errors, handleSubmit, clearErrors, control } = useForm()
const { id } = useParams()

// Variables
const userId = parseInt(usersId, 10)
const productPriceId = parseInt(productPrice, 10)
const intervalOptions = [
  {
    label: 'Monthly',
    value: '1',
}, {
    label: 'Quarterly',
    value: '3',
}, ]
// Function Statements
const toggle = () => setModal(!modal)
const toggleEdit = () => setIsEdit(!isEdit)
const inputEvent = (e: React.ChangeEvent<HTMLInputElement>): void
=> {
  if (errors[e.target.name]) {
    clearErrors(e.target.name)
  }
  if (errors.global) {
clearErrors('global') }}
// UseEffect Hooks
useEffect(() => {
  setLoading(product?.loading || productSubscriptions?.loading)
}, [product, productSubscriptions])
useEffect(() => {
  dispatch({ type: 'USERS_GET' })
}, [dispatch])
useEffect(() => {
  setCurrentTab(activeTabQuery || 1)
}, [activeTabQuery])
useEffect(() => {
checkPagination(setPagination, subscriptions, page)
}, [subscriptions, page, subscriptions.length])
```

- For further standards to follow in React, check this link: https://github.com/airbnb/javascript/tree/master/react 

## Typescript:
- Name the interface with the title of the variable it is used for followed by the Types all in CamelCases. - - for the types use only the variable names in CamelCases. For Example: If the variable or component name is exampleName/ExampleName then when naming its interface, name it like ExampleNameTypes and when naming its type name it as ExampleName
- When declaring types for the react props, use only the interface. This is just to make it consistent across the projects.
- When you know what exactly the data will be for any particular declaration, always write the type for the whole data instead of using generic declarations.
- Always start declaring types from the APIs themselves, so that it can inherit its types to wherever they are being used (either automatically using redux or manually importing) and reduce the need of declaring types elsewhere again for the same data.
- Use a separate file to declare the types in case the list goes too long and is harder to manage in a single file.

# Folder & File Structure/Naming:
- Follow the MVC structure when creating or modifying the folders or files.
- There are multiple Folders in the project specifically used for their specific purposes, They are:
 * Public: Mostly used in react projects to store the assets, some basic configuration files, and the index.html file which is the entry point of a react application.
 * src: All the source files of the project.
 * Api: All the API calls should be done inside this project and each different API should be categorized in its own separate folder. Components: All the reusable react components, that can be used across the project.
 * Config: Any configuration files that control any part of the application should be placed inside this folder.
 * Controller: All the Screen-wise react components with only the code that consists of all the logic and functionalities of the component. Helper: Any javascript functions or logic that can be reused across the projects should be placed inside this folder.
 * Lib: Same as Helpers but are supposed to be only usable in the project for which it was made.
 * View: All the code relating to the screens of a project such as JSX/HTML inside the React component should be placed in this folder.
- While naming the folders or the files relating to React, always use PascalCases.
- Name the files or folders descriptively, and try to keep them at one or two words max. If the name needs to be more lengthy then it most probably means that they need to be categorized into their own separate folders so that the name can be shared with its parent. 
- Categorize the files into separate folders as much as possible based on their specific types so that they can be accessed easily when the project gets bigger.
General:
- Names must be descriptive and clear to any developer. Do not use abbreviations, shortcuts, or unfamiliar words so anyone else working in the same code can understand it easily.
- Use CONSTANT_CASE whenever declaring any global constant values such as Action Types, Environment Variables, etc.
- Do not leave more than a single line break between the codes, unless there is a solid reason for it.

