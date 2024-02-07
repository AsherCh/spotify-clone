# Spotify Clone with Microservices Architecture

## Procedure to Run the System
1. **Create Docker Images for Each Microservice**
   - Each microservice has its own Dockerfile.
   - Build Docker images for each microservice using the Dockerfile.
     ```sh
     docker build -t <image-name> <path-to-dockerfile>
     ```

2. **Create a Docker Image for MongoDB**
   - Pull the MongoDB Docker image.
     ```sh
     docker pull mongo
     ```

3. **Create Docker Registry**
   - Set up a Docker registry to store all Docker images, including the MongoDB image.
     ```sh
     docker run -d -p 5000:5000 --restart=always --name registry registry:2
     ```

4. **Push Docker Images to the Registry**
   - Push built Docker images to the Docker registry.
     ```sh
     docker push <image-name>
     ```

5. **Create Kubernetes Services**
   - Define Kubernetes Services for each microservice using `*-service.yaml` files.

6. **Create Kubernetes Deployments**
   - Define Kubernetes Deployments for each microservice using `*-deployment.yaml` files.

7. **Deploy the System**
   - Apply the Kubernetes Service and Deployment configurations using `kubectl apply`.
     ```sh
     kubectl apply -f <service-config.yaml>
     kubectl apply -f <deployment-config.yaml>
     ```

8. **Test the System**
   - Access the exported port of the central microservice to test the deployed system.

## Design Decisions
- **MVC Architecture**
  - Each microservice follows the Model-View-Controller architecture for better organization and maintainability.
  - Advantages include separation of concerns and easier management of the codebase.
- **Microservices Structure**
  - The project consists of multiple microservices such as auth-service, song-service, media-service, and operator-service.
  - Each microservice has a consistent directory structure including config, controllers, models, routes, and middleware.
  - Separation of concerns promotes easier management and understanding of the codebase.
- **Application Entry Point**
  - `app.js` is the entry point for each microservice, initializing the server, configuring middleware, and setting up routes.
- **Dependency Management**
  - The project includes a `package.json` file for managing dependencies and package configurations, simplifying installation and management of required libraries.
- **Kubernetes Deployment**
  - Deployment and service files for each microservice are contained within a separate Kubernetes directory.
  - Deployment files (`*-deployment.yaml`) define how microservices should be deployed, while service files (`*-service.yaml`) determine how they are exposed within the cluster.

## Challenges and Solutions
- Challenges include maintaining consistency across microservices and managing dependencies.
- Solutions involve establishing coding guidelines, conducting regular code reviews, and utilizing package management tools.

## Conclusion
- Adopting the MVC architecture provides benefits for organization and maintainability.
- Challenges related to consistency and dependency management can be addressed through proper planning and utilization of resources.
- This project structure establishes a solid foundation for developing scalable and modular microservices.
- Feel free to contribute to the project and improve its functionality!
