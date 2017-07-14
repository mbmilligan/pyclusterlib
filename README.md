# pyclusterlib
Python library to abstract out running on clusters across various job managers

## Purpose

Numerous packages provide some kind of functionality to execute tasks
on clusters using job manager environments. This causes duplication of
effort, and also inconsistent support for different environments from
project to project. This project is initially a collaboration between
the authors
of [BatchSpawner](https://github.com/jupyterhub/batchspawner)
and [ipyparallel](https://github.com/ipython/ipyparallel)
to build a common resource for this task.

Note that [https://github.com/clusterlib/clusterlib]
exists but appears to be abandoned and has very limited functionality
compared to our needs.

## Design

See [ipyparallel#276](https://github.com/ipython/ipyparallel/issues/276) for the
original design discussion. Usage will follow the pattern:

```python
C = pyclusterlib.get_cluster(type, **params)
script = C.make_script(**params)
subcmd = C.submit_cmd(**params)

output = my_run_cmd(subcmd, stdin=script)
job = C.get_jobid(output)

statcmd = C.status_cmd(job, **params)

output = my_run_cmd(statcmd)
C.set_status(output)
```

and so on.
