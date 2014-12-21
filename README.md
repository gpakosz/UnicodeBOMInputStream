# UnicodeBOMInputStream

A helper class to skip [Unicode BOMs] at the beginning of input streams.

I initially released this class as a [Stack Overflow answer] and it apparently
got copy-pasted into several Java projects already. However, code put as answers
on Stack Overflow is licensed under [CC-BY-SA 3.0] which may not suit everybody.

[Unicode BOMs]: http://www.unicode.org/faq/utf_bom.html#bom1
[Stack Overflow answer]: http://stackoverflow.com/a/1835529/216063

--------------------------------------------------------------------------------

## Why?

Many years have passed since I wrote this class and today Java still doesn't
properly deal with UTF-8 Unicode Byte Order Marks (BOMs) at the beginning of
data. In 2001, someone opened bug [JDK-4508058] with the sound expectation Java
should detect and skip UTF-8 BOMs at the beginning of UTF-8 streams, the same
way it does for e.g. UTF-16.

Bug [JDK-4508058] remained open for a while, then got fixed and ultimately
reverted because [some other great programmers relied on that exact same bug]:

> the Java EE 5 RI and SJSAS 9.0 has been relying on detecting a BOM, setting
> the appropriate encoding, and discarding the BOM bytes before reading the
> input

See, they're complaining because shipped code breaks if/when JDK behavior
changes. And instead of fixing [JDK-4508058] and accept this would be an
annoyance only for Java EE 5 RI and SJSAS 9.0 users, people in charge at Sun
decided we're all living in a better world if [JDK-4508058] gets
closed as "won't fix". Because fuck you, just skip the BOM yourself.

[JDK-4508058]: http://bugs.java.com/bugdatabase/view_bug.do?bug_id=4508058
[some other great programmers relied on that exact same bug]: http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6378911
[CC-BY-SA 3.0]: http://creativecommons.org/licenses/by-sa/3.0/legalcode

--------------------------------------------------------------------------------

## Usage

Wrap any `InputStream` with `UnicodeBOMInputStream` and use `getBOM()` and/or
`skipBOM()` methods. See [`UnicodeBOMInputStreamUsage.java`].

[`UnicodeBOMInputStreamUsage.java`]: example/net/pempek/unicode/UnicodeBOMInputStreamUsage.java

--------------------------------------------------------------------------------

If you find this library useful and decide to use it in your own projects please
drop me a line [@gpakosz].

If you use it in a commercial project, consider using [Gittip].

[@gpakosz]: https://twitter.com/gpakosz
[Gittip]: https://www.gittip.com/gpakosz/
