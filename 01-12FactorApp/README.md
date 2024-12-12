# 12-Factor App

1. **Codebase**: The app's code is stored in a single versioned repository, with multiple deployments to different environments.  
2. **Dependencies**: Explicitly declare and isolate dependencies using a dependency manager, avoiding implicit dependencies.  
3. **Config**: Store configuration in environment variables, separated from the codebase to keep environments flexible.  
4. **Backing Services**: Treat backing services (databases, message queues, etc.) as attached resources that can be swapped out.  
5. **Build, Release, Run**: Separate the build, release, and run stages, ensuring that code is independently built, released, and run.  
6. **Processes**: The app runs as one or more stateless processes, with no local storage of user data between requests.  
7. **Port Binding**: The app should export a service by binding to a port and listening for incoming requests.  
8. **Concurrency**: Scale the app by running multiple processes or workers, using process-based concurrency.  
9. **Disposability**: Processes should be disposable, able to be started or stopped quickly to support scaling and reliability.  
10. **Dev/Prod Parity**: Keep development, staging, and production environments as similar as possible to reduce deployment surprises.  
11. **Logs**: Treat logs as event streams, capturing them centrally for analysis and debugging.  
12. **Admin Processes**: Run administrative tasks (e.g., migrations) as one-off processes, executed in the same environment as the app.

For more detailed information, visit [12factor.net](https://12factor.net/).[12factorGFG](https://www.geeksforgeeks.org/what-is-twelve-factor-app/)
