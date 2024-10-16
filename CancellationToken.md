---
tags:
  - programming_languages
  - dotnet
---
# So what is a `CancellationToken`?

Obviously, asynchronous code is good for long running operation, and the provided task mechanism is plenty powerful. But sometimes we need to control the execution flow of this tasks. Why? We want observability into our tasks and not let some task hold the CPU and thread pool and hog down precious resources. Sometimes we want to have a difference between a task getting cancelled manually versus cancelling it due to an exception (or timeout?).

Well worry not, .NET provides us with a mechanism for cooperative cancellation of asynchronous operations, based on a lightweight object called _cancellation token_.

# Basic Mental Model for the Cancellation Tokens

We have an object that creates one or more long running asynchronous operations. This object will pass this token to all of these operations. The individual operations can in turn pass copies of this token to other operations as well. At some later time, the object that created the token can use it to request the operations to stop what they are doing, essentially requesting a cancellation. This request can only be issued by the requesting object, i.e. no individual operation can cancel itself and other operations with that token. Importantly, each listener is responsible for noticing the request and responding to it in an appropriate and timely manner.

# How does .NET achieve this?
.NET provides 2 classes, [CancellationTokenSource](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtokensource?view=net-6.0) and [CancellationToken](https://docs.microsoft.com/en-us/dotnet/api/system.threading.cancellationtoken?view=net-6.0) to achieve the cancellation mechanism.

- `CancellationTokenSource` - This is the object responsible for creating a cancellation token and sending a cancellation request to all copies of that token.
- `CancellationToken` - This is the structure used by listeners to monitor the token’s current state.

The general pattern to implement the above stated, cooperative cancellation model is as follows:

- Instantiate a `CancellationTokenSource` object
- Pass the token returned by the `CancellationTokenSource.Token` property to each task or thread that listens for cancellation
- Provide a mechanism for each task or thread to respond to this cancellation
- Call the `CancellationTokenSource.Cancel` method to provide a notification for cancellation

