<!-- livebook:{"file_entries":[{"name":"ElixirConcurency.png","type":"attachment"},{"name":"ElixirConcurent.png","type":"attachment"},{"name":"thank.jpeg","type":"attachment"}]} -->
# Metadata

[Livebook](https://elixir-talk.fly.dev/)

# Elixir For Programmers

## Me - Tan Duong

* 9 Years of writing code in production
* 1 Year with Elixir
* Wrote Ruby/Python/Java/Javascript/Typescript

## Humanly

* Website: https://www.humanly.io/

* Products:

  * Screening & Scheduling via Chat UI
  * AI interview assistant

* Tech stack

  * Monolith Elixir/Phoenix
  * Frontend mixed Phoenix/LiveView/Elm

## Why Elixir?

* [How WhatsApp scaled to 1 billion users with only 50 engineers](https://www.reddit.com/r/programming/comments/qfbs22/how_whatsapp_scaled_to_1_billion_users_with_only/)
* [The Road to 2 Million Websocket Connections in Phoenix](https://www.phoenixframework.org/blog/the-road-to-2-million-websocket-connections)
* [What's your experience using Elixir?
  ](https://www.quora.com/Whats-your-experience-using-Elixir)

> It's functional, concurrent, highly scalable, super stable, offers gazzilion 9’s of reliability, has many built-in features like key/ value store for instance, pleasant Ruby-inspired syntax, fast growing number of libraries, awesomely welcoming community.

<!-- livebook:{"break_markdown":true} -->

![You merely adopted concurency. I was born in it, moled by it.](files/ElixirConcurency.png)

## Learning a new language

### Some hands on tutorials

* [Elixir Koans](https://github.com/elixirkoans/elixir-koans)
* [Replit](https://replit.com/) supported Elixir
* [How José Valim Solved Advent of Code 2021 with Elixir and LiveBook](https://youtu.be/mDxJjqx5-ns?si=L-kxwN8IS439dHCv)

### Books

* [Programming Elixir 1.6: Functional |> Concurrent |> Pragmatic |> Fun](https://pragprog.com/titles/elixir16/programming-elixir-1-6/)

### Questions to ask

* Language syntax:

  * Basic types
  * Basic operators
  * Pattern matching
  * conditional (case, cond, and if)
  * String
  * Map/Dictionary
  * Modules and Functions
  * IO and the file system
  * require and import
  * try, catch, and rescue
  * Erlang libraries
  * Debugging
  * Typespecs and behaviours

* Something maybe new with Elixir

  * Recursion
  * Enumerables and streams
  * Processes
  * Module attributes
  * Structs
  * Protocols
  * Comprehensions
  * Sigils
  * Optional syntax sheet

* Does it has what we need to build real application?

## Build Applications

* Elixir Lang: https://elixir-lang.org/
* Phoenix Framework: https://www.phoenixframework.org/
* ORM: [Ecto](https://hexdocs.pm/ecto/getting-started.html)
* Package Manager: https://hex.pm/
* Task runner: [Mix](https://elixir-lang.org/getting-started/mix-otp/introduction-to-mix.html)
* Background Job: [Oban](https://hexdocs.pm/oban/Oban.html)
* Deployment: [Phoenix Release](https://hexdocs.pm/phoenix/releases.html)

## Good part

* Stable
* Currency built in
* Good syntax: pattern matching, pipe operator
* Great documents
* Great tooling, excellence test framework

[From Elixir creator](https://evrone.com/blog/jose-valim-interview) (rephrased)

> I had two goals: extensibility and productivity. Productivity was about focusing on having really good tooling. There are other languages, like Ruby and Go, that focus on tooling and the development experience. Extensibility boiled down to two things: Protocols to deal with polymorphism similar to Clojure and metaprogramming with Macro.

## Some syntax

* Variable
* Condition
* Loop
* Function
* Module
* Pattern Matching

See: https://elixir-lang.org/getting-started/introduction.html

```elixir
# Basic datatype
IO.inspect(1, label: "integer")
IO.inspect(0x1F, label: "integer")
IO.inspect(1.0, label: "float")
IO.inspect(true, label: "boolean")
IO.inspect(:atom, label: "atom / symbol")
IO.inspect("elixir", label: "string")
IO.inspect([1, 2, 3], label: "list")
IO.inspect({1, 2, 3}, label: "tuple")
```

```elixir
# If
if nil do
  "This won't be seen"
else
  "This will"
end
```

```elixir
# Case
case {1, 2, 3} do
  {4, 5, 6} ->
    "This clause won't match"

  {1, x, 3} ->
    "This clause will match and bind x to 2 in this clause, x = #{x}"

  _ ->
    "This clause would match any value"
end
```

```elixir
# Map
map = %{:a => 1, 2 => :b}
```

```elixir
# Module, function
defmodule Math do
  def sum(a, b) do
    a + b
  end
end

Math.sum(1, 2)
```

```elixir
defmodule BinarySearch do
  def search(list, target) do
    do_search(list, target, 0, length(list) - 1)
  end

  defp do_search(_list, _target, min, max) when max < min do
    -1
  end

  defp do_search(list, target, min, max) do
    # IO.inspect("#{list}, #{target}, #{max}, #{min}")
    mid = trunc(div(min + max, 2))

    cond do
      target < Enum.at(list, mid) -> do_search(list, target, min, mid - 1)
      target > Enum.at(list, mid) -> do_search(list, target, mid + 1, max)
      target == Enum.at(list, mid) -> mid
    end
  end
end

# BinarySearch.search([1, 3, 5, 7, 11, 13, 17, 23], 15)
# |> IO.inspect(label: "Won't find anything")
list = [1, 3, 5, 7, 11, 13, 17, 23]
value = 3

index =
  BinarySearch.search(list, value)
  |> IO.inspect(label: "Will find index")

index2 =
  BinarySearch.search(list, 2)
  |> IO.inspect(label: "Won't find index")

Enum.at(list, index) == value
```

```elixir
defmodule QuickSort do
  @moduledoc """
  Implementation of QuickSort algorithm (https://en.wikipedia.org/wiki/Quicksort)

  You will be given an array of numbers, you have to sort numbers in ascending order
  using quick sort algorithm.

  Quick sort algorithm uses a divide and conquer strategy.
  It takes a pivot, and sort other numbers in functions of the pivot, divided them 
  in a smaller and a bigger group. Execute this step until there is empty list.

  Example:
   [2, 1, 5, 4, 3] 
    1. pivot:2 smaller:[1] bigger:[5, 4, 3]
    2. 2 [1] [5, 4, 3]  
    3. 2 [1] | 
             | 5 [4, 3] [] 
    4. 2 [1] | 
               | 5 | 
                   | 4 [3] []
    5. [1, 2, 3, 4, 5] # Recursion reunite all splited lists.

   [2, 1, 5, 4, 3] => [1, 2, 3, 4, 5]
  Complexity: O(n log n)
  """
  require Integer

  @doc """
    take a List and return the List with the numbers ordered
  """
  @spec sort(list(Integer)) :: list(Integer)
  def sort([]), do: []

  def sort([head | tail]) do
    smaller = Enum.filter(tail, fn x -> x <= head end) |> sort()
    bigger = Enum.filter(tail, fn x -> x > head end) |> sort()

    Enum.concat(smaller, [head]) |> Enum.concat(bigger)
  end
end

QuickSort.sort([2, 1, 5, 4, 3])
```

## Comprehension

```elixir
for n <- 1..4, do: n * n
```

```elixir
for i <- [:a, :b, :c], j <- [1, 2], do: {i, j}
```

```elixir
for <<c <- " hello world ">>, c != ?\s, into: "", do: <<c>>
```

```elixir
for {key, val} <- %{"a" => 1, "b" => 2}, into: %{}, do: {key, val * val}
```

![The world is concurrent, things don't share data and communicate with message, things fail](files/ElixirConcurent.png)

```elixir
defmodule Messaging do
  def run() do
    parent = self()

    spawn(fn -> send(parent, {:hello, self()}) end)

    receive do
      {:hello, pid} -> IO.inspect("Got hello from #{inspect(pid)}")
    end
  end
end

Messaging.run()
```

```elixir
defmodule Parallel do
  def pmap(collection, fun) do
    collection
    |> Enum.map(fn elem ->
      Task.async(fn -> fun.(elem) end)
    end)
    |> Enum.map(fn task ->
      Task.await(task)
    end)
  end
end

result = Parallel.pmap(0..10, fn x -> x * x end)

IO.inspect(result)
```

## The bad

* Editor support is okay, not great
* Interactive debugger never worked for me
* Most likely to write API client myself
* Not as many external libraries to choose from

## Surprises

* Elixir via expose us to the complexity of the following:

  * String
  * DateTime: for example, do you know that [time can go backward](https://elixirforum.com/t/system-system-time-vs-system-os-time/48529)?

* And Erlang has built it's own world and philosophy for how to built Robust application.

* Typing is coming to Elixir and it will be great!

## Question & Discussion

![Thank you](files/thank.jpeg)
