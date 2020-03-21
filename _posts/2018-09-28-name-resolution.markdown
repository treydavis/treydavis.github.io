---
layout: post
title:  "Name resolution in Clojure"
date:   2018-08-17 11:49:46 -0700
categories: clojure elisp javascript
---
Name resolution is the way a compiler or running program determines what is referred to by a name. Small differences in the algorithms used for name resolution become major distinguishing traits of a programming language.

The basic building-block for name resolution is the lookup table. Each entry in the table is a binding from name to value/object/component/etc.  A language's name resolution algorithm can be described in terms of what lookup tables are considered and in what order they are preferred.

The foundational lookup tables for Clojure are namespaces. Name resolution for symbols that are namespace qualified (`namespace/symbol`) is simple: if the namespace has a binding for the symbol it is successfully resolved.

When a symbol is not namespace qualified it is looked up in the current namespace, `*ns*`. Calls to `ns` and `in-ns` change the current namespace. Clojure source files use a call to `ns` at the begining so that each file is written in the context of a particular namespace.

~~~klipse
(ns boop)
(def a true)
(println { :current-*ns* (ns-name *ns*)
           :resolve-a (resolve 'a)
           :resolve-b (resolve 'b) })
(println "☝️ a is in boop, b is not\n")

(ns beep)
(def b true)
(println { :current-*ns* (ns-name *ns*)
           :resolve-a (resolve 'a)
           :resolve-b (resolve 'b)})
(println "☝️ b is in beep, a is not")
(println "but we can still get to a:" (resolve 'boop/a))
~~~

Suppose we have two lookup tables `A` and `B` and that `A` has preference over `B`. If both `A` and `B` have bindings for the name `x` then `A`'s binding for `x` will be said to shadow or mask `B`'s binding for `x`. This is an important and useful property of creating a preference-ordered stack of lookup tables. It provides the basis for encapsulation and modulatrity.

There are two different techniques for building up a stack of lookup tables: static and dynamic. The static technique is called 'static' because it allows names to be resolved without ever running the code. It is also called "lexical" for the same reason: bindings can be determined from language semantics.

Clojure supports lexical binding with `let`, `loop` and `fn`. Each accepts a vector to establish lexical bindings.

~~~klipse
(ns foo.core$macros) (defmacro local-bindings [] (list 'quote (keys (:locals &env))))
(ns foo.core)

(def x "ns")
(println "value of x:" x)

(let [x "B" from-b 1]
    (println "B locals:" (foo.core/local-bindings))
    (println "value of x:" x)
    (let [x "A" a-only 1]
        (println "A locals:" (foo.core/local-bindings))
        (println "value of x:" x)))
~~~

The second technique for stacking lookup tables is dynamic binding. These bindings are 'dynamic' because they can only resolved by running the code. Dynamic bindings can affect "free" references, those that are not lexically bound:

``` clojure
(defn foo [lexically-bound] free-reference)
;; free-reference has no lexical binding and could be dynamically bound
```

In Clojure, dynamic vars are declared on the namespace and marked as dynamic. Dynamic bindings are created with `binding` in the same format  as `let`.

~~~klipse
(def ^:dynamic dynamic-var "root-binding")
(defn foo [] dynamic-var)

(println "namespace:" (foo))
(binding [dynamic-var "dynamically-bound"]
    (println "binding:" (foo)))
(let [dynamic-var "lexically-bound"]
    (println "let:" (foo)))
~~~

Dynamic binding allows a function to output different values for the same input arguments, that is, it allows for violations of functional purity. Despite this undesireable quality, it has been included in Clojure for its utility and power. For evidence of the usefulness of dynamic binding look at Emacs-lisp (Elisp).

If you use Emacs, [as half of Clojurists do](http://blog.cognitect.com/blog/2017/1/31/clojure-2018-results), you'll encounter plenty of Elisp. Elisp's default name resultion uses dynamic binding. `let` in Elisp works like `binding` in Clojure:

``` lisp
(defun magit--shell-command (command &optional directory)
  (let ((default-directory (or directory default-directory))
        (process-environment process-environment))
    (push "GIT_PAGER=cat" process-environment)
    (magit-start-process shell-file-name nil
                         shell-command-switch command))
  (magit-process-buffer))
```

This snippet comes from Magit. It dynamically binds a custom directory to `default-directory`. It creates a new dynamic binding for `process-environment`, pushes on a new entry (without mutating the original) and calls `magit-start-process` which runs a shell command using the dynamically-established working directory and `PATH`.
