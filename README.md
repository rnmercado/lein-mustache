lein-mustache
=============

This plugin evaluates [Mustache](http://mustache.github.com/) templates using the [Clostache](https://github.com/fhd/clostache) library. This library is in development and has been tested with Clojure 1.3.0 and Leiningen 2.0.0-preview10.

Installation
============

`lein-mustache` is available as a plugin. So, add this to your `~/.lein/profiles.clj`:

    {:user {:plugins [[lein-mustache "0.2"]]}}

Or you can include it in your `project.clj`:

    {:profiles {:dev {:plugins [[lein-mustache "0.2"]]}}}

Use
===

To evaluate a Mustache template in file, `template`, with Clojure data in file, `data`, type this:

    $ lein mustache template data

To evaluate Mustache templates listed in `project.clj` with Clojure data in file `data`, include a key `:mustache` in `project.clj`.  The corresponding value is a sequence of maps, each containing a `:template-path` and `:destination-path`.

Then, invoke `lein mustache` without the template argument,

    $ lein mustache data

Destinations for evaluated templates may themselves be templates,

Example
=======

If `resources/hello.mustache` in your Leiningen project contains the following:

    Hello, {{name}}, welcome to {{system}}.

And `resources/data.clj` contains:

    {:name "Alex"
     :system "Your Computer"}

Then running

    lein mustache resources/hello.mustache resources/data.clj

Will output

    Hello, Alex, welcome to Your Computer.

If `project.clj` contains a `:mustache` entry,

    :mustache [{:template-path "resources/hello.mustache"
                :destination-path "target/hello.txt"}]

Then running

    lein mustache resources/data.clj

Will create the file `target/hello.txt` with the same contents as above.

Contributors
============

[Alex Chin](https://github.com/achin)
[Charles Simpson](https://github.com/charlessimpson)
[John Stoneham](https://github.com/jstoneham)
