# Elixir Cheatsheet

## Functions

<img alt='pipes' width='250' src="https://github.com/user-attachments/assets/fbfc6eaf-393c-4153-aa58-7f405252eba1">

_Source: https://en.wikipedia.org/wiki/File:Polyethylene_Pipe_lengths.jpg_

Think of functions as pipes. They take data and transform it into something else.

With the Pipe Operator `|>`, we can chain multiple functions together.

We can use this analogy to reason about with side-effects as well. Elxir seems to be a functional-lite language, it's not as strict as other functional languages. I may come back to this in the future as I'm still learning Elixir.

## Pattern Matching

We can use pattern matching to achieve most of our control flow.

It's kinda like a `switch` statement in other languages, but you use it at the function signature level and "overload" your functions with pattern matching and declare different versions of your functions.

Different pipes for different shapes. Part of the function's contract instead of hidden as an implementation detail.

<img alt='pipes' width='250' src="https://github.com/user-attachments/assets/03ea9347-cc17-4aa1-a065-f5ade73625df">

```js
// JS
switch(shape) {
  case 'square':
    doSquareThing()
    break
  case 'triangle':
    handleTriangleAsync()
    break
  default:
    explode()
}
```

```elixir
# Elixir
def handle_shape(shape = triangle) do
  # handle triangles
end

def handle_shape(shape = square) do
  # handle square
end

def handle_shape(_shape) do
  # handle 'default' case
end
```

## Tail Recursion (loops when we don't have loops)

We can achieve loops via recursion.

Elixir will recognize when we are at the end of a function and will perform a jump (similar to `goto) instead of pushing a new frame. This will not blow up your stack.

```elixir
# this could be done with pattern matching as well, but tail recursion is more obvious here
def recursive_sum(num) do
  if num > 1
    # Tail Call Optimization will still happen here because this is the end of the execution path.
    num + recursive_sum(num - 1)
  else
    num
end
```

## Processes

(BEAM) processes are not OS threads, they are managed by the BEAM virtual machine. This means that they are extremely lightweight in terms of memory and CPU.

Processes run functions in a separate execution context, we can use them to hold state. Elixir provides the `Agent`, `GenServer`, and `Task` abstrations that build on top of processes ([relevant docs](https://hexdocs.pm/elixir/processes.html)).

[Requires Editing] - Communication between processes is achieved via message passing. Unlike threads, state is not shared between processes.

**Related Concepts**

- [Green thread](https://en.wikipedia.org/wiki/Green_thread) - Goroutines from golang being an example.
