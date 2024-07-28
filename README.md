# Project Management App

This is a full-stack Project Management App built with Node.js, Express, GraphQL, MongoDB, and React. It allows users to manage clients and projects, including adding, updating, and deleting clients and projects.

## Table of Contents

1. [Installation](#installation)
2. [Technologies Used](#technologies-used)
3. [Project Structure](#project-structure)
4. [GraphQL API](#graphql-api)
5. [Client Setup](#client-setup)
6. [Server Setup](#server-setup)
7. [Running the App](#running-the-app)
8. [Contributing](#contributing)
9. [License](#license)

## Installation

### Prerequisites

- Node.js
- npm
- MongoDB

### Cloning the Repository

```bash
git clone https://github.com/yourusername/project-management-app.git
cd project-management-app
```

### Installing Dependencies

#### Server-side Dependencies

Navigate to the root directory and run:

```bash
npm install express graphql express-graphql mongoose dotenv
```

#### Client-side Dependencies

Navigate to the `client` directory and run:

```bash
cd client
npm install @apollo/client graphql bootstrap font-awesome
```

## Technologies Used

- **Node.js**: JavaScript runtime for building server-side applications.
- **Express**: Web framework for Node.js.
- **GraphQL**: Query language for APIs.
- **Apollo Server**: A GraphQL server implementation.
- **MongoDB**: NoSQL database.
- **Mongoose**: ODM for MongoDB.
- **React**: JavaScript library for building user interfaces.
- **Apollo Client**: Comprehensive state management library for JavaScript that enables you to manage both local and remote data with GraphQL.
- **Bootstrap**: CSS framework for responsive design.
- **Font Awesome**: Icon set and toolkit.

## Project Structure

```
project-management-app/
├── client/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── queries/
│   │   ├── App.js
│   │   ├── index.js
│   │   └── ...
├── config/
│   ├── models/
│   │   ├── Client.js
│   │   ├── Project.js
│   └── db.js
├── graphql/
│   ├── schema.js
├── routes/
│   ├── clients.js
│   ├── projects.js
├── .env
├── package.json
├── server.js
└── ...
```

## GraphQL API

### Types

#### ProjectType

```javascript
const ProjectType = new GraphQLObjectType({
  name: 'Project',
  fields: () => ({
    id: { type: GraphQLID },
    name: { type: GraphQLString },
    description: { type: GraphQLString },
    status: { type: GraphQLString },
    client: {
      type: ClientType,
      resolve(parent, args) {
        return Client.findById(parent.clientId);
      },
    },
  }),
});
```

#### ClientType

```javascript
const ClientType = new GraphQLObjectType({
  name: 'Client',
  fields: () => ({
    id: { type: GraphQLID },
    name: { type: GraphQLString },
    email: { type: GraphQLString },
    phone: { type: GraphQLString },
  }),
});
```

### Queries

- `projects`: Fetches all projects
- `project(id: ID)`: Fetches a single project by ID
- `clients`: Fetches all clients
- `client(id: ID)`: Fetches a single client by ID

### Mutations

- `addClient(name: String!, email: String!, phone: String!)`: Adds a new client
- `deleteClient(id: ID!)`: Deletes a client and associated projects
- `addProject(name: String!, description: String!, status: String!, clientId: ID!)`: Adds a new project
- `deleteProject(id: ID!)`: Deletes a project
- `updateProject(id: ID!, name: String, description: String, status: String)`: Updates a project

## Client Setup

1. Install dependencies:

```bash
cd client
npm install
```

2. Start the client development server:

```bash
npm start
```

## Server Setup

1. Install dependencies:

```bash
cd ..
npm install
```

2. Configure the environment variables:

Create a `.env` file in the root directory and add the following:

```
MONGO_URI=your_mongodb_uri
PORT=your_port
```

3. Start the server:

```bash
npm start
```

## Running the App

1. Make sure MongoDB is running.
2. Start the server:

```bash
npm start
```

3. Start the client development server:

```bash
cd client
npm start
```

4. Open your browser and navigate to `http://localhost:3000` to see the app.

## Contributing

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes.
4. Commit your changes (`git commit -m 'Add some feature'`).
5. Push to the branch (`git push origin feature-branch`).
6. Open a pull request.

## License

This project is licensed under the MIT License.
