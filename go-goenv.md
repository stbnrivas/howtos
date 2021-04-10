# goenv installation

```bash
git clone https://github.com/syndbg/goenv.git ~/.goenv


$ echo 'export GOENV_ROOT="$HOME/.goenv"' >> ~/.bash_profile
$ echo 'export PATH="$GOENV_ROOT/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(goenv init -)"' >> ~/.bash_profile


# Go tools expect a certain layout of the source code. GOROOT and GOPATH are environment variables that define this layout.
# 1. GOROOT is a variable that defines where your Go SDK is located.
#           You do not need to change this variable, unless you plan to use different Go versions.
# 2. GOPATH is a variable that defines the root of your workspace. By default, the workspace directory ~/go
#

# before to go 1.8, it was required to set a local environment variable called $GOPATH which tell to compiler
# where to find imported third party source code
$ echo 'export GOPATH="$HOME/go' >> ~/.bash_profile

$ echo 'export PATH="$GOROOT/bin:$PATH"' >> ~/.bash_profile
$ echo 'export PATH="$PATH:$GOPATH/bin"' >> ~/.bash_profile


goenv install 1.12.0
```



```
go env


GOARCH="amd64"
GOBIN=""
GOEXE=""
GOHOSTARCH="amd64"
GOHOSTOS="linux"
GOOS="linux"
GOPATH="/home/stbn/go/1.6.4"
GORACE=""
GOROOT="/home/stbn/.goenv/versions/1.6.4"
GOTOOLDIR="/home/stbn/.goenv/versions/1.6.4/pkg/tool/linux_amd64"
GO15VENDOREXPERIMENT="1"
CC="gcc"
GOGCCFLAGS="-fPIC -m64 -pthread -fmessage-length=0"
CXX="g++"
CGO_ENABLED="1"

```


creating a workspace, go workspace will contain  `src`, `bin` folders and `vendor`

- `src` may contain multiple version control repositories, this allowfor a canonical import of code in your project such `github.com/digitalocean/godo`
- `bin` executables built and installed by go tools


```
mkdir -p $HOME/go/{bin,src}
```


```bash
go get github.com/gobuild/gopack
```