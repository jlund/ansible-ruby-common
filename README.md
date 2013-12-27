ruby-common
========

Ansible role that compiles and installs Ruby (https://www.ruby-lang.org) and Bundler (http://bundler.io). This role is generic enough to support any version of Ruby, and it is best used in conjunction with another role that supplies the required variables and that depends on this common base.

Role Variables
--------------

**Variables that *must* be set by the user (or another role)**

    ruby_version: This variable controls the version of Ruby that will be compiled and installed. It should correspond with the tarball filename excluding the ".tar.gz2" extension (e.g. "ruby-1.9.3-p484").

    ruby_checksum: The SHA256 checksum of the gzipped tarball that will be downloaded and compiled.

    ruby_download_location: The URL that the tarball should be retrieved from. Using the ruby_version variable within this variable is a good practice (e.g. "http://cache.ruby-lang.org/pub/ruby/1.9/{{ ruby_version }}.tar.gz").

**Variables that *can* be set by the user (or another role)**

    rails_env: This role includes a convenient shell script that lets you invoke Rake commands using Bundler with the proper RAILS_ENV environment variable set. This script is placed in /usr/local/bin/rake-env. This can be useful in other tasks (e.g. if you wanted to run a Rake task using the command module). This variable is used to control the Rails environment for this script and is set to "production" by default.

This role also includes a GC wrapper shell script that lets you tune the Ruby garbage collection settings. This script is placed in /usr/local/bin/ruby-gc-wrapper. These three variables are used within the template that generates this script:

    ruby_free_min: Sets the RUBY_FREE_MIN environment variable.
    ruby_gc_malloc_limit: Sets the RUBY_GC_MALLOC_LIMIT environment variable.
    ruby_heap_min_slots: Sets the RUBY_HEAP_MIN_SLOTS environment variable.

These variables are blank by default (i.e. they do not change the GC settings at all) and your chosen GC settings will only be used if the `ruby-gc-wrapper` executable is used instead of `ruby`.

**Variables that are set by the role itself (and that shouldn't need to be modified)**

    ruby_dependencies: Controls the installation of dependencies that are necessary in order to properly compile Ruby. Includes libreadline-dev, libssl-dev, libyaml-dev, and zlib1g-dev by default.

    ruby_symlinks: Controls which binaries will be symlinked into /usr/local/bin. Includes bundle, erb, gem, irb, rake, rdoc, ri, ruby, and testrb by default.

    ruby_location: Controls where Ruby will be installed and is set to "/opt/{{ ruby_version }}" by default.

License
-------

The MIT License (MIT)

Copyright (c) 2013 Joshua Lund

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Author Information
------------------

You can find me on [Twitter](https://twitter.com/joshualund), and on [GitHub](https://github.com/jlund/). I also occasionally blog at [MissingM](http://missingm.co).
