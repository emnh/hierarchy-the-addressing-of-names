# hierarchy-the-addressing-of-names
Hierarchy: The addressing of names, a discipline for writing context-limited programs.

# A program is an object and starts thus:
```js
const program = {};
```

# A function is inserted into the program like this:

```js
program.hello = function() {
  console.log("Hello world!");
};
```

# A function can call another

```js
program.add = function(a, b) {
  return a + b;
};

program.hello2 = function() {
  console.log(program.add(2, 3));
};
```

# We should group the functions under functions and so on

```js
program.functions = {};
program.state = {};
program.entrypoints = {};
```

# How do we relate to changes over time? With append-icitis? Or rename-icitis? Or just rewrite and git?

```js
program.functions.mv = function(oldPath, newPath) {
  for (let i = 0; i < oldPath.length; i++) {
    // It becomes too troublesome to rename functions in this way
  }
};
```

# So the program rewritten:

```js
program.functions.add = function(a, b) {
  return a + b;
};
program.entrypoints.hello = function() {
  console.log("Hello world!");
};
program.entrypoints.hello2 = function() {
  console.log(program.functions.add(2, 3));
};
```

# Wouldn't it be nice if we had a tool to move or rename functions? I guess some IDEs can do it.

Either find and use an IDE that can do this rename or create a commandline tool.
As a safety and cleanliness measure the tool may require git status to be clean.

# It can get unwieldy to write all function names with full paths.

Provide some form of context loading.

```js
program.entrypoints.hello2 = function() {
  const add = program.functions.add;
};
```

Should there be a tool perhaps to search and add const function shortcuts inside a function?

# Maybe we need a register function

```js
program.functions.register = function(path, fn) {
  // Chech that the path is not occupied and that the parent path exists and if not make it.
  // Assign function to path in program hierarchy.
};
```

# Every function must fit roughly in one screen.

Put a hard limit to function size and a tool that keeps it that way.

# Every father has at most seven sons..
and each son has at most seven sons and so forth. The context is always limited to 7.
The path can be longer than 7, but 7^7 is a little less than a million so you should be good for a while with shorter paths.
