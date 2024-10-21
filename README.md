# tech-learnings

**Cargo cult programming(copy paste programming)**

Cargo cult programmers copy and paste code they
either inherit or find on the internet (often, StackOverflow) without understanding why
it works, only that it works. As a result, they’re often unable to extend or make changes
to code. Similarly, cargo cult programmers often use web frameworks without understanding why the framework uses certain patterns or conventions, as well as the tradeoffs that are being made.

**What is an Idea behind a s/w Framework ?**

The reason data is persisted as cookies in the client and sessions in the server is because HTTP is a connection-less protocol, and each call to the server has no stored knowledge of the previous call. Without this understanding, using cookies and sessions seems a convoluted way of persisting information between connections. Using a framework to get around this complexity is smart because a framework normally hides the complexity and presents a uniform interface for persistence between connections. As a result, a new programmer would simply assume all it takes to persist data between connections is to use this interface.
