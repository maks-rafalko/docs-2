# Generics

Each type can take arguments containing other type declarations. Validation of
arguments and their number lies on the implementing side; the parser does not
limit their number or nesting and does not check their semantic correctness in
any way.

Each argument is enclosed in triangle brackets `<` and `>` and separated by a
comma (`,`).

> Please note that throughout the documentation the term "**template argument**"
> is used because the similar term "**template parameter**" is used to describe
> a declaration.
>
> If the PHP language supported generic types, then the declaration
> (in pseudo-language) of the type:
>
> * `interface Traversable<TKey of array-key, TValue of mixed>` would contain **parameters**
>
> and the reference to the type:
>
> * `Traversable<int<0, max>, string>` would contain **arguments**.

<tabs>
<tab title="examples">

> Reference to an existing class, interface or enum with template arguments.
> ```typescript
> Path\To\ExampleClass<T, U>
> ```
> {style="note"}

> Reference to builtin type with template arguments containing other generics.
>  ```typescript
>  iterable<int<0, max>, Collection<User>>
>  ```
> {style="note"}

> Trailing comma is allowed.
>  ```typescript
>  HashMap<Request, User,>
>  ```
> {style="note"}

</tab>
<tab title="counterexamples">

> Missing template argument.
> ```typescript
> example<>
> 
> // Syntax error, unexpected ">"
> ```
> {style="warning"}

> Leading comma is NOT allowed.
> ```typescript
> example<,T>
> 
> // Syntax error, unexpected ","
> ```
> {style="warning"}

</tab>
</tabs>

### Call-Site Hints

Each generic argument allows you to define an additional hint, which can 
be used, for example, in static analyzers to indicate the
[call-site variance](https://phpstan.org/blog/guide-to-call-site-generic-variance#call-site-variance).


<tabs>
<tab title="examples">

> Any identifier (in this case "`covariant`") before the template argument`s type is acceptable.
> ```typescript
> HashMap<array-key, covariant Request>
> ```
> {style="note"}

</tab>
<tab title="counterexamples">

> Only valid identifiers are allowed.
> ```typescript
> Collection<42 User>
> 
> // Syntax error, unexpected "User"
> ```
> {style="warning"}

> Multiple hints are not allowed.
> ```typescript
>  HashMap<array-key, some covariant Request>
> 
> // Syntax error, unexpected "Request"
> ```
> {style="warning"}

</tab>
</tabs>

### List Syntax

In addition to modern list declarations such as `list<int>` or
`array<array-key, int>`, the legacy `int[]` syntax is allowed.

<tabs>
<tab title="examples">

> List (array) of `User` objects.
> ```typescript
> User[]
> ```
> {style="note"}

> List of list (nested array) of `User` objects.
> ```typescript
> User[][]
> ```
> {style="note"}

</tab>
<tab title="counterexamples">

> Incorrect syntax (was [used in the PSR](https://github.com/php-fig/event-dispatcher/blob/1.0.0/src/ListenerProviderInterface.php#L14) by mistake).
> ```typescript
> User[int]
> 
> // Syntax error, unexpected "int"
> ```
> {style="warning"}

</tab>
</tabs>
