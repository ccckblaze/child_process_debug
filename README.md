# child-process-debug #

Convenience methods for debugging child processes in Node.JS. Child processes will be started with `--debug` if the
parent was started with `--debug` and the children will each get their own increasing port number based off the 
parent's port number. The default port is 5858. 

## Example ##
```JS
var childProcessDebug = require('child-process-debug');

for (var i = 0; i < 4; i++) {
    //if this script wasn't run with --debug this will spawn node example.js [0-3]
    //if this script was run with --debug, this will spawn node --debug=[5859-5862] example.js [0-3]
    childProcessDebug.spawn(['example.js', i]);
}
```

## Methods ##

### spawn([command][, args][, options]) ###
This takes the exact same arguments as `child_process.spawn` and if the parent had debugging turned on (via --debug),
it'll turn on debugging for the spawned child. `command` is also optional (unlike `child_process.spawn`) and defaults
to `process.execPath`.

### nextPort() ###
Returns the next debug port that comes after the current process's debug port. If the current process doesn't have
debug turned on then this will return `undefined`. This is useful if you're not using `spawn` and want to specify the
`--debug=port` argument yourself.

### port() ###
Returns the current process's debug port or `undefined` if debug is not turned on.