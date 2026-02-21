# Self-Hosting and Deployment

Activepieces offers a Cloud solution as well as robust self-hosted options. 

## Self-Hosted Environment

Self-hosting is extremely common due to data privacy constraints. It comes in two primary forms:
1. **Docker Compose**: The quickest local or single-instance setup path. It runs the API server, Frontend, a PostgreSQL database, and Redis (for queues).
2. **Kubernetes (Helm)**: For enterprise scalability.

### Architecture Services
- **API (Backend)**: NestJS server handling operations.
- **Worker**: The node executing the sandboxed code and pieces.
- **Frontend**: The Angular UI.
- **Postgres**: State and metadata storage.
- **Redis**: BullMQ job queue for reliable flow execution scheduling.

## Railway & Cloud Providers
- Many users deploy easily on Railway or Render using 1-click templates for Activepieces. 

### Debugging Deployment Issues
When a user asks for troubleshooting on a deployment:
- Is Redis reachable? (Check if queued tasks simply hang indefinitely, that usually means the Worker can't talk to Redis).
- Is Postgres reachable? (API won't start).
- CORS issues: Ensure `FRONTEND_URL` is configured correctly in environment variables.
