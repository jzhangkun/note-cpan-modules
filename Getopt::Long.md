# Getopt::Long - Extended processing of command line options

### negatable options and incremental options.
- negatable !
```perl
    my $verbose = '';   # option variable with default value (false)
    GetOptions ('verbose!' => \$verbose);
```
--verbose to enable
--noverbse to disable or --no--verbose to disable

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
Specify destination as array reference or adding a "@"
````perl
    my @libfiles = ();
    GetOptions ("library=s" => \@libfiles);
    # or 
    my $libfiles = [];
    GetOptions ("library=s@" => \$libfiles);
````
Usage in command line
````perl
--library lib/stdlib --library lib/extlib
````

### Options with hash values
Specify the desination as hash reference or adding a '%'
````perl
    GetOptions ("define=s" => \%defines);
    or
    GetOptions ("define=s%" => \$defines);
````
Usage in command line
````perl
--define os=linux --define vendor=redhat
````

### Mixing command line option with other arguments
Usually programs take command line options as well as other arguments, for example, file names. It is good practice to always specify the options first, and the other arguments last. Getopt::Long will, however, allow the options and arguments to be mixed and 'filter out' all the options before passing the rest of the arguments to the program. 
<b>To stop Getopt::Long from processing further arguments, insert a double dash -- on the command line:</b>


