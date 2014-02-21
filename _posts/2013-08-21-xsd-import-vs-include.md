---
layout: post
title: "XSD: import vs. include"
excerpt: ""
tags:
  - xsd
---
Something to keep in mind when trying to use common elements across multiple schemas is that you need to `include` them rather than `import` them. Make sure you don't add a default namespace to the file you're `import`ing, which will allow the elements to inherit the namespace of the file they're being imported to. And make sure you set a namespace for the importing file, otherwise you'll see an error like the following:

> References from this schema to components in no namespace are not allowed,
> since not indicated by an import statement.

If this happens, ensure you've set a default namespace on your importing XSD and that it's the same as the `targetNamespace`.
