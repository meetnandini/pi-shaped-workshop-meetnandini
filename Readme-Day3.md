Question : How would you expose an internal microservice (e.g., user-auth) differently than a public-facing frontend in a Kubernetes-based product?

Answer : In a Kubernetes-based product, internal microservices like user-auth (which handle sensitive data like tokens, credentials, or internal logic) should be restricted from public access and only accessible within the cluster. This can be approached as :
Internal Microservice (user-auth)
• Use ClusterIP service (default type):
Exposes the service only within the cluster. Other services can communicate via DNS (e.g., http://user-auth:8080), but it’s not accessible externally.
• Secure communication with mTLS between services.
• RBAC and Network Policies can restrict which other services/pods can communicate with it.
• No Ingress or NodePort, unless you add an API gateway or authentication proxy in front of it.
 Public-Facing Frontend
• Expose via Ingress or LoadBalancer:
• Ingress: Efficiently routes based on paths (e.g., /home, /login) using a single public IP.
• LoadBalancer: Gives a direct public IP (used in production clouds).
• TLS termination at Ingress, rate limiting, and authentication headers to secure public endpoints.
We can use ClusterIP for internal services and Ingress or LoadBalancer for frontend/public ones.


Question: Why might a product use Ingress instead of directly exposing each microservice via LoadBalancer?

Answer : Using Ingress provides greater control, lower cost, and more efficiency in managing external access.
Benefits of Using Ingress:
1. Cost-Efficient:
• Using a LoadBalancer for every microservice can result in dozens of public IPs and unnecessary cloud cost.
• Ingress uses one LoadBalancer (or IP) to manage access to many services.
2. Centralized Traffic Routing:
• You can define rules like:
• /login → auth-service
• /dashboard → UI service
• Easy to update in a single place (Ingress resource) instead of changing all service configurations.
3. TLS Termination & SSL Management:
• TLS/SSL can be terminated at the Ingress Controller using tools like cert-manager, reducing overhead on individual services.
4. Path-based or Host-based Routing:
• Route based on URL paths (e.g., /api, /admin) or hostnames (e.g., admin.example.com vs user.example.com).
5. Security & Rate Limiting:
• Many ingress controllers (like NGINX, Traefik) support advanced features like WAF, rate limiting, IP whitelisting, etc.