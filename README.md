# babashka.json

This library provides an abstraction over several JSON implementations, covering the most common scripting use cases:

- `read-str`: reading a JSON object from a string with a configurable keyword function, defaulting to `keyword`
- `write-str`: writing a Clojure value to a JSON string
- `get-provider`: returns a symbol of the currently used JSON provider

The idea of this library is that you can use it in both JVM Clojure and
babashka, without having to write code to dispatch between your choice of JVM
Clojure library and babashka's built-in `cheshire.core` library. Instead of this:

``` clojure
#?(:bb (cheshire.core/parse-string ...)
   :clj (clojure.data.json/read-str ...))
```

you can now write:

``` clojure
(babashka.json/read-str ...)
```

instead, while still choosing your preferred implementation on the JVM.

On the JVM, this library uses whatever is on your classpath, in the following order:

- [cheshire](https://github.com/dakrone/cheshire)
- [charred](https://github.com/cnuernber/charred)
- [clojure.data.json](https://github.com/clojure/data.json)
- [jsonista](https://github.com/metosin/jsonista)

You can force an implementation by setting the `babashka.json.provider` JVM
system property before loading this library to:

- `cheshire/cheshire`
- `org.clojure/data.json`
- `com.cnuernber/charred`
- `metosin/jsonista`

For convenience this library depends on one JSON implementation,
`org.clojure/data.json`, so you don't have to include another dependency. If you don't want this dependency on your classpath, you can use:

```
:exclusions [org.clojure/data.json]
```

More implementations will be added and contributions are welcome.

Planned:

- None currently, feel free to open an issue or a PR

If you are the author of one of the planned libraries, feel free to provide a PR as well.

At some point this library will be included in babashka, but for now you can use it as a library in `bb.edn`.
