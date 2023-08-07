---
title: "mach opus"
description: "Opus audio decoding and encoding for Zig via the battle-hardened xiph.org libopus"
draft: false
layout: "docs"
docs_type: "pkg"
rss_ignore: true
---

<div style="display: flex; flex-direction: column; justify-content: space-between; align-items: center; margin-bottom: 1rem;">
    <picture>
        <source media="(prefers-color-scheme: dark)" srcset="/assets/mach/opus-full-dark.svg">
        <img alt="mach-opus" src="/assets/mach/opus-full-light.svg" style="height: 7rem; margin-top: 1rem;">
    </picture>
    <a href="https://github.com/hexops/mach-opus">GitHub repository</a>
</div>

Opus audio decoding and encoding for Zig via the battle-hardened xiph.org libopus

## Experimental

This is an **experimental** project according to [our stability guarantees](../../about/stability):

> When a project has an experimental warning, it means all bets are off. You should carefully read the warning to understand why the project is experimental, and assume the worst.

**Status:** Ready for use, but docs are not great. We're considering if opus is the right format for Mach.

## Getting started

Create a `build.zig.zon` in your project (replace `LATEST_COMMIT` with the latest commit hash):

```zig
.{
    .name = "mypkg",
    .version = "0.1.0",
    .dependencies = .{
        .mach_opus = .{
            .url = "https://pkg.machengine.org/mach-opus/LATEST_COMMIT.tar.gz",
        },
    },
}
```

Run `zig build` in your project, and the compiler instruct you to add a `.hash = "..."` field next to `.url`:

```
note: expected .hash = "12209838fcfb7a77d2d6931efdc7448c033a1b7dad11d082c94bbeeba9d1038cd311",
```

Then use the dependency in your `build.zig`:

```zig
pub fn build(b: *std.Build) void {
    ...
    exe.addModule("mach-opus", b.dependency("mach_opus", .{
        .target = target,
        .optimize = optimize,
    }).module("mach-opus"));
}
```

You can now use it in your `src/main.zig` file:

```zig
const opus = @import("mach-opus");
```

### Issues? Questions?

Triple-check you followed the `build.zig.zon` instructions correctly, it's easy to mess that part up.

Feel free to join the [Mach Discord community](../../discord) for help.