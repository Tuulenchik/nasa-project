# NASA Mission Control

A full-stack space mission scheduling project with an Express/MongoDB backend and a frontend served by the same Node.js application.

The backend loads habitable planets from a CSV dataset, synchronizes launch data from the SpaceX API, stores the data in MongoDB, and exposes REST endpoints for managing launches and retrieving planets.

## Features

- Load habitable planets from Kepler CSV data
- Fetch and store launch data from the SpaceX API
- Store planets and launches in MongoDB
- View all habitable planets
- View all launches with pagination support
- Schedule a new launch
- Abort an existing launch
- Serve the frontend through Express
- Test API endpoints with Jest and Supertest

## Tech Stack

- Node.js
- Express
- MongoDB + Mongoose
- Axios
- CSV Parse
- Jest
- Supertest
- CORS
- Morgan

## Why I Built This

I built this project to practice backend development with real data sources, database persistence, API design, and full-stack integration. It helped me understand how to work with external APIs, parse datasets, and structure a backend application into routes, controllers, models, and services.

## Project Structure

```text
src/
  app.js
  server.js
  routes/
    api.js
    planets/
    launches/
  models/
    planets.model.js
    planets.mongo.js
    launches.model.js
    launches.mongo.js
  services/
    mongo.js
    query.js
public/
data/
```
## Environment Variables

Create a `.env` file in the root directory:

```
PORT=8000
MONGO_URL=your_mongodb_connection_string
```

## Installation

```bash
npm install
```
## Run the Project

Start in development mode:

```bash
npm run watch
```

Start normally:

```bash
npm start
```

The server runs on: 

`http://localhost:8000`

## API Base URL

```text
/v1
```

## API Endpoints

**Get all planets**

`GET /v1/planets`

Returns a list of habitable planets loaded from dataset.

**Get all launches**

`GET /v1/launches`

Optional query parameters:

`GET /v1/launches?page=1&limit=10`

**Schedule a new launch**

`POST /v1/launches`

Example request body:

```json
{
  "mission": "Kepler Exploration X",
  "rocket": "Explorer IS1",
  "target": "Kepler-62 f",
  "launchDate": "December 27, 2030"
}
```

Example success response:
```json
{
  "mission": "Kepler Exploration X",
  "rocket": "Explorer IS1",
  "target": "Kepler-62 f",
  "launchDate": "2030-12-26T20:00:00.000Z"
}
```

**Abort a launch**

`DELETE /v1/launches/:id`

Example:

`DELETE /v1/launches/101`

Success response:

```json
{
  "ok": true
}
```

## Data Sources

This project uses two main data sources:

- a Kepler dataset in CSV format for habitable planets
- the SpaceX API for historical launch data

## Frontend Integration

The application serves static frontend files from the `public` directory and uses a wildcard route so frontend routing can work correctly.

## Testing

Run tests with:

```bash
npm test
```

Tests cover:

- GET /v1/launches
- POST /v1/launches
- missing required launch fields
- invalid launch dates

## What I Learned

Through this project I improved my understanding of:

- structuring an Express backend
- working with MongoDB and Mongoose
- integrating third-party APIs
- parsing CSV data streams
- building REST endpoints
- serving a frontend from an Express app
- writing API tests with Jest and Supertest