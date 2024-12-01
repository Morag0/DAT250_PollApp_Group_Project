# DAT250-Project-Group-1-FeedApp

## Prerequisites

Before running the application, ensure the following software is installed:

- **Node.js** (version 16 or higher)
- **RabbitMQ** (latest version)

## How to run MongoDB and RabbitMQ

### For Windows

- Start the MongoDB service from the Windows Services Manager
- Start the RabbitMQ service from the Windows Services Manager

### For MacOS

- `brew services start mongodb`
- `brew services start rabbitmq`

### For Linux

- `sudo systemctl start mongodb`
- `sudo systemctl enable rabbitmq-server`
  - `sudo systemctl start rabbitmq-server`

## How to create the database

### Start PostgreSQL in Docker:

`cd setup`

`docker-compose up -d`

You can check if the database, users and roles were made correctly by logging in to the user and listing the database:

`docker exec -it postgres-feedapp psql -U feed-app-user -d feed_app_sql`

`\du`

The output should look something like this:

![database image](./setup/database.png)

The database is not initialized and running. To fill the database with tables, start the backend. If unsure how to do this, see the topic `How to run backend`

To stop the docker image you use:
`docker-compose down -v`
Note for testing it is wise to empty the databases through the frontend before closing so that it does not mess up the logic.

`NB! If you're asked for a password for the user called postgre, use password: yourpassword`

## How to run backend

Change directory to git repo:

`cd <PROJECT NAME>`

Ensure RabbitMQ is running:

Start server on port 3000:

`npm install`

`npm start`

## How to run frontend

Change directory to pollApp:

`cd pollApp`

Install dependencies:

`npm install`

Start frontend on port 5173:

`npm run dev`

## How it works

### Backend

The backend server runs on `http://localhost:3000` and provides the following functionalities:

- Creating polls
- Fetching polls and their vote options
- Updating vote counts
- Clearing the database

### Frontend

The frontend runs on `http://localhost:5173` and enables users to:

- Create polls with multiple vote options
- Vote on poll options
- View all polls and their respective vote counts
- Clear the database from the interface

### Database

The Postgre database is created with the required user and privileges when running `npm start`. When the backend starts the tables in the database will be generated automatically. While the MongoDB database is running when making the connection in MongoDB Compass

## RabbitMQ Configuration

Make sure RabbitMQ is installed and running on localhost. There is no additional setup required unless you are using a remote RabbitMQ instance.

## Troubleshooting

### Backend issues

- Make sure that RabbitMQ is running.
- Make sure you have installed the correct dependencies. See `How to run backend`

### Frontend issues

- Make sure that the required dependencies are installed. See `How to run frontend`

### Port issues

- Make sure that the ports `3000` for the backend and `5672` for RabbitMQ are not blocked by the firewall.
