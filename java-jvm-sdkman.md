# sdkman

SDKMAN! is a tool for managing parallel versions of multiple Software Development Kits on most Unix based systems. It provides a convenient Command Line Interface (CLI) and API for installing, switching, removing and listing Candidates. Formerly known as GVM the Groovy enVironment Manager, it was inspired by the very useful RVM and rbenv tools, used at large by the Ruby community.

```
sudo apt-get install unzip zip sed
```



```bash
sdk

# Usage: sdk <command> [candidate] [version]
#        sdk offline <enable|disable>
#
#    commands:
#        install   or i    <candidate> [version]
#        uninstall or rm   <candidate> <version>
#        list      or ls   [candidate]
#        use       or u    <candidate> [version]
#        default   or d    <candidate> [version]
#        current   or c    [candidate]
#        upgrade   or ug   [candidate]
#        version   or v
#        broadcast or b
#        help      or h
#        offline           [enable|disable]
#        selfupdate        [force]
#        update
#        flush             <broadcast|archives|temp>
```


```bash
sdk install scala 2.13.1
sdk install scala 2.11.12

sdk list java | grep installed

sdk list scala
sdk use scala 2.11.12
sdk default scala 2.11.12


sdk uninstall scala 3.1.1.
```