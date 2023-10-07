# reverse-shell-php
This repo includes reverse shell executable script in php

# Reverse Shell PHP Script Explanation

This PHP script is designed to create a reverse shell, a network connection from a compromised target machine (the one running this script) to an attacker-controlled server. Please note that this script is for educational purposes only and should not be used for unauthorized or malicious activities.

## Configuration Variables

- `$ip`: The IP address to which the reverse shell will connect. Change this to the attacker's server IP.
- `$port`: The port on the attacker's server to which the reverse shell will connect. Change this to the desired port.
- `$chunk_size`: The maximum size of data chunks to transfer between the shell and the attacker's server.
- `$shell`: The command to execute on the compromised machine once the reverse shell is established.

## Daemonization

- The script attempts to daemonize itself using `pcntl_fork`. Daemonization involves forking the process to run in the background and become a session leader, detaching from the terminal. This helps prevent zombie processes.

## Filesystem and Umask Configuration

- It changes the current working directory to the root directory.
- Removes any inherited umask, ensuring that file permissions are not affected.

## Reverse Shell Connection

- The script establishes a TCP connection to the attacker's server using `fsockopen`.

## Shell Process Execution

- It spawns a shell process on the compromised machine using `proc_open` with the specified `$shell` command.
- Sets up pipes for standard input, standard output, and standard error to communicate with the shell process.

## Non-blocking Streams

- Sets streams for the socket and shell pipes to non-blocking mode to prevent blocking issues during communication.

## Communication Loop

- Enters a loop to continuously handle communication between the compromised machine and the attacker's server.
- It checks for data availability on the socket and shell process pipes using `stream_select`.
- If data is available, it reads from one end and writes it to the other end to maintain the interactive shell connection.

## Cleanup and Closure

- Closes all open sockets and pipes.
- Terminates the shell process using `proc_close`.

## Print Function

- The `printit` function is used to display messages to the console, but it only prints if the script is not daemonized. This is useful for debugging purposes.

This script is essentially a tool that, when misused, can be used for unauthorized access and control of a compromised machine. It is crucial to emphasize that using such scripts for any illegal activities or without proper authorization is against the law and unethical. Always use your programming skills responsibly and legally.
