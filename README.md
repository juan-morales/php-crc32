# php-crc32

by [Andrew Brampton](https://bramp.net)

Simple CRC32 implementations, that support all crc32 polynomials, as 
well as (if you compile it) hardware accelerated versions of CRC32C (Castagnoli).

# Usage

```php
require('crc32.php');

$crc = $crc = CRC32::create(CRC32::CASTAGNOLI);
$crc->update('hello');
echo $crc->hash();
```

Depending on the environment and the polynomial, `CRC32::create` will choose the fastest available verison, and return one of the following classes:

* `CRC32_PHP` - A pure PHP implementation.
* `CRC32_Builtin` - A [PHP Hash framework](http://php.net/manual/en/book.hash.php) implementation.
* `CRC32C_Google` - A Hardware Acceleration implementation.

# Hardware Acceleration

The hardware acceleration version makes use of the highly optomised [google/crc32c](https://github.com/google/crc32c) project, which is compiled into a PHP extension.

You'll need to add `extension=crc32c.so` to your primary php.ini file.

## Compile
```
brew install crc32c

./buildconf && \
./configure --with-crc32c=/Users/bramp/homebrew/Cellar/crc32c/1.0.7/ && \
make test TESTS=ext/crc32c/tests
```

# Benchmark

For the `CRC32C` polynomials, we compare the three different implementations.

```shell
$ php crc32_benchmark.php 

TODO
native: 12.54 MB/s
purephp: 6.09 MB/s
```

# Related

* https://bugs.php.net/bug.php?id=71890

# TODO

[ ] Test if this works on 32 bit machine.

# Licence (Apache 2)

* This is not an official Google product (experimental or otherwise), it is just code that happens to be owned by Google. *

```
Copyright 2019 Google Inc. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```