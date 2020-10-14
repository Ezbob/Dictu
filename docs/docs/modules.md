---
layout: default
title: Modules
nav_order: 11
---

# Modules
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Modules

Modularity is important in any project, and a project in Dictu is obviously no exception to this rule. Dictu solves this problem
by breaking files up into "modules". Every file is it's own module, and each module has it's own namespace, this means
a variable defined in `file.du` will not overwrite a variable in `file1.du` if imported.

### Importing

#### Standard library

When you wish to import a module from the standard library you use the import keyword. Importing from the standard library
is slightly different to importing a user created script (see below).

```cs
import Math;

Math.PI; // 3.14... 
```

#### User created scripts

When you wish to import another Dictu script, you use the import keyword. This takes an optional identifier which will be the
identifier of the module being imported. This is different to importing from the standard library as a string path is passed rather
than an identifier.

```cs
// Module not imported into current namespace, however the code in "some/file.du" is still ran.
import "some/file.du";

// This will import the module into the current namespace under the SomeModule identifier.
import "some/file.du" as SomeModule;
```

When importing a module with an identifer, you can access the top level module variables using the `.` operator, much
like you would for a class.

**some/file.du**
```cs
var x = 10;

def test() {
    return "test";
}
```

**main.du**
```cs
import "some/file.du" as SomeModule;

print(SomeModule.x); // 10
print(SomeModule.test()); // "test"
```

Once an module has been imported, it is stored within the VM, and is not executed again even if it is imported elsewhere.
What happens is the module is "loaded" again, which means if it was to change in the time from import, it will not be changed
within your program even if re-importing the module.