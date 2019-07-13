# awslogs

[https://github.com/jorgebastida/awslogs](https://github.com/jorgebastida/awslogs)


- installation

```bash
pip install --user awslogs
```


- initialization

```bash
awslogs groups --profile ${profile}
${ec2_machine1}
${ec2_machine2}
```

- use

```bash
awslogs streams ${ec2_machine1} --profile ${profile}
# test
awslogs get synchronicity --profile ${profile}
```