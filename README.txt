Project Title: JUnit4 and Maven Example
Description: A minimal example. Demonstrates how to use JUnit4 and Maven
Project URL: git://github.com/sastay/JUnit4-and-Maven-Example.git

Author: Sascha Tayefeh
Author URL: http://www.tayefeh.de
Date: 2010-07-10

When I migrated an old project from JUnit3 to JUnit4, I ran into some problems.
mvn:test produced an error:

[SNIP START]
---------------------------------------------
junit.framework.AssertionFailedError: No tests found in minimal.DoSomeActionTest
---------------------------------------------
[SNIP STOP]

The test classes were no longer available. I found that I had to

1. remove inheritance from :TestCase() and annotate all test methods with @Test

This project provides a trivial scenario (refer to src/test/java/minimal/DoSomeActionTest.java):

[SNIP START]
---------------------------------------------
package minimal;

import static org.junit.Assert.assertTrue;
import org.junit.Test;

/**
 * Trivial test class. Demonstrates the syntax of JUnit4.
 * Important: Do NOT inherit this class from TestCase() or JUnit3.x is enforced
 *
 * @author Sascha Tayefeh
 */
public class DoSomeActionTest {
    @Test
    public void testIsThisReallyTrue() {
        assertTrue(true);
    }
}
---------------------------------------------
[SNIP STOP]

Also mind the pom.xml which includes the maven-compiler-plugin
to enforce Java 1.6 incl. annotations:

[SNIP START]
---------------------------------------------
     <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-compiler-plugin</artifactId>
         <version>2.3.1</version>
         <configuration>
             <source>1.6</source>
             <target>1.6</target>
             <encoding>UTF-8</encoding>
         </configuration>
     </plugin>
---------------------------------------------
[SNIP STOP]

When running mvn:test you should get following positive message:

[SNIP START]
---------------------------------------------
-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running minimal.DoSomeActionTest
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.047 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESSFUL
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2 seconds
[INFO] Finished at: Mon Jul 12 17:22:44 CEST 2010
[INFO] Final Memory: 10M/19M
[INFO] ------------------------------------------------------------------------
---------------------------------------------
[SNIP STOP]

Ref: 
1. http://www.junit.org 
2. http://www.tayefeh.de/2010/07/junit4-and-maven-minimal-example
