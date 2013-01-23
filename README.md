# tripsit

Connects two JACK servers over the network using JackTrip and SSH.

## Requirements

### Client
- [JACK](http://jackaudio.org/)
- [JackTrip](http://jackaudio.org/)
- [Expect](http://sourceforge.net/projects/expect/)
- [ssh](http://www.openssh.com/)

### Server
- [JACK](http://jackaudio.org/)
- [JackTrip](http://jackaudio.org/)
- [sshd](http://www.openssh.com/)

## Usage

    tripsit
        [--verbose] # Enable verbose (and messy) output
        [--server-jacktrip COMMAND] # Command to launch JackTrip on the server. --server is added automatically.
        [--client-jacktrip COMMAND] # ...and on the client. --client HOST is added automatically.
        [--server-cmd COMMAND [--server-cmd COMMAND ...]] # Post-launch commands to execute on the server, e.g. jack_connect <src> <dst>.
        [--client-cmd COMMAND [--client-cmd COMMAND ...]] # ...and on the client.
        [--user USERNAME] # SSH username.
        [--port PORT] # SSH port.
        --host HOST # SSH (and JackTrip server) host.

SIGINT or SIGKILL will stop both JackTrip instances.

### Example

    $ tripsit \
        --server-jacktrip /usr/local/bin/jacktrip \
        --server-cmd /usr/local/bin/jack_connect JackTrip:receive_1 system:playback_1 \
        --server-cmd /usr/local/bin/jack_connect JackTrip:receive_2 system:playback_1 \
        --client-jacktrip /usr/local/bin/jacktrip \
        --client-cmd /usr/local/bin/jack_connect Music\ Player\ Daemon:left JackTrip:send_1 \
        --client-cmd /usr/local/bin/jack_connect Music\ Player\ Daemon:right JackTrip:send_2 \
        --user ahihi \
        --host 10.0.0.9
    Password:
    Server is ready
    Client is ready
    Server commands finished
    Client commands finished
