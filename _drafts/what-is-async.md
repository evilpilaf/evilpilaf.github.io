---
layout:     post
title:      What is Async?
keywords:   async await tpl asynchronous sync synchronous sequential blocker
---

I wanted to kickoff my blog by writing about a programming pattern that's becoming more and more prevalent and visible across all languages and frameworks: the ***async/await*** pattern.

## Where it comes from
We've seen [more](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/await) [and](https://tc39.github.io/ecmascript-asyncawait/) [more](https://www.python.org/dev/peps/pep-0492/) platforms, languages and libraries adopting async and/or await like constructs, the most recent example being [Javascript](https://tc39.github.io/ecma262/#sec-async-function-definitions), so with all this buzz around this I want to try and explain what Async is, where it comes from an how it works in a purely conceptual way, without going into many implementation details.

## How it works
![Sequential example]({{"/media/img/sync-thread.png#right" | absolut_url}})

Synchronous (or sequential or blocking) is the simplest style of programming, where tasks are executed one after the other, with one finishing completely before starting the next. This is great when the program does all operations in-process, but if there where any external dependencies, like reading or writing to a file or calling a web service it means the program will be frozen until the dependency returns.

### So how can we improve the performance of this kind of code?
![Sequential multi-threaded]({{"/media/img/sync-multi-thread.png#left" | absolut_url}})

Well, a common solution comes from multi-treading, creating more threads to handle the calls and waits, that way new tasks can just use them and not worry about being blocked. This seems like an acceptable solution until you realize the waste of resources you're incurring, not only the cost of creating and maintaining all the threads, but the amount of idle time that could be used better otherwise.

<div class="tip">Also many environments are single-threaded (See Javascript)</div>


### Async to the rescue
![Sequential multi-threaded]({{"/media/img/async-single-thread.png#right" | absolut_url}})
Seeing that the waste of resources comes from code waiting on an external entity to complete, the Asynchronous (or Non-Blocking) model returns control of the execution to the thread whilst the caller is blocked and resumes its execution once it finishes, this way the amount of idle waiting in a thread is minimized and we can better distribute our resources.

This model isn't new to the programming world, all the way to the lowest level in our computers rely on this technique to improve performance and reliability: CPUs schedule and de-schedule execution of programs constantly to achieve the semblance of multi-tasking. TCP sends independent packages without waiting for transmission of the previous chunks to be acknowledged or completed.

Sequential programming can seem simpler and more natural, after all a basic definition of an algorithm is [***"A step-by-step procedure for solving a problem or accomplishing some end..."***](https://www.merriam-webster.com/dictionary/algorithm) so having the steps execute one after the other seems like the simplest solution. Truth is, sequentiality is an illusion, the CPU, network, storage, caches and a number of other in between processes will change the true order of execution of your code, so instead of fighting, embrace it because locks and signals, semaphores, conditional variables and all the waiting constructs come at a cost.

In the next post we'll explore more on the async pattern and see some practical examples. In the meantime I hope you enjoyed this post and see you next time!