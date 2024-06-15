# Background Jobs

## Introduction
Many types of applications require background tasks that run independently of the user interface (UI). 

Examples include batch jobs, intensive processing tasks, and long-running processes such as workflows. Background jobs can be executed without requiring user interaction—the application can start the job and then continue to process interactive requests from users. This helps to minimize the load on the application UI, improving availability and reducing interactive response times.

For example, an application that generates thumbnails of uploaded images can perform this task as a background job, saving the thumbnail to storage when complete, without the user needing to wait. Similarly, when a user places an order, a background workflow can process the order while the UI allows the user to continue browsing the web app. Once complete, the background job can update the order data and send a confirmation email to the user.

## What are Background Jobs?
Background jobs are tasks that run independently of the user interface. They are particularly useful for tasks that:
- Do not require user interaction.
- Should not burden the UI.
- Can run asynchronously without impacting user experience.

### Types of Background Jobs
Background jobs typically include:
- **CPU-intensive jobs**: Mathematical calculations or structural model analysis.
- **I/O-intensive jobs**: Executing a series of storage transactions or indexing files.
- **Batch jobs**: Nightly data updates or scheduled processing.
- **Long-running workflows**: Order fulfillment or provisioning services and systems.
- **Sensitive-data processing**: Tasks that are better handled in a secure location.

## When to Use Background Jobs?
Background jobs are ideal when:
- The task can run without user interaction.
- The UI should not wait for the task to complete.
- Tasks that are resource-intensive or long-running.

### Triggers
Background jobs can be initiated through:
- **Event-driven triggers**: Started in response to an event.
- **Schedule-driven triggers**: Invoked on a schedule.

#### Event-driven Triggers
Event-driven invocation starts the background task in response to an event. Examples include:
- **Queue messages**: A message containing action data (e.g., user placing an order) triggers the background task.
- **Storage changes**: Monitoring storage for changes and using this data as input.
- **API requests**: UI or another job makes a request to an endpoint or web service.

Typical tasks suited for event-driven invocation include:
- Image processing
- Workflows
- Sending information to remote services
- Sending email messages
- Provisioning new users in multitenant applications

#### Schedule-driven Triggers
Schedule-driven invocation uses a timer to start the background task. Examples include:
- **Local timers**: Running within the application or operating system.
- **External timers**: Running in different applications, such as Azure Logic Apps.
- **Delayed timers**: A separate process or application starts a timer for a one-off invocation.

Typical tasks suited for schedule-driven invocation include:
- Batch-processing routines
- Routine data processing tasks
- Data analysis for daily reports
- Data retention cleanup
- Data consistency checks

### Considerations for Schedule-driven Tasks
- Ensure the task runs as a single instance to avoid duplication if the scheduler is scaled.
- Handle scenarios where tasks run longer than the period between scheduler events.

## How to Return Results?
Background jobs execute asynchronously, meaning their execution progress does not impact the UI or calling process. If communication is needed between the background task and the calling process, implement a mechanism such as:
- **Status indicators in storage**: Accessible to the UI or caller task.
- **Reply queues**: The background task sends status and completion messages.
- **Exposed APIs or endpoints**: The UI or caller can query for status information.
- **Callback mechanisms**: Background task calls back to the UI or caller via API or events.

# Resources
https://learn.microsoft.com/en-us/azure/architecture/best-practices/background-jobs#returning-results

## What Next?
### Related Topics
- Event-Driven Architecture
- Asynchronous Programming
- Queue-Based Load Leveling

### Topics for Deeper Understanding
- Advanced Scheduling Techniques
- Secure Data Processing in Background Jobs
- Scaling Background Job Processing

