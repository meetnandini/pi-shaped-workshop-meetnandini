Question 1 : Why is Docker useful in building and deploying microservices for a real-world product (like an e-commerce or banking app)?

Answer : Docker provides a lightweight, consistent, and isolated environment for each microservice, making it ideal for complex products like e-commerce or banking apps. Benefits include:
• Consistency: Works the same across dev, staging, and production.
• Isolation: Each microservice runs in its own container, avoiding dependency conflicts.
• Portability: Containers can run anywhere—local machine, cloud, or on-prem.
• Faster Deployment: Containers spin up quickly, enabling faster release cycles and CI/CD automation.


Question 2 : What is the difference between a Docker image and a container in the context of scaling a web application?

Answer: 

Docker Image
1. Blueprint or snapshot of an application and environment
2. Read only
3. created once and used many times
4. can be understood as a class in OOP

Docker Container
1. A running instance of a docker image
2. Read, write
3. Can be restarted, stopped or scaled dynamically
4. Can be understood as an object instanced of a class

Question 3 : How does Kubernetes complement Docker when running a product at scale (e.g., hundreds of containers)?

Answer : 
While Docker handles containerization, Kubernetes handles container orchestration. Kubernetes brings:
• Auto-scaling: Adjusts the number of containers based on CPU/memory usage.
• Self-healing: Restarts failed containers automatically.
• Load balancing: Distributes traffic evenly across container replicas.
• Service discovery: Enables communication between microservices seamlessly.
• Rolling updates & rollbacks: Zero-downtime deployments and safe rollbacks.
