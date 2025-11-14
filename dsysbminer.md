# dsysbminer Documentation
__dsysbminer__ is the miner program.

## Installation & Configuration
- source code: [__dsysbminer__ source code](https://github.com/mosalut/dsysbminer)
- excutable: [__dsysbminer__](https://github.com/mosalut/dsysbminer/releases/download/v1.0.0/dsysbminer_x86_64-1.0.0.rar)

## Running  
```bash
./dsysbminer [-http_port]
```

Assuming you are already in the directory where the program is located, you can run the miner program directly in the terminal, or run it in the background using `&`. Cause __dsysbminer__ was going to connect the main program __dsysb__, you should run __dsysb__ first.
For example:  

```bash
./dsysbminer &
```

For background execution, it is recommended to use [__tmux__](https://github.com/tmux/tmux/wiki)
