In this tutorial, we'll cover the basics of GraphQL schema design using four different types (Scalar, Object, Enum, Input), mutations, and queries. This will give you a solid understanding of how to structure GraphQL schemas effectively.

### GraphQL Schema Tutorial

#### 1. Scalars

Scalars represent primitive data types (e.g., String, Int, Float, Boolean, ID) in GraphQL. They are used to define the types of fields in GraphQL schemas.

```graphql
scalar Date

type Event {
  id: ID!
  name: String!
  date: Date!
  attendees: Int!
}
```

- **`scalar Date`**: Defines a custom scalar type `Date` in GraphQL. Scalars can be used for representing custom data types like dates, timestamps, etc.

- **`type Event { ... }`**: Defines an object type `Event` with fields:
  - `id`: Unique identifier of type `ID!` (non-nullable ID).
  - `name`: Name of the event of type `String!` (non-nullable String).
  - `date`: Date of the event of type `Date!` (non-nullable custom scalar `Date`).
  - `attendees`: Number of attendees of type `Int!` (non-nullable Int).

#### 2. Objects

Objects are composite types in GraphQL that contain multiple fields. They represent entities with specific characteristics and relationships.

```graphql
type User {
  id: ID!
  username: String!
  email: String!
  role: Role!
}

type Post {
  id: ID!
  title: String!
  content: String!
  author: User!
}

enum Role {
  ADMIN
  USER
}
```

- **`type User { ... }`**: Defines an object type `User` with fields:
  - `id`: Unique identifier of type `ID!`.
  - `username`: Username of type `String!`.
  - `email`: Email address of type `String!`.
  - `role`: Role of type `Role!` (enumeration `Role`).

- **`type Post { ... }`**: Defines an object type `Post` with fields:
  - `id`: Unique identifier of type `ID!`.
  - `title`: Title of the post of type `String!`.
  - `content`: Content of the post of type `String!`.
  - `author`: Author of the post of type `User!`.

- **`enum Role { ... }`**: Defines an enumeration `Role` with values:
  - `ADMIN`: Represents an administrator role.
  - `USER`: Represents a regular user role.

#### 3. Enumerations

Enumerations (`enum`) define a set of possible values for a field. They constrain the field to only one of the specified values.

```graphql
enum Status {
  ACTIVE
  INACTIVE
  PENDING
}

type Task {
  id: ID!
  title: String!
  status: Status!
}
```

- **`enum Status { ... }`**: Defines an enumeration `Status` with values:
  - `ACTIVE`
  - `INACTIVE`
  - `PENDING`

- **`type Task { ... }`**: Defines an object type `Task` with fields:
  - `id`: Unique identifier of type `ID!`.
  - `title`: Title of the task of type `String!`.
  - `status`: Status of the task of type `Status!` (enumeration `Status`).

#### 4. Inputs

Input types are used to pass arguments to mutations. They are similar to object types but are used specifically for inputting data rather than querying data.

```graphql
input CreateUserInput {
  username: String!
  email: String!
  password: String!
}

type Mutation {
  createUser(input: CreateUserInput!): User!
  updateUser(id: ID!, input: UpdateUserInput!): User!
}

input UpdateUserInput {
  username: String
  email: String
  password: String
}
```

- **`input CreateUserInput { ... }`**: Defines an input object type `CreateUserInput` with fields:
  - `username`: Username of type `String!`.
  - `email`: Email address of type `String!`.
  - `password`: Password of type `String!`.

- **`type Mutation { ... }`**: Defines mutation operations:
  - `createUser(input: CreateUserInput!): User!`: Creates a new user with input parameters of type `CreateUserInput` and returns a `User`.
  - `updateUser(id: ID!, input: UpdateUserInput!): User!`: Updates an existing user identified by `id` with input parameters of type `UpdateUserInput` and returns a `User`.

- **`input UpdateUserInput { ... }`**: Defines an input object type `UpdateUserInput` with optional fields (`username`, `email`, `password`) for updating user information.

### Summary

- **Scalars**: Represent primitive data types.
- **Objects**: Composite types with fields that represent entities.
- **Enumerations**: Define a set of possible values for a field.
- **Inputs**: Used to pass arguments to mutations.

### Example Queries and Mutations

#### Example Queries

```graphql
{
  users {
    id
    username
    email
    role
  }

  posts {
    id
    title
    author {
      id
      username
    }
  }
}
```

#### Example Mutations

```graphql
mutation {
  createUser(input: { username: "alice", email: "alice@example.com", password: "password123" }) {
    id
    username
    email
    role
  }

  updateUser(id: "1", input: { email: "newemail@example.com" }) {
    id
    email
  }
}
```

This tutorial covers essential aspects of GraphQL schema design, including scalar types, object types, enumerations, and input types. It also demonstrates how to use mutations to create and update data. Implementing these concepts will enable you to design robust GraphQL APIs efficiently. Adjust the examples and types to fit your specific application's needs!