# md5

- create uuid from string

```bash
echo -n ${string_to_convert} | md5sum | awk '{print $1}'
```