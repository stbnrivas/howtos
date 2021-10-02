# standard io redirections


the standard input/output/error descriptor

- 0: stdin
- 1: stdout
- 2: stderr


## redirecting output

```
cd /tmp
ls > files
ls 1> files   # explicitly and equivalent
```

## redirecting error

```
cd /tmp
./non-existing-file.sh 2> errors.txt
```

## redirecting input

```
cat < existing-file
echo < existing-file

cat existing-file | grep
```


xargs

## redirecting output and error

```
# redirecting for different file
./non-existing-file.sh 1> output.txt 2> error.txt


# redirecting for same file
./non-existing-file.sh > output-error.txt 2>&1

echo "to output" & ./non-existing-file.sh 1> output-error.txt 2> output-error.txt # NOT WORKING
```





## redirect stdout to multiple programs

```
tee
```

## exec family

- execl
- execlp
- execle
- execv
- execvp
- execvpe


The exec() family of functions replaces the current process image with a new process image.

## run a new process without block terminal

```
{ sleep 5; } &

ls&

nohup # run a command immune to hangups, with output to a non-tty
```

