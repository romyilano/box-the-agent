# Agent sandbox rule (VCN #42)

Never run generated code directly on the host. To execute any code you write, wrap it
exactly like this:

    docker run --rm --network none --memory 256m python:3.11-slim python -c "<the code>"

The agent's code is DATA handed to `docker run` as an argv element — never something the
host executes directly. No `shell=True`. Untrusted code runs only inside a throwaway,
network-less, memory-capped container that is deleted on exit.
