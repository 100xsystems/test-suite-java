# @100xsystems/test-suite-java

Shared JUnit 5 test helpers for 100xSystems Java curriculum.

Eliminates boilerplate duplication across lesson test files — the Java equivalent of [@100xsystems/test-suite-typescript](https://github.com/100xsystems/test-suite-typescript).

## What's Included

| Helper | Type | Description |
|--------|------|-------------|
| `BaseTest` | Abstract class | Extend this in lesson tests. Provides assertions, helpers, temp dir utilities |
| `FileHelper` | Static utility | File existence checks, content reading, directory listing |
| `BuildHelper` | Static utility | Maven compile/test execution, command running |

## Usage

Add the dependency to your lesson's `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>com.100xsystems</groupId>
        <artifactId>test-suite-java</artifactId>
        <version>0.1.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

Then in your lesson test file:

```java
import com.systems.testhelper.BaseTest;
import org.junit.jupiter.api.Test;

class Lesson1Test extends BaseTest {

    @Test
    void hasPomXml() {
        assertFileExists("pom.xml");
    }

    @Test
    void hasMainClass() {
        assertFileExists("src/main/java/com/claudecode/Main.java");
    }

    @Test
    void buildSucceeds() {
        expectBuildSucceeds();
    }

    @Test
    void pomHasPicocli() {
        assertFileContains("pom.xml", "picocli");
    }
}
```

## Available Helpers (from BaseTest)

### File Assertions
- `assertFileExists(path)` — file exists check
- `assertFileNotExists(path)` — file does not exist
- `assertDirExists(path)` — directory exists
- `assertFileContains(path, substring)` — content substring check
- `assertFileNotContains(path, substring)` — content absence check
- `assertFileMatches(path, regex)` — content regex match
- `assertFileHasContent(path)` — non-empty file check

### File Reading
- `readFile(path)` — read UTF-8 content
- `readJsonString(path)` — read and validate JSON

### Build Verification
- `expectBuildSucceeds()` — run `mvn compile` and assert success
- `runCommand(command)` — run any shell command
- `runMavenCompile()` / `runMavenTest()` — Maven lifecycle commands

### Temp Directory Helpers
- `withTempDir(fn)` — create, use, and clean up a temp directory
- `withTempFile(name, content, fn)` — create, write, use, and clean up

## Publishing

```bash
# Set up GitHub token in ~/.m2/settings.xml
# Then:
mvn deploy
```

## License

MIT
