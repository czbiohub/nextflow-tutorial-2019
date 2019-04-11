# nextflow-tutorial-2019
Materials for the Nextflow tutorial held at Biohub on April 11th, 2019

## Schedule

- 10am - 12pm - Learning
  - We will work through Nextflow's awesome [beginner tutorial](https://nextflow-io.github.io/nf-hack18/training.html) together
  - We'll focus on Sections 1-2 - "Installation" and "Simple Rna-Seq pipeline" in the morning
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

## Examples of Nextflow pipelines and patterns

### Toy examples: [Nextflow patterns](https://github.com/nextflow-io/patterns)

> A curated collections of Nextflow implementation patterns

These are toy/small examples showing Nextflow functionality for very basic
examples, from the Nextflow developers. This is certainly *somewhat* helpful for getting started but very limited in scope  for more complicated situations.
Here's some copy-pastable code for searching for example outputs. In this example, we're looking for how to make a program output values in addition to files by searching for `output:` and the 5 lines after it with `-A 5`.

```
git clone https://github.com/nextflow-io/patterns nextflow-io/patterns
cd nextflow-io/patterns
git grep -A 5 'output:' .
```

Here's the output:

```
collect-into-file.nf:  output:
collect-into-file.nf-  file 'file.fq' into unzipped_ch
collect-into-file.nf-  script:
collect-into-file.nf-  """
collect-into-file.nf-  < $x zcat > file.fq
collect-into-file.nf-  """
--
conditional-process.nf:  output:
conditional-process.nf-  file 'x.txt' into foo_ch
conditional-process.nf-  when:
conditional-process.nf-  !params.flag
conditional-process.nf-
conditional-process.nf-  script:
--
conditional-process.nf:  output:
conditional-process.nf-  file 'x.txt' into bar_ch
conditional-process.nf-  when:
conditional-process.nf-  params.flag
conditional-process.nf-
conditional-process.nf-  script:
... truncated ..
```

### Slightly more realistic: [`nextflow-demos`](https://github.com/stevekm/nextflow-demos)

> Example Nextflow pipelines and programming techniques

This is a curated list of example Nextflow pipelines maintained by non-Nextflow developers which can be helpful. Again, we're looking for ways to have multiple outputs from a single process.

```
git clone https://github.com/stevekm/nextflow-demos
cd nextflow-demos
git grep -A 5 'output:' .
```

Output:
```
LaTeX-aggregate/main.nf:    output:
LaTeX-aggregate/main.nf-    file("texput.pdf") into pdfs
LaTeX-aggregate/main.nf-
LaTeX-aggregate/main.nf-    script:
LaTeX-aggregate/main.nf-    """
LaTeX-aggregate/main.nf-    echo '\\shipout\\hbox{${word}}\\end' | pdftex
--
LaTeX-aggregate/main.nf:    output:
LaTeX-aggregate/main.nf-    file("report.pdf")
LaTeX-aggregate/main.nf-
LaTeX-aggregate/main.nf-    script:
LaTeX-aggregate/main.nf-    """
LaTeX-aggregate/main.nf-    pdflatex "${report}"
--
aggregate-db-report/people.nf:    output:
aggregate-db-report/people.nf-    set val(name), val(url), file("${output}") into people_pics
aggregate-db-report/people.nf-
aggregate-db-report/people.nf-    script:
aggregate-db-report/people.nf-    output = "${name}.jpg"
aggregate-db-report/people.nf-    """
... truncated ...
```


### Awesome Nextflow

There's a few places you can look for curated lists of Nextflow workflows as inspiration for your own workflows.

- [nextflow-io/awesome-nextflow](https://github.com/nextflow-io/awesome-nextflow)
- Internal Biohub workflows: [czbiohub/awesome-nextflow](https://github.com/czbiohub/awesome-nextflow)
