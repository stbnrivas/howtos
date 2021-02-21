# scala installation using sdk

```bash
#see https://sdkman.io/install
curl -s "https://get.sdkman.io" | bash
sdk version

sdk selfupdate
sdk update
rm -rf ~/.sdkman
```

listing versions
p
```bash
sdk list
sdk list java
sdk list scala
sdk list sbt

sdk list kotlin
```


installing specific version

```bash

sdk list java

# Vendor       | Use | Version      | Dist    | Status     | Identifier
#---------------------------------------------------------------------------
# AdoptOpenJDK | >>> | 12.0.1.j9    | adpt    | installed  | 12.0.1.j9-adpt
#              |     | 12.0.1.hs    | adpt    |            | 12.0.1.hs-adpt
#              |     | 11.0.4.j9    | adpt    |            | 11.0.4.j9-adpt
#              |     | 11.0.4.hs    | adpt    |            | 11.0.4.hs-adpt
#              |     | 8.0.222.j9   | adpt    |            | 8.0.222.j9-adpt
#              |     | 8.0.222.hs   | adpt    |            | 8.0.222.hs-adpt
# Amazon       |     | 11.0.4       | amzn    |            | 11.0.4-amzn
#              |     | 8.0.222      | amzn    |            | 8.0.222-amzn
# Azul Zulu    |     | 12.0.2       | zulu    |            | 12.0.2-zulu
#              |     | 11.0.4       | zulu    |            | 11.0.4-zulu

sdk install java 12.0.1.j9
sdk install java 8.0.222.j9
```

select between versions

```bash
sdk default java 12.0.1.j9
sdk use java 12.0.1.j9
```
