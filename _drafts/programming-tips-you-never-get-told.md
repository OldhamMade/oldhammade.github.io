Commits:

PMs want the ticket number. Devs want an outline of what you changed. Keep it simple.

Regular Expressions:

If your language of choice has the option, ALWAYS use "verbose". If not, place each logical chunk of your regex into a list, each list item on a new line, and use a comment to describe what that chunk is doing. Implode the list into a string to use it.

You are not a good programmer:

You're just not. I've been programming for 15 years. I meet new devs all the time. Very rarely do I meet someone I can learn something from, and I spend a lot of my business hours fixing what other people have done -- that's my job. But I also know I'm not a good programmer. There are superstars everywhere. You may be one of them. But the good programmers know they're just good *enough* at the things they know.

Write self-documenting code:

Give your variables *real* names. Think about that word there: name. It's more than just an identifier. Its more than that. Try to describe what the data within the variable *is*. `i`, `j`, and `k` are useless. One day you'll realise this, and that day will probably be when you come to re-read your old code and wonder what was going through your mind when you wrote it. Do your future-self a solid and put your thought process down into the actual code.

Write comments:

This follows from above; when something is complex, explain what you're doing in comments *as well as* in the code. Explain the reasons why you're doing it. Explain the dependences/gotchas/pitfalls you're facing, because they might not be there when future-you looks back at the code to fix the bug and realises they can optimise those things out.

Learn what's in the standard library:

To this day it shocks me that so many devs try to re-invent the wheel because they don't know there's something in the stdlib for the language they're working in. It takes no time at all to browse the ToC to see if there's a package/module/function that might save you hours of dev.

Learn the data structures available to you:



Early/Often:

You've heard the "save early, save often" mantra. Here are some variations that also hold true:

- return early, return often:
- break early, break often
- throw early, throw often


Use the right tool for the job:

Spend a little time and do a bit of research. While the stdlib might have a module that does what you need to do, someone may have created a much more useful package that works around some warts you didn't know about. The `Requests` package comes to mind.
