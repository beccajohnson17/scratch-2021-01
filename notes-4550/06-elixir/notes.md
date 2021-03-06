## Elixir Language

Erlang: Designed for telecom switches, which require reliability and
concurrency.

 - Uses "processes" as a core concept.
 - These processes run as sequential functional code without shared memory.
 - Inter-process communication is by message passing.
 - Side effects are by message passing to build-in processes that can cheat
   (i.e. by making system calls).

Elixir: An alternate language for the Erlang VM.

The Elixir plan for web apps:

 - Each request is handled by a new Erlang process.
 - Erlang processes can be used to store state, or to manage long-running
   client connections.
 - Safe communication between processes, even across multiple servers, is
   innately provided by the VM.

The language itself is similar to ISL from Fundies 1:

 - Elixir is a lot like ISL from Fundies 1.
 - Functional language
 - Can't mutate data.
 - Can't re-assign variables.
 - Linked lists as core data type
 - No loop statements
 - Repeat by recursion
 - Loop functions: map, filter, reduce
 - Interactive REPL

But with some extra features not in ISL:

 - Non-LISP syntax
 - Seperate function / variable namespaces
 - Modules
 - Pattern matching
 
 - Side effects (like I/O)
 - Maps (associative arrays) are a core data type
 - Lightweight processes
 - send / receive 

## Elixir examples:

 - RW
   - ElixirScript
   - Loop functions
   - Functions have module prefixes
   - Pipelines
 - Tick
   - Show concurrent processes.

## Phoenix Framework / Practice App

```
# clone git repo
$ git clone http://github.com/NatTuck/cs4550-hw04.git
$ cd cs4550-hw04

# fetch deps
$ mix deps.get
$ (cd assets && npm install)

# run local dev server
$ mix phx.server
```

 - Double a number.

HTTP story for doubling a number.

 - HTTP GET /
   - Reply: Index page.
 - HTTP POST /double
   - Request: Send value to double
   - Response: Show result page.

We can think of a HTTP request as being like a function call. The server
needs to take inputs (request path, query string, post data) and produce an
output (the response).

We can think of Phoenix as being a tool that helps us define those functions.

The basic flow in Phoenix is:

```
request
 |> router 
 |> pipeline
 |> controller action 
 |> view
 |> template
```

Let's walk through that for doubling a number.

Note that most of the logic is in lib/pratice_web, where
the web-specific stuff lives, but that we eventually call
out to a file outside that directory to actually double
the number. Our app could conceptually end up having,
e.g., a command line interface that doesn't use HTTP
and the code to double a number would still be used.


### Deployment

 - Create "pratice" user on server.
 - Clone git repo to server.
 - Read deploy.sh - do TODOs.
 - Double check config/prod.exs - set URL.
 - Run deploy.sh
 - Install nginx config file.
 - Read start.sh - do TODOs.
 - Run start.sh
 - Think about what happens on reboot, either:
   - Add @reboot rule to crontab (crontab -e ; @reboot /home/practice/.../start.sh )
   - Create and install a systemd service file for your app.

The deployment documentation:

 - https://hexdocs.pm/distillery/guides/phoenix\_walkthrough.html
 - https://github.com/phoenixframework/phoenix/blob/master/guides/deployment/deployment.md

## Adding a New Form / Function 

Need to add the following pieces:

 - Form on the main page
 - Route
 - Controller action
 - Template
 - Implementation
 - Test

Example functionality:

 - Input: x
 - Ouput: All prime numbers up to x

