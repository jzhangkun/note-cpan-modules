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
````perl
    --size 24 -- --all
````
In this example, --all will not be treated as an option, but passed to the program unharmed, in @ARGV.

### User-defined subroutines to handle options

## Advanced
### Object oriented interface
Getopt::Long can be used in an object oriented way as well:
````perl
    use Getopt::Long;
    $p = Getopt::Long::Parser->new;
    $p->configure(...configuration options...);
    if ($p->getoptions(...options descriptions...)) ...
    if ($p->getoptionsfromarray( \@array, ...options descriptions...)) ...
````

### Documentation and help texts
Getopt::Long encourages the use of Pod::Usage to produce help messages. 
See Pod::Usage for details.

### Parsing options from an arbitrary array
By default, GetOptions parses the options that are present in the global array @ARGV. A special entry GetOptionsFromArray can be used to parse options from an arbitrary array.
````perl
    $ret = GetOptions(\%opts, ... );
    $ret = GetOptionsFromArray(\@ARGV, \%opts, ... );
````
### Parsing options from an arbitrary string
A special entry GetOptionsFromString can be used to parse options from an arbitrary string.
As with GetOptionsFromArray, a first argument hash reference now becomes the second argument.

### Storing options values in a hash
To obtain this, a reference to a hash must be passed as the first argument to GetOptions().

### Argument callback
A special option 'name' <> can be used to designate a subroutine to handle non-option arguments. 
````perl
    my $width = 80;
    sub process { ... }
    GetOptions ('width=i' => \$width, '<>' => \&process);
````

