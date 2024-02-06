---
title: atomate2 setup
prev: /docs/strachan-lab
---

This page serves as a guiding resource for [atomate2](https://github.com/materialsproject/atomate2) in the Strachan Lab. As of now, it is intended to be a companion to the installation guide at [materials project](https://materialsproject.github.io/atomate2/user/install.html). If there exists demand for a more comprehensive guide, that can be done later.

## What is atomate2?

According to [their README](https://github.com/materialsproject/atomate2),

> Atomate2 is a free, open-source software for performing complex materials science workflows using simple Python functions. Features of atomate2 include
>
> - It is built on open-source libraries: pymatgen, custodian, jobflow, and FireWorks.
> - A library of "standard" workflows to compute a wide variety of desired materials properties.
> - The ability scale from a single material, to 100 materials, or 100,000 materials.
> - Easy routes to modifying and chaining workflows together.
> - It can build large databases of output properties that you can query, analyze, and share in a systematic way.
> - It automatically keeps meticulous records of jobs, their directories, runtime parameters, and more.

After using and refining my implementation of atomate2 for over a year, it has allowed me to escape the cycle of hacky python scripts and messy file structures. Instead, atomate2 lets me use a robust, scalable set of workflows that are consistent with the state of the art in our field.

## Installing atomate2

The atomate2 installation guide is fairly robust; go follow those instructions. Notes on each step are available below.

### VASP

If you don't already have access, ask Kat (or another group member) about getting access to VASP in our HPC environment.

### MongoDB

If you're not familiar with MongoDB already, it is a database that stores information as *documents*. In atomate2, a document often corresponds with a VASP run, an intermediate script, or some post-processing analysis. It's worth getting some basic familiarity with the MongoDB syntax, as it is the main way to query documents in the database. The idea here is that instead of keeping track of runs through messy file structures in temporary scratch directories across different HPC systems, you can just query for the run you want based on the run details (system of interest, calculation type, user-supplied tags).

While you could self-host your own MongoDB, it's a lot easier to use the infrastructure that already exists in our group. Kat has deployed a MongoDB docker image on Geddes, and created services to make this IP accessible to outside services. Details of the database are provided below, but for direct access to the database you should speak to Kat directly about getting added as a user.

### Conda

Unfortunately, the atomate2 library is a mess of dependencies, and installation can be a bit tricky. Follow the atomate2 guide as far as you can, but expect additional issues to arise with dependencies. You will likely need to modify some of the codebase; so again, ask Kat as needed :)

### Config files

A collection of some of the more specific atomate2 config files I use for my instance on Negishi are copied below.

`jobflow.yaml`

```yaml
JOB_STORE:
  docs_store:
    type: MongoStore
    database: yourdbname
    host: ask-kat
    port: 27017
    username: username
    password: password
    collection_name: outputs
  additional_stores:
    data:
      type: GridFSStore
      database: yourdbname
      host: ask-kat
      port: 27017
      username: username
      password: password
      collection_name: outputs_blobs
```

`my_launchpad.yaml`

```yaml
host: ask-kat
port: 27017
name: yourdbname
username: username
password: password
ssl_ca_file: null
logdir: null
Istrm_lvl: DEBUG
user_indices: []
wf_user_indices: []
authsource: admin
retry: true
```

`my_qadapter.yaml` (this is for negishi - other cluster will be different)

```yaml
_fw_name: CommonAdapter
_fw_q_type: SLURM
rocket_launch: rlaunch -c /home/knykiel/atomate2/config singleshot
nodes:  1
ntasks: 72
walltime: 04:00:00
account: standby
job_name: null
logdir: /home/knykiel/atomate2/logs/
launch_dir: /scratch/negishi/knykiel/launches/
pre_rocket: | 
  set echo

  module --force purge
  module load rcac
  module load intel
  module load openmpi
  module load impi
  module load intel-mkl
  module load anaconda
  module list

  export PATH="$HOME/bin:$PATH"

post_rocket: null
```

There are some scripts floating around Kat's system that are used for mass submitting, restarting, and  modifying workflows. These can be combined into a GitHub repo upon request.

## General atomate2 tips

- reading the [fireworks documentation](https://materialsproject.github.io/fireworks/) will greatly help you understand the system of fireworks, workflows, rockets, launches, etc.
- atomate2 has [many standard workflows](https://materialsproject.github.io/atomate2/user/codes/vasp.html#list-of-vasp-workflows), and you can often extend them with pymatgen (i.e. SQSTransformation)
- adding a metadata tag to each FW with `fw.spec.update` can help with querying later
- you can apply INCAR updates with [powerups](https://github.com/materialsproject/atomate2/blob/8b1ee044674bb75ee9cd025d9ffc6d883f772fa5/src/atomate2/vasp/powerups.py#L2)
- launching with `qlaunch -r rapidfire -m N` is a convenient system to launch `N` jobs at once, and queue new jobs as they finish. This can be done with SLURM to run for weeks.