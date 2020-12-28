## Network Engine Docker Image

The image sets up Stockfish engine as a network service via xinetd. It downloads the source code from [Stockfish](https://github.com/official-stockfish/Stockfish) and compiles for *x86_64*. Works with [Droidfish](https://github.com/peterosterlund2/droidfish).

*stockfish.conf* is the configuration file for xinetd. The default tcp port is *54321*.