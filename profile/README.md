<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/jenesis/.github/main/profile/jenesis-lockup-dark.svg">
    <img alt="Jenesis" src="https://raw.githubusercontent.com/jenesis/.github/main/profile/jenesis-lockup-light.svg" height="90">
  </picture>
</p>

<p align="center"><em>Java-native config, plugin-free, with <code>module-info.java</code> treated as a feature, not an afterthought.</em></p>

<p align="center">
  <a href="https://jenesis.build"><strong>jenesis.build</strong></a>
</p>

## A build tool for Java, written in Java

The engine ships *with* your project as plain source under `build/jenesis/`, and the JDK launches it directly.
There is no wrapper binary, no fetched plugin tree and no daemon. Modules declared with `module-info.java`
drive the build, every step is content-hashed so unchanged work is reused, and every dependency can be pinned
by version *and* by the checksum of the artifact it resolved to. It needs a JDK 25 or newer, and nothing else.

```bash
sdk install jenesis && jenesis-init      # or: curl -fsSL https://get.jenesis.build | bash
java build/jenesis/Project.java          # build, test and package
```

## The tools

| Tool | What it does | Repository |
|---|---|---|
| **[Jenesis](https://jenesis.build/tool/)** | The build tool itself. Vendored as source, driven by `module-info.java`, with content-hashed steps and checksum pinning. | [`jenesis`](https://github.com/jenesis/jenesis) |
| **[jpx](https://jenesis.build/jpx/)** | Runs any published module or Maven artifact with one command: `npx` for the module path. | [`jenesis`](https://github.com/jenesis/jenesis) |
| **[Launcher](https://jenesis.build/launcher/)** | Executable jars that keep real Java modularity. Dependencies are rebuilt into a live `ModuleLayer` instead of being merged into a fat jar. | [`jenesis-launcher`](https://github.com/jenesis/jenesis-launcher) |
| **[Module Index](https://jenesis.build/modules/)** | Every module name declared on Maven Central, resolved to the artifact behind it, so a build can answer what `module-info.java` actually asks. | [`jenesis-modules`](https://github.com/jenesis/jenesis-modules) |
| **[Repository](https://jenesis.build/repository/)** | A module-aware, database-free artifact repository serving Maven, modules and OCI over one content-addressed store. Publish a modular jar once, and both ecosystems resolve it. | [`jenesis-repository`](https://github.com/jenesis/jenesis-repository) |

The [documentation](https://github.com/jenesis/jenesis-documentation) behind jenesis.build lives here too, as
do the [Homebrew tap](https://github.com/jenesis/homebrew-tap) and the
[Scoop bucket](https://github.com/jenesis/scoop-bucket) that distribute releases.

## Where this comes from

Jenesis is the work of [Rafael Winterhalter](https://github.com/raphw), who also wrote
[Byte Buddy](https://bytebuddy.net), the code generation and manipulation library used by
[Mockito](https://site.mockito.org/), [Hibernate](https://hibernate.org/),
[Jackson](https://github.com/FasterXML/jackson) and [Bazel](https://bazel.build/). Oracle recognised it with
a Duke's Choice award in 2015, and it is downloaded over 75 million times a year.

Byte Buddy came from taking the JVM seriously as it is rather than working around it. Jenesis comes from the
same instinct, applied to what the years since have made plain: the Java module system is a first-class part
of the language that most builds still treat as an afterthought, and the toolchain around it asks projects to
adopt a wrapper, a plugin ecosystem and a daemon before it will compile a single class. A build should be
readable Java, it should resolve what a module actually declares, and it should be something you can vendor
into a repository and still trust years later. That is the whole of the effort here: to leave the Java
ecosystem a little better equipped than it was.
