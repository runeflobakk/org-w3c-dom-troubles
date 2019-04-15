# Bundling classes from org.w3c.dom

There are certain artifacts which bundle a tiny amount of classes/interfaces from the `org.w3c.dom` package, and they will cause problems. In particular, if you have any of these on your classpath, you may encounter compile errors with your own code trying to refer to anything under the `org.w3c.dom` package:

- Jaxen 1.1.6 (should be fixed in [1.2.0](https://github.com/jaxen-xpath/jaxen/releases/tag/v1.2.0))
- xom 1.2.5
- xercesImpl 2.8.0

Ref: https://bugs.eclipse.org/bugs/show_bug.cgi?id=536928#c73



# Error in Eclipse Photon 4.11 Java editor (fixed in 4.12M1)

**The issue described below is verified fixed in version 4.12M1:
https://bugs.eclipse.org/bugs/show_bug.cgi?id=545687**




This project isolates a certain aspect of this issue:
[bugs.eclipse.org/bugs/show_bug.cgi?id=536928](https://bugs.eclipse.org/bugs/show_bug.cgi?id=536928)

Eclipse refuses to compile source code which references `w3c.org.dom.*` with `xml-apis` present on classpath:

![compile error](compile-error.png)

This compiles fine with javac. Excluding `xml-apis` from classpath will make the source compile also with the Eclipse compiler. But it seems like the error is still present _in the editor view_ even after excluding `xml-apis` as a transitive dependency of e.g. `xercesImpl`, but the "red markers" disappears from the Project Explorer view. Eclipse manages to compile the source code, even though the editor shows errors.

## With xml-apis on classpath

![editor-error](editor-error.png) ![explorer-with-xmlapis](explorer-with-xmlapis.png)


## Without xml-apis on classpath

![editor-error](editor-error.png) ![explorer-without-xmlapis](explorer-without-xmlapis.png)
