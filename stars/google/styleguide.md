---
project: styleguide
stars: 38347
description: |-
    Style guides for Google-originated open-source projects
url: https://github.com/google/styleguide
---

# Google Style Guides

Every major open-source project has its own style guide: a set of conventions
(sometimes arbitrary) about how to write code for that project. It is much
easier to understand a large codebase when all the code in it is in a consistent
style.

“Style” covers a lot of ground, from “use camelCase for variable names” to
“never use global variables” to “never use exceptions.” This project
([google/styleguide](https://github.com/google/styleguide)) links to the style
guidelines we use for Google code. If you are modifying a project that
originated at Google, you may be pointed to this page to see the style guides
that apply to that project.


*   [AngularJS Style Guide][angular]
*   [Common Lisp Style Guide][cl]
*   [C++ Style Guide][cpp]
*   [C# Style Guide][csharp]
*   [Go Style Guide][go]
*   [HTML/CSS Style Guide][htmlcss]
*   [JavaScript Style Guide][js]
*   [Java Style Guide][java]
*   [JSON Style Guide][json]
*   [Markdown Style Guide][markdown]
*   [Objective-C Style Guide][objc]
*   [Python Style Guide][py]
*   [R Style Guide][r]
*   [Shell Style Guide][sh]
*   [Swift Style Guide][swift]
*   [TypeScript Style Guide][ts]
*   [Vim script Style Guide][vim]

This project also contains [google-c-style.el][emacs], an Emacs settings file
for Google style.

We used to host the cpplint tool, but we stopped making internal updates public.
An open source community has forked the project, so users are encouraged to use
https://github.com/cpplint/cpplint instead.

If your project requires that you create a new XML document format, the
[XML Document Format Style Guide][xml] may be helpful. In addition to actual
style rules, it also contains advice on designing your own vs. adapting an
existing format, on XML instance document formatting, and on elements vs.
attributes.

The style guides in this project are licensed under the CC-By 3.0 License, which
encourages you to share these documents. See
[https://creativecommons.org/licenses/by/3.0/][ccl] for more details.

The following Google style guide lives outside of this project:

*  [Effective Dart][dart]
*  [Kotlin Style Guide][kotlin]

Since projects are largely maintained in a [VCS], writing good commit messages
is important to long term project health. Please refer to [How to Write a Git
Commit Message](https://cbea.ms/git-commit/) as an excellent resource. While it
explicitly refers to the Git [SCM], its principles apply to any system, and many
Git conventions are trivial to translate to others.

## Contributing

With few exceptions, these style guides are copies of Google's internal style
guides to assist developers working on Google owned and originated open source
projects. Changes to the style guides are made to the internal style guides
first and eventually copied into the versions found here. **External
contributions are not accepted.** Pull requests are regularly closed without
comment.

People can file [issues using the GitHub tracker][gh-tracker]. Issues that raise
questions, justify changes on technical merits, or point out obvious mistakes
may get some engagement and could in theory lead to changes, but we are
primarily optimizing for Google's internal needs.

<a rel="license" href="https://creativecommons.org/licenses/by/3.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/3.0/88x31.png" /></a>

[cpp]: https://google.github.io/styleguide/cppguide.html
[csharp]: https://google.github.io/styleguide/csharp-style.html
[swift]: https://google.github.io/swift/
[objc]: objcguide.md
[gh-tracker]: https://github.com/google/styleguide/issues
[go]: go/
[java]: https://google.github.io/styleguide/javaguide.html
[json]: https://google.github.io/styleguide/jsoncstyleguide.xml
[kotlin]: https://developer.android.com/kotlin/style-guide
[py]: https://google.github.io/styleguide/pyguide.html
[r]: https://google.github.io/styleguide/Rguide.html
[sh]: https://google.github.io/styleguide/shellguide.html
[htmlcss]: https://google.github.io/styleguide/htmlcssguide.html
[js]: https://google.github.io/styleguide/jsguide.html
[markdown]: https://google.github.io/styleguide/docguide/style.html
[ts]: https://google.github.io/styleguide/tsguide.html
[angular]: https://google.github.io/styleguide/angularjs-google-style.html
[cl]: https://google.github.io/styleguide/lispguide.xml
[vim]: https://google.github.io/styleguide/vimscriptguide.xml
[emacs]: https://raw.githubusercontent.com/google/styleguide/gh-pages/google-c-style.el
[xml]: https://google.github.io/styleguide/xmlstyle.html
[dart]: https://www.dartlang.org/guides/language/effective-dart
[ccl]: https://creativecommons.org/licenses/by/3.0/
[SCM]: https://en.wikipedia.org/wiki/Source_control_management
[VCS]: https://en.wikipedia.org/wiki/Version_control_system

