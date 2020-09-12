
# Speed up your Python using Rust

![brocha](https://developers.redhat.com/blog/wp-content/uploads/2017/08/avatar_2017-150x150.jpg)

By  [Bruno Rocha](https://developers.redhat.com/blog/author/brocha/ "Bruno Rocha")  November 16, 2017

![Speed up your Python using Rust](https://developers.redhat.com/blog/wp-content/uploads/2017/11/rustpy-e1510683503342.png)

## What is Rust?

**Rust** is a systems programming language that runs blazingly fast, prevents segfaults, and guarantees thread safety.

**Featuring**

-   zero-cost abstractions
-   move semantics
-   guaranteed memory safety
-   threads without data races
-   trait-based generics
-   pattern matching
-   type inference
-   minimal runtime
-   efficient C bindings

  
Description is taken from [rust-lang.org](http://rust-lang.org/).

## [](https://github.com/rochacbruno/rust-python-example#why-does-it-matter-for-a-python-developer)Why does it matter for a Python developer?

The better description of Rust I heard from [**Elias**](https://github.com/dlight) (a member of the [**Rust Brazil Telegram Group)**](https://t.me/rustlangbr).

> **Rust is** a language that allows you to build high level abstractions, but without giving up low-level control – that is, control of how data is represented in memory, control of which threading model you want to use etc.  
> **Rust is** a language that can usually detect, during compilation, the worst parallelism and memory management errors (such as accessing data on different threads without synchronization, or using data after they have been deallocated), but gives you a hatch escape in the case you really know what you’re doing.  
> **Rust is** a language that, because it has no runtime, can be used to integrate with any runtime; you can write a native extension in Rust that is called by a program node.js, or by a python program, or by a program in ruby, lua etc. and, however, you can script a program in Rust using these languages. — “Elias Gabriel Amaral da Silva”

There is a bunch of Rust packages out there to help you extending Python with Rust.

I can mention [Milksnake](https://github.com/getsentry/milksnake) created by Armin Ronacher (the creator of Flask) and also [PyO3](https://github.com/PyO3/pyo3) The Rust bindings for Python interpreter.  

#### Everything you need to grow your career.

With your free Red Hat Developer program membership, unlock our library of cheat sheets and ebooks on next-generation application development.

[SIGN UP](http://developers.redhat.com/register?intcmp=701f2000001ODrzAAG "Everything you need to grow your career.")

[![](https://developers.redhat.com/blog/wp-content/themes/rhd-frontend-blog-theme/inc/promos/images/bookshelf-mixed-v2.png "Everything you need to grow your career.")](http://developers.redhat.com/register?intcmp=701f2000001ODrzAAG "Everything you need to grow your career.")

### _See a complete reference list at the bottom of this article._

Let’s **see it in action**

For this post, I am going to use [Rust Cpython](https://github.com/dgrunwald/rust-cpython), it’s the only one I have tested, it is compatible with stable version of Rust and found it straightforward to use.

> **NOTE**:  [PyO3](https://github.com/PyO3/pyo3)  is a fork of rust-cpython, comes with many improvements, but works only with the nightly version of Rust, so I prefered to use the stable for this post, anyway the examples here must work also with PyO3.

**Pros:** It is easy to write Rust functions and import from Python and as you will see by the benchmarks it worth in terms of performance.

**Cons:** The distribution of your **project/lib/framework** will demand the Rust module to be compiled on the target system because of variation of environment and architecture, there will be a **compiling** stage which you don’t have when installing Pure Python libraries, you can make it easier using [rust-setuptools](https://pypi.python.org/pypi/setuptools-rust) or using the [MilkSnake](https://github.com/getsentry/milksnake) to embed binary data in Python Wheels.

## [](https://github.com/rochacbruno/rust-python-example#python-is-sometimes-slow)Python is sometimes slow

Yes, Python is known for being “slow” in some cases and the good news is that this doesn’t really matter depending on your project goals and priorities. For most projects, this detail will not be very important.

However, you may face the **rare** case where a single function or module is taking too much time and is detected as the bottleneck of your project performance, often happens with string parsing and image processing.

## [](https://github.com/rochacbruno/rust-python-example#example)Example

Let’s say you have a Python function which does a string processing, take the following easy example of `counting pairs of repeated chars`, but have in mind that this example can be reproduced with other `string processing` functions or any other generally slow process in Python.

# How many subsequent-repeated group of chars are in the given string? 
abCCdeFFghiJJklmnopqRRstuVVxyZZ... {millions of chars here}
  1   2    3        4    5   6

Python is slow for doing large  `string` processing, so you can use `pytest-benchmark` to compare a `Pure Python (with Iterator Zipping)` function versus a `Regexp` implementation.

# Using a Python3.6 environment
$ pip3 install pytest pytest-benchmark

Then write a new Python program called `doubles.py`

import re
import string
import random

# Python ZIP version
def count_doubles(val):
    total = 0
    # there is an improved version later on this post
    for c1, c2 in zip(val, val[1:]):
        if c1 == c2:
            total += 1
    return total

# Python REGEXP version
double_re = re.compile(r'(?=(.)\1)')

def count_doubles_regex(val):
    return len(double_re.findall(val))

# Benchmark it
# generate 1M of random letters to test it
val = ''.join(random.choice(string.ascii_letters) for i in range(1000000))

def test_pure_python(benchmark):
    benchmark(count_doubles, val)

def test_regex(benchmark):
    benchmark(count_doubles_regex, val)

Run **pytest** to compare:

$ pytest doubles.py                                                                                                           
=============================================================================
platform linux -- Python 3.6.0, pytest-3.2.3, py-1.4.34, pluggy-0.4.
benchmark: 3.1.1 (defaults: timer=time.perf_counter disable_gc=False min_roun
rootdir: /Projects/rustpy, inifile:
plugins: benchmark-3.1.1
collected 2 items

doubles.py ..


-----------------------------------------------------------------------------
Name (time in ms)         Min                Max               Mean          
-----------------------------------------------------------------------------
test_regex            24.6824 (1.0)      32.3960 (1.0)      27.0167 (1.0)    
test_pure_python      51.4964 (2.09)     62.5680 (1.93)     52.8334 (1.96)   
-----------------------------------------------------------------------------

Lets take the `Mean` for comparison:

-   **Regexp** – 27.0167 **<– less is better**
-   **Python Zip** – 52.8334

# [](https://github.com/rochacbruno/rust-python-example#extending-python-with-rust)Extending Python with Rust

## [](https://github.com/rochacbruno/rust-python-example#create-a-new-crate)Create a new crate

> **crate** is how we call Rust Packages.

Having rust installed (recommended way is [https://www.rustup.rs/](https://www.rustup.rs/)) Rust is also available on Fedora and RHEL repositories by the [rust-toolset](https://developers.redhat.com/blog/2017/11/01/getting-started-rust-toolset-rhel/)

> I used `rustc 1.21.0`

In the same folder run:

cargo new pyext-myrustlib

It creates a new Rust project in that same folder called `pyext-myrustlib` containing the `Cargo.toml` (cargo is the Rust package manager) and also a `src/lib.rs` (where we write our library implementation).

## [](https://github.com/rochacbruno/rust-python-example#edit-cargotoml)Edit Cargo.toml

It will use the `rust-cpython` crate as dependency and tell cargo to generate a `dylib` to be imported from Python.

[package]
name = "pyext-myrustlib"
version = "0.1.0"
authors = ["Bruno Rocha <rochacbruno@gmail.com>"]

[lib]
name = "myrustlib"
crate-type = ["dylib"]

[dependencies.cpython]
version = "0.1"
features = ["extension-module"]

## [](https://github.com/rochacbruno/rust-python-example#edit-srclibrs)Edit src/lib.rs

What we need to do:

1.  Import all macros from `cpython` crate.
2.  Take `Python` and `PyResult` types from CPython into our lib scope.
3.  Write the `count_doubles` function implementation in `Rust`, note that this is very similar to the Pure Python version except for:
    -   It takes a `Python` as first argument, which is a reference to the Python Interpreter and allows Rust to use the `Python GIL`.
    -   Receives a `&str` typed `val` as reference.
    -   Returns a `PyResult` which is a type that allows the rise of Python exceptions.
    -   Returns an `PyResult` object in `Ok(total)` (**Result** is an enum type that represents either success (Ok) or failure (Err)) and as our function is expected to return a `PyResult` the compiler will take care of **wrapping** our `Ok` on that type. (note that our PyResult expects a `u64` as return value).
4.  Using `py_module_initializer!` macro we register new attributes to the lib, including the `__doc__` and also we add the `count_doubles` attribute referencing our `Rust implementation of the function`.
    -   Attention to the names **lib**myrustlib, **initlib**myrustlib, and **PyInit.**
    -   We also use the `try!` macro, which is the equivalent to Python’s`try.. except`.
    -   Return `Ok(())` – The `()` is an empty result tuple, the equivalent of `None` in Python.

#[macro_use]
extern crate cpython;

use cpython::{Python, PyResult};

fn count_doubles(_py: Python, val: &str) -> PyResult<u64> {
    let mut total = 0u64;

    // There is an improved version later on this post
    for (c1, c2) in val.chars().zip(val.chars().skip(1)) {
        if c1 == c2 {
            total += 1;
        }
    }

    Ok(total)
}

py_module_initializer!(libmyrustlib, initlibmyrustlib, PyInit_myrustlib, |py, m | {
    try!(m.add(py, "__doc__", "This module is implemented in Rust"));
    try!(m.add(py, "count_doubles", py_fn!(py, count_doubles(val: &str))));
    Ok(())
});

## Now let’s build it with cargo

$ cargo build --release
    Finished release [optimized] target(s) in 0.0 secs

$ ls -la target/release/libmyrustlib*
target/release/libmyrustlib.d
target/release/libmyrustlib.so*  <-- Our dylib is here

Now let’s copy the generated `.so` lib to the same folder where our `doubles.py` is located.

> NOTE: on **Fedora** you must get a `.so` in other system you may get a `.dylib` and you can rename it changing extension to `.so`.

$ cd ..
$ ls
doubles.py pyext-myrustlib/

$ cp pyext-myrustlib/target/release/libmyrustlib.so myrustlib.so

$ ls
doubles.py myrustlib.so pyext-myrustlib/

> Having the `myrustlib.so` in the same folder or added to your Python path allows it to be directly imported, transparently as it was a Python module.

## [](https://github.com/rochacbruno/rust-python-example#importing-from-python-and-comparing-the-results)Importing from Python and comparing the results

Edit your `doubles.py` now importing our `Rust implemented` version and adding a `benchmark` for it.

import re
import string
import random
import myrustlib   #  <-- Import the Rust implemented module (myrustlib.so)

def count_doubles(val):
    """Count repeated pair of chars ins a string"""
    total = 0
    for c1, c2 in zip(val, val[1:]):
        if c1 == c2:
            total += 1
    return total


double_re = re.compile(r'(?=(.)\1)')

def count_doubles_regex(val):
    return len(double_re.findall(val))


val = ''.join(random.choice(string.ascii_letters) for i in range(1000000))

def test_pure_python(benchmark):
    benchmark(count_doubles, val)

def test_regex(benchmark):
    benchmark(count_doubles_regex, val)

def test_rust(benchmark):   #  <-- Benchmark the Rust version
    benchmark(myrustlib.count_doubles, val)

# Benchmark

$ pytest doubles.py
==============================================================================
platform linux -- Python 3.6.0, pytest-3.2.3, py-1.4.34, pluggy-0.4.
benchmark: 3.1.1 (defaults: timer=time.perf_counter disable_gc=False min_round
rootdir: /Projects/rustpy, inifile:
plugins: benchmark-3.1.1
collected 3 items

doubles.py ...


-----------------------------------------------------------------------------
Name (time in ms)         Min                Max               Mean          
-----------------------------------------------------------------------------
test_rust              2.5555 (1.0)       2.9296 (1.0)       2.6085 (1.0)    
test_regex            25.6049 (10.02)    27.2190 (9.29)     25.8876 (9.92)   
test_pure_python      52.9428 (20.72)    56.3666 (19.24)    53.9732 (20.69)  
-----------------------------------------------------------------------------

Lets take the `Mean` for comparison:

-   **Rust** – 2.6085 **<– less is better**
-   **Regexp** – 25.8876
-   **Python Zip** – 53.9732

Rust implementation can be **10x** faster than Python Regex and **21x** faster than Pure Python Version.

> Interesting that **Regex** version is only 2x faster than Pure Python  ![🙂](https://s.w.org/images/core/emoji/11.2.0/svg/1f642.svg)

> NOTE: That numbers makes sense only for this particular scenario, for other cases that comparison may be different.

# Updates and Improvements

After this article has been published I got some comments on [r/python](https://www.reddit.com/r/Python/comments/7dct9v/use_rust_to_write_python_modules/) and also on [r/rust](https://www.reddit.com/r/rust/comments/7dctmp/red_hat_developers_blog_speed_up_your_python/)

The contributions came as [Pull Requests](https://github.com/rochacbruno/rust-python-example/pulls?utf8=%E2%9C%93&q=is%3Apr) and you can send a new if you think the functions can be improved.

Thanks to: [Josh Stone](https://github.com/cuviper) we got a better implementation for Rust which iterates the string only once and also the Python equivalent.

Thanks to: [Purple Pixie](https://github.com/purple-pixie) we got a Python implementation using `itertools`, however this version is not performing any better and still needs improvements.

## [](https://github.com/rochacbruno/rust-python-example#iterating-only-once)Iterating only once

fn count_doubles_once(_py: Python, val: &str) -> PyResult<u64> {
    let mut total = 0u64;

    let mut chars = val.chars();
    if let Some(mut c1) = chars.next() {
        for c2 in chars {
            if c1 == c2 {
                total += 1;
            }
            c1 = c2;
        }
    }

    Ok(total)
}

def count_doubles_once(val):
    total = 0
    chars = iter(val)
    c1 = next(chars)
    for c2 in chars:
        if c1 == c2:
            total += 1
        c1 = c2
    return total

## [](https://github.com/rochacbruno/rust-python-example#python-with-itertools)Python with itertools

import itertools

def count_doubles_itertools(val):
    c1s, c2s = itertools.tee(val)
    next(c2s, None)
    total = 0
    for c1, c2 in zip(c1s, c2s):
        if c1 == c2:
            total += 1
    return total

### Why not C/C++/Nim/Go/Ĺua/PyPy/{other language}?

Ok, that is not the purpose of this post, this post was never about comparing `Rust` X `other language`, this post was specifically about **how to use Rust to extend and speed up Python** and by doing that it means you have a good reason to choose Rust instead of `other language` or by its ecosystem or by its safety and tooling or just to follow the hype, or simply because you like Rust doesn’t matter the reason, this post is here to show how to use it with **Python**.

I (personally) may say that Rust is more `future proof` as it is new and there are lots of improvements to come, also because of its ecosystem, tooling, and community and also because I feel comfortable with Rust syntax, I really like it!

So, as expected people started complaining about the use of other languages and it becomes a sort of benchmark, and I think it is cool!

So as part of my request for improvements some people on [Hacker News](https://news.ycombinator.com/item?id=15719254) also sent ideas, [martinxyz](https://github.com/martinxyz) sent an implementation using C and SWIG that performed very well.

C Code (swig boilerplate omitted)

uint64_t count_byte_doubles(char * str) {
  uint64_t count = 0;
  while (str[0] && str[1]) {
    if (str[0] == str[1]) count++;
    str++;
  }
  return count;
}

And our fellow Red Hatter [Josh Stone](https://github.com/cuviper) improved the Rust implementation again by replacing `chars` with `bytes` so it is a fair competition with `C` as C is comparing bytes instead of Unicode chars.

fn count_doubles_once_bytes(_py: Python, val: &str) -> PyResult<u64> {
    let mut total = 0u64;

    let mut chars = val.bytes();
    if let Some(mut c1) = chars.next() {
        for c2 in chars {
            if c1 == c2 {
                total += 1;
            }
            c1 = c2;
        }
    }

    Ok(total)
}

There are also ideas to compare Python `list comprehension` and `numpy` so I included here

Numpy:

import numpy as np

def count_double_numpy(val):
    ng=np.fromstring(val,dtype=np.byte)
    return np.sum(ng[:-1]==ng[1:])

List comprehension

def count_doubles_comprehension(val):
    return sum(1 for c1, c2 in zip(val, val[1:]) if c1 == c2)

The complete test case is on repository `test_all.py` file.

## [](https://github.com/rochacbruno/rust-python-example#new-results)New Results

**NOTE**: Have in mind that the comparison was done in the same environment and may have some differences if run in a different environment using another compiler and/or different tags.

-------------------------------------------------------------------------------------------------
Name (time in us)                     Min                    Max                   Mean          
-------------------------------------------------------------------------------------------------
**test_rust_bytes_once**             476.7920 (1.0)         830.5610 (1.0)         **486.6116 (1.0)**    
**test_c_swig_bytes_once**           795.3460 (1.67)      1,504.3380 (1.81)        **827.3898 (1.70)**   
test_rust_once                   985.9520 (2.07)      1,483.8120 (1.79)      1,017.4251 (2.09)   
**test_numpy**                     1,001.3880 (2.10)      2,461.1200 (2.96)      **1,274.8132 (2.62)**   
test_rust                      2,555.0810 (5.36)      3,066.0430 (3.69)      2,609.7403 (5.36)   
test_regex                    24,787.0670 (51.99)    26,513.1520 (31.92)    25,333.8143 (52.06)  
test_pure_python_once         36,447.0790 (76.44)    48,596.5340 (58.51)    38,074.5863 (78.24)  
**test_python_comprehension**     49,166.0560 (103.12)   50,832.1220 (61.20)    **49,699.2122 (102.13)** 
test_pure_python              49,586.3750 (104.00)   50,697.3780 (61.04)    50,148.6596 (103.06) 
test_itertools                56,762.8920 (119.05)   69,660.0200 (83.87)    58,402.9442 (120.02) 
-------------------------------------------------------------------------------------------------

-   The `new Rust implementation comparing bytes` is **2x better** than the old comparing Unicode `chars`
-   The `Rust` version is still better than the `C` using SWIG
-   `Rust` comparing `unicode chars` is still better than `numpy`
-   However `Numpy` is better than the `first Rust implementation` which had the problem of **double iteration over the unicode chars**
-   Using a `list comprehension` does not make significative difference than using `pure Python`

> NOTE: If you want to propose changes or improvements send a PR here: [https://github.com/rochacbruno/rust-python-example/](https://github.com/rochacbruno/rust-python-example/)

# [](https://github.com/rochacbruno/rust-python-example#conclusion)Conclusion

Back to the purpose of this post “How to Speed Up your Python with Rust” we started with:

– **Pure Python**  function taking  **102 ms.  
**– Improved with  **Numpy** (which is implemented in C) to take  **3 ms.  
**– Ended with **Rust**  taking  **1 ms.**

In this example  **Rust**  performed  **100x faster**  than our  **Pure** Python.

`Rust` will not magically save you, you must know the language to be able to implement the clever solution and once implemented in the right it worth as much as C in terms of performance and also comes with amazing tooling, ecosystem, community and safety bonuses.

`Rust` may not be **yet** the `general purpose language` of choice by its level of complexity and may not be the better choice yet to write common simple `applications` such as `web` sites and `test automation` scripts.

However, for `specific parts` of the project where Python is known to be the bottleneck and your natural choice would be implementing a `C/C++` extension, writing this extension in Rust seems easy and better to maintain.

There are still many improvements to come in Rust and lots of others crates to offer `Python <--> Rust` integration. Even if you are not including the language in your tool belt right now, it is really worth to keep an eye open to the future!

## [](https://github.com/rochacbruno/rust-python-example#credits)References

The code snippets for the examples showed here are available in GitHub repo: [https://github.com/rochacbruno/rust-python-example](https://github.com/rochacbruno/rust-python-example).

The examples in this publication are inspired by `Extending Python with Rust` talk by **Samuel Cormier-Iijima** in **Pycon Canada**. video here: [https://www.youtube.com/watch?v=-ylbuEzkG4M](https://www.youtube.com/watch?v=-ylbuEzkG4M).

Also by `My Python is a little Rust-y` by **Dan Callahan** in **Pycon Montreal**. video here: [https://www.youtube.com/watch?v=3CwJ0MH-4MA](https://www.youtube.com/watch?v=3CwJ0MH-4MA).

Other references:

-   [https://github.com/mitsuhiko/snaek](https://github.com/mitsuhiko/snaek)
-   [https://github.com/PyO3/pyo3](https://github.com/PyO3/pyo3)
-   [https://pypi.python.org/pypi/setuptools-rust](https://pypi.python.org/pypi/setuptools-rust)
-   [https://github.com/mckaymatt/cookiecutter-pypackage-rust-cross-platform-publish](https://github.com/mckaymatt/cookiecutter-pypackage-rust-cross-platform-publish)
-   [http://jakegoulding.com/rust-ffi-omnibus/](http://jakegoulding.com/rust-ffi-omnibus/)
-   [https://github.com/urschrei/polylabel-rs/blob/master/src/ffi.rs](https://github.com/urschrei/polylabel-rs/blob/master/src/ffi.rs)
-   [https://bheisler.github.io/post/calling-rust-in-python/](https://bheisler.github.io/post/calling-rust-in-python/)
-   [https://github.com/saethlin/rust-lather](https://github.com/saethlin/rust-lather)

**Join Community:**

Join Rust community, you can find group links in [https://www.rust-lang.org/en-US/community.html](https://www.rust-lang.org/en-US/community.html).

**If you speak Portuguese,** I recommend you to join [https://t.me/rustlangbr](https://t.me/rustlangbr) and there is the [http://bit.ly/canalrustbr](http://bit.ly/canalrustbr) on Youtube.

## [](https://github.com/rochacbruno/rust-python-example#author)Author

**Bruno Rocha**

-   Senior Quality Engineer at **Red Hat**
-   Teaching Python and Flask at  [CursoDePython.com.br](http://cursodepython.com.br/)
-   Fellow Member of Python Software Foundation
-   Member of RustBR study group

More info: [http://about.me/rochacbruno](http://about.me/rochacbruno) and [http://brunorocha.org](http://brunorocha.org/)

----------

**Where to go next—Develop on Red Hat Enterprise Linux**

-   [**How to install Python 3, pip, venv, virtualenv, and pipenv**](https://developers.redhat.com/blog/2018/08/13/install-python3-rhel/)
-   [**Install Rust via  `yum`  and build Hello World**](https://developers.redhat.com/products/clang-llvm-go-rust/hello-world/#fndtn-rust)

----------

**Whether you are new to Containers or have experience, downloading this** [**cheat sheet**](https://developers.redhat.com/promotions/docker-cheatsheet/) **can assist you when encountering tasks you haven’t done lately.**

---
# 为什么要用Rust取代C/C ++重写Python底层？

_198_

分享

Rust是Mozilla开发的注重性能和内存安全的语言，它的设计目的是逐渐取代C/C ++，但这个过程还需要一段时间。

值得肯定的是，Rust在现有阶段可以取代传统上部分C语言库。用于统计和机器学习的Python系统中的大部分内容都是用C语言编写而成的，所以模块被重写的可能性非常大。

![图0：为什么要用Rust取代C/C ++重写Python底层？](http://cdn.aqee.net/techug/uploads/2017/08/31cd0003c0a27b6f7223.gif "图0：为什么要用Rust取代C/C ++重写Python底层？")

虽然Rust是编译型语言，Python是解释型语言，但是由于两者的ABI(应用程序二进制接口)在设计上存在相似性，Rust代码可以应用到Python上。现在一些Rust包已经被用于Python绑定，通过Rust库也可以将C语言的API应用到Python上。

大量新项目的应用使得开发Rust库更容易，方便绑定Python和部署具有Rust二进制文件的Python软件包。下面4个项目的实际应用，说明结合Python与Rust在一定程度上完全可以取代C/C ++。

## **Rust-CPython**

定义：Rust-Cpython就是在Rust中CPython运行时的一组绑定，Rust程序连接到CPython上，使用它的ABI来运行Python程序，在Rust环境下与Python的面向对象一起工作。

适用对象：熟练使用控制CPython的Rust程序员。需要注意的是，由于Python对象管理方式的问题，Rust的内存安全性能并不能完全发挥作用，所以使用要谨慎。

![图1：为什么要用Rust取代C/C ++重写Python底层？](http://cdn.aqee.net/techug/uploads/2017/08/31d00002e4ee5f78549c.gif "图1：为什么要用Rust取代C/C ++重写Python底层？")

## **PyO3**

[![](http://www.techug.com/wordpress/wp-content/uploads/2017/08/werqw.jpg)](https://shop162567423.taobao.com/)定义：对于Rust开发人员来讲，PyO3项目提供了两个方向的基本方法来编写绑定Python的Rust软件。Rust程序可以与Python对象和解释器接口，并且可以与C模块相同的方式将Rust应用到Python中。

PyO3支持的Python功能有限，但是实现最基本的功能还是可以的。PyO3惯用的Rust功能是通过装饰既有代码去实现Python-aware。

适用人员：那些编写与Python运行直接交互模块的程序员。

## **Snaek**

定义：在这个项目的早期阶段，Snaek允许开发人员根据需要创建加载Python动态的Rust库，但是这个Rust库不依赖于静态连接Python的运行。Rust库使用Snaek时，不需要专门针对Python进行编写，只公开C语言兼容的方法就可以了。但Snaek的一个潜在缺点是不能使用ctypes，ctypes是与C代码接口的标准Python库，它使用的是cffi。cffi是由PyPy团队开发的一个备选库，学习cffi并不难，但如果真的要使用cffi，一些已经使用ctypes的项目都需要重写。

适用人员：将Rust写入的方法应用到Python脚本中或想对Python做进一步了解的Rust程序员。

![图2：为什么要用Rust取代C/C ++重写Python底层？](http://cdn.aqee.net/techug/uploads/2017/08/31cc00018a1868f8ea25.gif "图2：为什么要用Rust取代C/C ++重写Python底层？")

## **Cookiecutter**

定义：这个项目涉及将二进制模块与Python库绑定时出现的常见问题。Cookiecutter从模板创建Python项目，可用的模板Cookiecutter PyPackage Rust Cross-Platform Publish简化了将Rust二进制文件与Python库捆绑在一起的过程。

这个项目非常重要的目标是能够生成二进制分发（Wheel），这样就不需要最终用户自己编译Rust代码。Windows用户经常因为缺乏预编译的Windows二进制Python包在工作中受阻，所以这个项目应该是非常受欢迎的。

适用人员：那些用Rust绑定创建许多Python项目或试图发布项目的程序员。

---



