<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/jenesis/.github/main/profile/jenesis-logo-dark.svg">
    <img alt="Jenesis" src="https://raw.githubusercontent.com/jenesis/.github/main/profile/jenesis-logo-light.svg" width="84">
  </picture>
</p>

<p align="center"><em>Java-native config, plugin-free, with <code>module-info.java</code> treated as a feature, not an afterthought.</em></p>

<p align="center">
  <a href="https://jenesis.build"><strong>jenesis.build</strong></a> - <a href="mailto:hello@jenesis.build"><stong>hello@jenesis.build</stong></a>
</p>

## What this is

A toolchain for Java that takes the module system at its word, and treats the artifacts a build consumes as
something you should be able to verify. It covers the build itself, the way a published module is run, the jar
it is packaged into, the index that says which artifact publishes a given module name, and the repository that
serves them all. Everything is written in Java, runs on a JDK 25 or newer, and needs nothing else: no wrapper
binary, no fetched plugin tree, no daemon.

```bash
sdk install jenesis && jenesis-init      # or: curl -fsSL https://get.jenesis.build | bash
java build/jenesis/Make.java             # build, test and package
```

## The tools

| Tool | What it does | Repository |
|---|---|---|
| **[Jenesis](https://jenesis.build/tool/)** | The build tool. Vendored into your project as plain source and launched by the JDK, driven by `module-info.java`, with content-hashed steps and checksum pinning. | [`jenesis`](https://github.com/jenesis/jenesis) |
| **[jpx](https://jenesis.build/jpx/)** | Runs any published module or Maven artifact with one command: `npx` for the module path. | [`jenesis`](https://github.com/jenesis/jenesis) |
| **[Launcher](https://jenesis.build/launcher/)** | Executable jars that keep real Java modularity. Dependencies are rebuilt into a live `ModuleLayer` instead of being merged into a fat jar. | [`jenesis-launcher`](https://github.com/jenesis/jenesis-launcher) |
| **[Module Index](https://jenesis.build/modules/)** | Every module name declared on Maven Central, resolved to the artifact behind it, so a build can answer what `module-info.java` actually asks. | [`jenesis-modules`](https://github.com/jenesis/jenesis-modules) |
| **[Repository](https://jenesis.build/repository/)** | A module-aware, database-free artifact repository serving Maven, modules and OCI over one content-addressed store. Publish a modular jar once, and both ecosystems resolve it. | [`jenesis-repository`](https://github.com/jenesis/jenesis-repository) |

The [documentation](https://github.com/jenesis/jenesis-documentation) behind jenesis.build lives here too, as
do the [Homebrew tap](https://github.com/jenesis/homebrew-tap) and the
[Scoop bucket](https://github.com/jenesis/scoop-bucket) that distribute releases.

## Knowing what you build on

A build is only as trustworthy as the code it pulls in, so the things that establish that are part of the tool
rather than plugins bolted onto it. Dependencies are pinned by version *and* by the checksum of the artifact
that was resolved, so the bytes you build are the bytes you vetted. Every build emits a CycloneDX bill of
materials by default, licences are checked against your policy, and the resolved graph is scanned against the
OSV advisory database. All of it runs over the same dependency graph the build already computed.

[Jenesis Repository](https://jenesis.build/repository/) is the other half of the same concern, on the serving
side: a repository you run yourself, which stores every artifact by its content hash and serves it under the
Maven layout, the module layout and the OCI protocol at once, so what a build resolves is something you
control and can account for.

## Where this comes from

Jenesis was initiated by [Rafael Winterhalter](https://github.com/raphw), who also wrote
[Byte Buddy](https://bytebuddy.net), the code generation and manipulation library that is downloaded over five
billion times a year and that Oracle recognised with a Duke's Choice award in 2015.

Maintaining a library that far down the dependency graph is a long lesson in how software actually reaches the
machines that run it. A tool that central is distributed through the same pipeline as everything else, and the
integrity of that pipeline is mostly convention: a coordinate resolved at build time, a repository trusted by
default, an artifact nobody checks against what its author published. Java deserves better than that, and the
module system already gives the language the vocabulary to say what a program is made of.

That is the effort here: to make the toolchain around Java honest about what it builds and where the pieces
came from, from the build that resolves them to the repository that serves them, and to leave the ecosystem a
little better equipped than it was.
