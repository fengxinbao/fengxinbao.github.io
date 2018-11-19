---
layout: post
categories: osgi
---
Modularity is an important aspect of large Java systems. Build scripts and projects are often split up into modules in order to improve the build, but this is rarely taken into account at runtime.

In the second of the Modular Java series, we'll cover static modularity. We'll describe how to create bundles, how to install them into an OSGi engine and how to set up (versioned) dependencies between bundles. In the next episode, we'll look at dynamic modularity and show how bundles can react to other bundles coming and going.

As covered last time in [Modular Java: What Is It?](http://www.infoq.com/articles/modular-java-what-is-it), Java has always had packages as a unit of modularity at development time, and JARs as a unit of modularity at deployment time. However, although build tools like Maven guarantee a certain combination of packages and JARs at compile time, these dependencies may be inconsistent with the runtime classpath. To solve this problem, modules can declare their dependency requirements so that, at runtime, they can be checked prior to execution.

OSGi is a runtime dynamic module system for Java. Specifications describe the behaviour of how the OSGi runtime works; the current release is OSGi R4.2 (as covered by InfoQ previously).

An OSGi module (also known as a bundle) is just a simple JAR file, with additional information in the archive's MANIFEST.MF. At a minimum, each bundle's manifest must contain:


- Bundle-ManifestVersion: must be 2 for OSGi R4 bundles (otherwise defaults to 1 for OSGi R3 bundles)
- Bundle-SymbolicName: textual identifier of the bundle, often in reverse domain name format such as com.infoq and frequently corresponds to the packages contained therein
- Bundle-Version: a version of the form major.minor.micro.qualifier where the first three elements are numeric (defaulting to 0) and qualifier is textual (defaulting to the empty string)

# Creating a bundle

The simplest bundle contains purely a manifest file as follows:

    Bundle-ManifestVersion: 2
    Bundle-SymbolicName: com.infoq.minimal
    Bundle-Version: 1.0.0

That wouldn't be tremendously exciting to create, however, so let's create one with an activator. This is an OSGi-specific piece of code which is invoked when the bundle is started, like a per-bundle main method.

```java
package com.infoq;
import org.osgi.framework.*;
public class ExampleActivator implements BundleActivator {
  public void start(BundleContext context) {
    System.out.println("Started");
  }
  public void stop(BundleContext context) {
    System.out.println("Stopped");
  }
}
```

In order for OSGi to know which class is the activator, we need to add two extra items to the manifest:

	Bundle-Activator: com.infoq.ExampleActivator
	Import-Package: org.osgi.framework




