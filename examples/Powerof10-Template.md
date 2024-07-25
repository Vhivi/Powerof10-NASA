# The Power of 10: Rules for Developing Safety-Critical Code (Adaptation for {proglang} Programming)

- [The Power of 10: Rules for Developing Safety-Critical Code (Adaptation for {proglang} Programming)](#the-power-of-10-rules-for-developing-safety-critical-code-adaptation-for-proglang-programming)
  - [1. **Restrict control flow to very simple constructs**](#1-restrict-control-flow-to-very-simple-constructs)
  - [2. **Give all loops a fixed upper bound**](#2-give-all-loops-a-fixed-upper-bound)
  - [3. **Do not use dynamic memory allocation after initialization**](#3-do-not-use-dynamic-memory-allocation-after-initialization)
  - [4. **No function should be longer than a single sheet of paper**](#4-no-function-should-be-longer-than-a-single-sheet-of-paper)
  - [5. **The density of assertions in code should be at least two assertions per function**](#5-the-density-of-assertions-in-code-should-be-at-least-two-assertions-per-function)
  - [6. **Declare all data objects at the smallest possible level of scope**](#6-declare-all-data-objects-at-the-smallest-possible-level-of-scope)
  - [7. **Every calling function must check the return value of non-void functions, and every called function must check the validity of all parameters provided by the caller**](#7-every-calling-function-must-check-the-return-value-of-non-void-functions-and-every-called-function-must-check-the-validity-of-all-parameters-provided-by-the-caller)
  - [8. **Limit the use of the preprocessor to file inclusions and simple macro definitions**](#8-limit-the-use-of-the-preprocessor-to-file-inclusions-and-simple-macro-definitions)
  - [9. **Restrict the use of pointers**](#9-restrict-the-use-of-pointers)
  - [10. **All code must be compiled with all compiler warnings enabled at the most pedantic level available**](#10-all-code-must-be-compiled-with-all-compiler-warnings-enabled-at-the-most-pedantic-level-available)

## 1. **Restrict control flow to very simple constructs**

**Original rule:** Do not use `goto`, `setjmp`, or `longjmp` statements, nor direct or indirect recursion.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 2. **Give all loops a fixed upper bound**

**Original rule:** It must be trivially possible for a checking tool to statically prove that the loop cannot exceed a predefined upper bound.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 3. **Do not use dynamic memory allocation after initialization**

**Original rule:** Avoid the use of `malloc` and garbage collectors.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 4. **No function should be longer than a single sheet of paper**

**Original rule:** Limit functions to approximately 60 lines of code.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 5. **The density of assertions in code should be at least two assertions per function**

**Original rule:** Use assertions to check for abnormal conditions that should never occur in real execution.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 6. **Declare all data objects at the smallest possible level of scope**

**Original rule:** Limit the scope of variables to avoid unintended side effects.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 7. **Every calling function must check the return value of non-void functions, and every called function must check the validity of all parameters provided by the caller**

**Original rule:** Check the return value of all functions and the validity of parameters.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 8. **Limit the use of the preprocessor to file inclusions and simple macro definitions**

**Original rule:** Limit the use of the preprocessor to file inclusions and simple macro definitions.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 9. **Restrict the use of pointers**

**Original rule:** Use at most one level of dereferencing.

**{proglang} adaptation:** Adapt the rule to the specific constructs of the language.

:warning: Example to avoid :warning:

```{proglang}
```

:heavy_check_mark: Recommended example :heavy_check_mark:

```{proglang}
```

| :warning: Example to avoid :warning: | :heavy_check_mark: Recommended example :heavy_check_mark: |
|--|--|
|  |  |
|  |  |
|  |  |

## 10. **All code must be compiled with all compiler warnings enabled at the most pedantic level available**

**Original rule:** All code must be compiled without warnings and analyzed daily with at least one static code analyzer.

**{proglang} adaptation:** If possible, put here any static code analyzer that can be used with the language.

[Link or badge to the static code analyzer](https://www.example.com)

These adaptations of NASA rules in {proglang} aim to ensure code quality, readability, and maintainability while adhering to principles of critical software development.
