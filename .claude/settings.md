# Project Context: spark-java25-au-naturel

## Overview

This is a fork of [spark](https://github.com/lucko/spark) by lucko, modified to support Java 25 and newer JVM versions.

## Project Structure

```
spark-java25-au-naturel/
├── spark-api/          # Public API (MIT licensed)
├── spark-common/       # Shared code for all platforms
├── spark-forge/        # Minecraft Forge mod
├── spark-fabric/       # Minecraft Fabric mod (disabled)
├── spark-bukkit/       # Bukkit/Spigot plugin
├── spark-paper/        # Paper plugin
├── spark-bungeecord/   # BungeeCord proxy plugin
├── spark-velocity/     # Velocity proxy plugin
├── spark-sponge*/      # Sponge plugins
└── spark-neoforge/     # NeoForge mod
```

## Build System

- **Gradle 8.14.3** with Java 21 toolchain
- Build command: `JAVA_HOME=/path/to/jdk-21 ./gradlew :spark-forge:build --no-daemon`
- Output: `spark-forge/build/libs/spark-X.X.X-forge.jar`

## Key Files Modified from Original

### Async-profiler Integration
- `spark-common/src/main/java/me/lucko/spark/common/sampler/async/jfr/JfrReader.java` - Rewritten for v4.x format
- `spark-common/src/main/java/me/lucko/spark/common/sampler/async/jfr/Dictionary.java` - Updated key handling
- `spark-common/src/main/java/me/lucko/spark/common/sampler/async/AsyncProfilerAccess.java` - Removed Java 25 check
- Native libraries in `spark-common/src/main/resources/spark/` - v4.2.1

### Bug Fixes
- `spark-common/src/main/java/me/lucko/spark/common/sampler/java/JavaSampler.java` - Race condition fix
- `spark-common/src/main/java/me/lucko/spark/common/sampler/async/AsyncSampler.java` - Rotation race condition fix
- `spark-common/src/main/java/me/lucko/spark/common/sampler/BackgroundSamplerManager.java` - Disabled by default

### Forge Compatibility
- `spark-forge/build.gradle` - Targets Forge 1.20.1-47.4.10
- `spark-forge/src/main/java/me/lucko/spark/forge/plugin/ForgeServerSparkPlugin.java` - Deferred command registration
- `spark-forge/src/main/java/me/lucko/spark/forge/plugin/ForgeClientSparkPlugin.java` - Fixed initialization timing

## Dependencies

| Package | Version |
|---------|---------|
| async-profiler | 4.2.1 (tools.profiler:async-profiler:4.2) |
| ByteBuddy | 1.17.5 |
| ASM | 9.9 |

## Common Tasks

### Building for Forge
```bash
JAVA_HOME=/path/to/jdk-21 ./gradlew :spark-forge:build --no-daemon
```

### Testing
- Test on Java 21 for regression
- Test on Java 25 for new functionality
- Verify `/spark profiler` and `/sparkc profiler` commands work

## License

GPL v3 - All modifications must remain open source.
