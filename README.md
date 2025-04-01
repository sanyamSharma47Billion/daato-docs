# DaatoTech Core Setup
 
Welcome to the DaatoTech Core repository! This README provides detailed instructions for setting up your local development environment.
 
## Getting Started
 
1. **Clone the Repository**
   ```bash
   git clone https://github.com/daatotech/core.git
   ```
 
2. **Install Dependencies**
   Navigate to the cloned repository directory and run:
   ```bash
   yarn install
   ```
> **Note:** Ensure you are using Yarn for package management.
 
## Local Setup Requirements
 
To run DaatoTech Core locally, you will need the following:
 
- **Docker**: Install from [Docker Hub](https://hub.docker.com/)
- **MongoDB**: For core and API
- **Redis**
- **MongoDB Compass**
- **Twingate**: For managing private services
 
We will provide environment configurations for local, API, and core setups, as well as core database collections.
 
## Local Database Setup
 
Create the necessary Docker containers with the following commands:
 
### Local API Database
```bash
docker run --restart always -d --name daato-local \
  -e MONGO_INITDB_ROOT_USERNAME=mongodb \
  -e MONGO_INITDB_ROOT_PASSWORD=mongodb \
  -p 27017:27017 mongo
```
 
### Local Core Database
```bash
docker run --restart always -d --name daato-local-core \
  -e MONGO_INITDB_ROOT_USERNAME=mongodb \
  -e MONGO_INITDB_ROOT_PASSWORD=mongodb \
  -p 27018:27017 mongo
```
 
### Redis
```bash
docker run --restart always --name my-redis -d -p 6379:6379 redis
```
 
## Running the Servers
 
Once your environment is set up, start the servers using Yarn:
 
- **Core Server**
  ```bash
  yarn start:core
  ```
 
- **API Server**
  ```bash
  yarn start:api
  ```
 
- **Frontend Server**
  ```bash
  yarn start:frontend
  ```
 
- **Before Pushing the Code**
  Ensure code formatting and testing with:
  ```bash
  npx nx run-many --all --target=lint --max-warnings=0 && npx nx format:write --all && npx nx run-many --target=test --projects=api,core --verbose && git gui
  ```
 
## Email Service Setup
 
To use the email service, clone the service repository:
```bash
git clone git@ssh.daato.ai:daato-v2/services.git
```
 
Ensure Twingate is running for accessing the service backend:
 
- Start Twingate service:
  ```bash
  sudo twingate service-start
  ```
 
- Stop Twingate service:
  ```bash
  sudo twingate service-stop
  ```
 
## Accessing the Servers
 
- **Frontend**: [http://localhost:4200/](http://localhost:4200/)
- **Core**: [http://localhost:4444/](http://localhost:4444/)
- **API**: [http://localhost:3333/](http://localhost:3333/)
- **Services Backend**: [http://localhost:8000/api/workflows](http://localhost:8000/api/workflows)
 
## Updating Service URLs
 
Update the service `baseURL` in your code depending on the environment:
 
```javascript
baseURL: `http://services-backend.${process.env.ENV_NAME}:8000/api/workflows`,
baseURL: `http://localhost:8000/api/workflows`,
```
 
## Troubleshooting
 
If a port is in use, you may need to stop the conflicting process. For example, if the API server is running on port 3333:
 
1. Find the process using the port:
   ```bash
   lsof -i tcp:3333
   ```
 
2. Kill the process:
   ```bash
   kill -9 <PID>
   ```
   Replace `<PID>` with the Process ID from the `lsof` output.
 
## Additional Resources
 
For more information about DaatoTech and its modules, visit the [Daato Support Portal](https://daato.freshdesk.com/en/support/solutions).
