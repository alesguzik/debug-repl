# debug-repl

Inspired by [an older
library](https://github.com/georgejahad/debug-repl), debug-repl is a
debug repl implemented as an nrepl middleware. It allows you to set
breakpoints that cause the execution to stop and switches the repl to
evaluate code in the context of the breakpoint.

## Usage

Add the dependency and the middleware, e.g. in your `:user` profile:

``` clojure
:dependencies [[com.gfredericks/debug-repl "0.0.9"]]
:repl-options
  {:nrepl-middleware
    [com.gfredericks.debug-repl/wrap-debug-repl]}
```

Then when you're ready to set breakpoints (you may need to reload your
namespaces or do `(use 'clojure.core :reload)` first):

``` clojure
user> (let [x 41] (break!))
Hijacking repl for breakpoint: unnamed
user> (inc x)
42
user> (unbreak!)
nil
nil
```

### `unbreak!!`

The `unbreak!!` function (with two `!`s) will cancel all further
breakpoints for the remainder of the original evaluation's scope.

### `catch-break!`

A macro which will break only if the wrapped code throws an exception.

## TODOs

- Implement `(throw! ex-fn)` for unbreaking and causing the original
  execution to throw an exception.

## License

Copyright © 2014 Gary Fredericks

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.
