# Getopt::Long - Extended processing of command line options

### negatable options and incremental options.
- negatable !
```perl
    my $verbose = '';   # option variable with default value (false)
    GetOptions ('verbose!' => \$verbose);
```
--verbose to enable
--noverbse to disable

- incremental +
````perl
    my $verbose = '';   # option variable with default value (false)
    GetOptions ('verbose+' => \$verbose);
````
each occurrence of --verbose could increase the verbosity level of the program.

### Options with values
Three kinds of values are supported: 
- 'i': integer numbers;
- 'f': floating point numbers;
- 's': strings.
````perl
    my $tag = '';       # option variable with default value
    GetOptions ('tag=s' => \$tag);
````

### Options with multiple values
By adding a "@"
````perl
     my @libfiles;
    GetOptions ("library=s@" => \@libfiles);
````
