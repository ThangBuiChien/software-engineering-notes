# Table of content

- [Design system most commonly problem](#design-system-most-commonly-problem)

# Design system most commonly problem

## Table of content

1. Read heavy systems
2. High write traffic
3. Single point of failure
4. High availability
5. High latency
6. Handling large files
7. Monitoring and alerting
8. Slow DB queries

## Read heavy systems

- **Problem**: Read heavy systems are systems where the read requests are much more frequent than write requests.
- **Solution**:
  - **Caching**: Use caching to store the results of read queries and serve them from the cache.
  - **Read replicas**: Use read replicas to scale out read queries.
  - **Load balancer**: Use a load balancer to distribute read requests across multiple servers.
  - **Database sharding**: Use database sharding to distribute read requests across multiple databases.
