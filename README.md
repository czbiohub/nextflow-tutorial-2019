# nextflow-tutorial-2019
Materials for the Nextflow tutorial held at Biohub on April 11th, 2019

## Schedule

- 10am - 12pm - Learning
  - We will work through Nextflow's awesome [beginner tutorial](https://nextflow-io.github.io/nf-hack18/training.html) together
  - We'll focus on Section 2 - "Simple Rna-Seq pipeline" in the morning
- 12pm - 1pm - Lunch (provided)
- 1pm - 5pm - Hackathon
  - Convert some of your own workflows into Nextflow
  - If you don't have anything ready yet, you can do the [more advanced](https://nextflow-io.github.io/nf-hack18/handson.html) Nextflow tutorial

## Creating your own Nextflow Workflow

Use [cookiecutter-nextflow](https://github.com/czbiohub/cookiecutter-nextflow) to create a template folder with example nextflow workflows. Make sure to add your GitHub repo to [czbiohub/awesome-nextflow](https://github.com/czbiohub/awesome-nextflow)!

We'll use the nextflow-core (nf-core) developers excellent template. Please also check out their [pipeline creation guidelines](https://nf-co.re/adding_pipelines) for more info on writing good pipelines.

### Install [`nf-core/tools`](https://github.com/nf-core/tools)

```
pip install nf-core
```

### Create a pipeline template with `nf-core create`

Check out the documentation for `nf-core create`:

```
 Tue  2 Apr - 15:18  ~/code/nf-core-test   master ✔ 
  nf-core create --help

                                          ,--./,-.
          ___     __   __   __   ___     /,-._.--~\
    |\ | |__  __ /  ` /  \ |__) |__         }  {
    | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                          `._,._,'

Usage: nf-core create [OPTIONS]

  Create a new pipeline using the nf-core template

Options:
  -n, --name TEXT         The name of your new pipeline  [required]
  -d, --description TEXT  A short description of your pipeline  [required]
  --new-version TEXT      The initial version number to use
  --no-git                Do not initialise pipeline as new git repository
  -f, --force             Overwrite output directory if it already exists
  -o, --outdir TEXT       Output directory for new pipeline (default: pipeline
                          name)
  --help                  Show this message and exit.
```

Now we can see that the `--name` and `--description` fields are required. Here's an example

```
nf-core create --name pipelinename --description "pipeline description"
```
 
![nf-core create example output](figures/nf-core-create.gif) 

Here's the example output:
```
 Tue  2 Apr - 15:16  ~/code 
  nf-core create -n test -d "test of nf-core"

                                          ,--./,-.
          ___     __   __   __   ___     /,-._.--~\
    |\ | |__  __ /  ` /  \ |__) |__         }  {
    | \| |       \__, \__/ |  \ |___     \`-._,-`-,
                                          `._,._,'


INFO: Creating new nf-core pipeline: nf-core/test

INFO: Initialising pipeline git repository

INFO: Done. Remember to add a remote and push to GitHub:
  cd /Users/olgabot/code/nf-core-test
  git remote add origin git@github.com:USERNAME/REPO_NAME.git
  git push
```

Here's another example with a slightly more realistic name:

```
nf-core create --name largegenomeassembly --description "Assembly for large (1 gigabase+) genomes"
```

Note that pipeline names must be all lowercase and with no punctuation.



https://nf-co.re/adding_pipelines


### Make a GitHub repository and push to GitHub

Make a [new czbiohub GitHub repository](https://github.com/organizations/czbiohub/repositories/new) with your pipeline name. Enable Travis-CI and don't add any .gitignore or README because the template has it. Also, make it public :)

### Test datasets

Nextflow developers have kindly curated test datasets in [nf-core/test-datasets](https://github.com/nf-core/test-datasets/). If that doesn't have what you want, aggressively downsample your data e.g. down to 1% of the input reads, or just one chromosome.


### Enable Github Pages

Turning on GitHub pages will create a little website out of the `docs/` folder in the repository. Here's an example using their defaults: https://czbiohub.github.io/nf-core-test/


### Add your pipeline to [czbiohub/awesome-nextflow](https://github.com/czbiohub/awesome-nextflow)

We have our own internal Nextflow workflows enumerated at [czbiohub/awesome-nextflow](https://github.com/czbiohub/awesome-nextflow). There is also a more global [nextflow-io/awesome-nextflow](https://github.com/nextflow-io/awesome-nextflow) list of nextflow workflows you may want to check out before writing your own.
