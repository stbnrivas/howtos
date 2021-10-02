# dd

```
dd if=<input> of=<output>
```

# using dd to convert

```
dd if=/tmp/group of=/tmp/GROUP conv=ucase
```

dd can also perform various conversions; the conv=ucase option will convert all of the characters to upper-case characters.



## dd with progress

```
dd if=/dev/zero of=/dev/sda status=progress
```
