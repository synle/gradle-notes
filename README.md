# gradle-notes

### Gradle Wrapper
https://docs.gradle.org/current/userguide/gradle_wrapper.html

```bash
gradle wrapper
gradle wrapper --gradle-version 7.4.2 --distribution-type all
```

### Add a task that depends on another task
```
tasks.register("citest") {
}
citest.dependsOn ':test'
```

### Hooking up unit test

#### Depdendencies

```
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter-api:5.8.2'
}
```

#### Test Task
```
test {
    useJUnitPlatform()

    testLogging {
        events "PASSED", "SKIPPED", "FAILED", "STANDARD_OUT", "STANDARD_ERROR"
    }
}
```

#### Sample Test Code
Below are sample unit tests
`src/test/java/com/example/MyTest.java`

```java
package com.example;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

@SpringBootApplication
public class MyTest {
  @Test
  public void testOne() throws Exception {
    int a = 10;
    int b = 20;
    int actual = 30;

    assertEquals(actual, 30);
  }

  @Test
  public void testTwo() {
      System.out.println("This test method should be run");
  }
}
```


### [checkstyle (linting)](https://checkstyle.sourceforge.io/)

`./gradlew check`

```
apply plugin: 'checkstyle'

checkstyle {
  toolVersion "8.1"
  config = rootProject.resources.text.fromFile('checkstyle.xml')
}
```


### [PMD (code analyzer)](https://pmd.github.io)

`./gradlew pmdMain` or `./gradlew pmdTest`

```
apply plugin: 'pmd'

pmd {
  toolVersion "6.7.0"
  ruleSets = []
  ruleSetFiles = files('pmd-ruleset.xml')
}
```

### [jacoco code coverage](https://www.eclemma.org/jacoco/)

`./gradlew jacocoTestReport` or `./gradlew jacocoTestCoverageVerification`

```
apply plugin: 'jacoco'

// jacoco configs
jacoco {
  toolVersion = "0.8.5"
}

jacocoTestReport {
  reports {
    xml.enabled true
    html.enabled true
  }
}

jacocoTestCoverageVerification {
  violationRules {
    rule {
      limit {
        minimum = 0.01
      }
    }
  }
}
```
