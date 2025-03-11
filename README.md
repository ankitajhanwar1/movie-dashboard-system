# Movies Full-Stack Application with Frontend and Backend

This repository contains a full-stack application with a frontend and backend, each in separate directories. The project uses Docker Compose to easily bootstrap the entire environment.

## 1. How to Start the Project

### 1.1 Prequisites

Install Docker on your system (https://www.docker.com/products/docker-desktop/)
Install Docker compose on your system 

### 1.2 Running the Application in Docker

Follow these steps to set up and run the project:

1. **Clone the repository:**
    ```bash
    git clone --recursive https://github.com/ankitajhanwar1/movie-dashboard-system.git
    cd movie-dashboard-system
    ```

2. **Navigate to the root directory of the project (where `docker-compose.yml` is located).**

3. **Start the whole environment using Docker Compose:**
    ```bash
    docker-compose up --build -d
    ```
    This will build the frontend, backend services and databases - Elasticsearch.

4. **Access the application:**
    - Frontend: [http://localhost:3000](http://localhost:3000)
    - Backend: [http://localhost:3001](http://localhost:3001)

5. **Stop the application:**
    ```bash
    docker-compose down
    ```

## 2. How to Use the App

Once the application is up and running, you can use the app as follows:

1. Open the frontend in your browser by going to `http://localhost:3000`.
2. On the frontend, you can search for movies and view the movie details.
3. The frontend communicates with the backend via HTTP API calls to fetch and display movie data stored in Elasticsearch.

## 3. Testing the system on local

### 3.1 To run the backend test cases
```bash
cd backend
npm install
npm run test
```

### 3.2 To run the frontend test cases
```bash
cd frontend
npm install
npm run test
```

## 4. Architecture Design Decisions

### 4.1 System Architecture

This system follows a typical full-stack architecture with the frontend and backend separated into distinct services.

- **Frontend (React):** The frontend is a React application, built using TypeScript. It communicates with the backend through REST APIs to fetch movies data.
  
- **Backend (NestJS):** The backend is built using NestJS, a Node.js framework. It exposes API endpoints to fetch movie data from Elasticsearch and return it to the frontend. The backend also integrates with third-party APIs (like OMDB) to retrieve movie information and store in Elasticsearch.
  
- **Elasticsearch:** Elasticsearch is used as the data store for movie-related data. The backend interacts with Elasticsearch to store and retrieve movie records.

### 4.2 Data Flow

1. The **frontend** makes a GET requests to the backend to get all movies and to get movies with a search query.
2. The **backend** queries Elasticsearch for the relevant movie data.
3. The backend also interacts with external APIs (e.g., OMDB) to retrieve movie information and stores it in Elasticsearch.
4. The **backend** returns the movie data to the frontend.
5. The **frontend** displays the movie data to the user.

### 4.3 Architecture Diagram

    +------------+       +---------------------+       +------------------+
    | Frontend   | ----> |    Backend (NestJS) | ----> |  Elasticsearch   |
    | (React)    |       |   (API & Logic)     |       |  (Data Store)    |
    +------------+       +---------------------+       +------------------+
                                    |
                                    |  
                                    |
                                    v
                      +-----------------------------+
                      |  Third-party APIs (OMDB)    |
                      |   (Movie Data Source)       |
                      +-----------------------------+


#### Components:
- **Frontend (React)**: User-facing application.
- **Backend (NestJS)**: Handles API requests, processes logic, and communicates with Elasticsearch and external APIs.
- **Elasticsearch**: Data store for movie information.

