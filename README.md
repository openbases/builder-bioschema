# Open Schemas Builder

![https://github.com/openschemas/spec-template/raw/master/img/hexagon_square_small.png](https://github.com/openschemas/spec-template/raw/master/img/hexagon_square_small.png)

This is an [openbases](https://openbases.github.io) builder for Open Schemas
to generate a specification using the [map2model](https://www.github.com/openschemas/map2model)
example that uses [openschemas-python](https://www.github.com/openschemas/openschemas-python/)
to generate a specification for contribution to [schema.org](https://www.schema.org). 
You can use the container to generate your specification as follows:

 1. Fill in the templates provided on Google Drive, and download as tsv
 2. Run the [openschemas/schema-builder](https://hub.docker.com/r/openschemas/schema-builder) container to generate your specification files
 3. Contribute your specification by way of a pull request to [openschemas](https://www.github.com/openschemas/specifications) (still under development)

That's it! More information coming soon.

## Usage

### 1. Generate your Front Matter
Edit the file [configuration.yml](specifications/configuration.yml) in 
the [specifications](specifications) directory and fill in the values for your
specification. Are you editing or contributing more than one? Feel free to copy paste the chunk
(not including the "specifications" header) and have more than one.

### 2. Write your specification!
Now generate your new template! You can create a copy of the Google Drive template [provided here](https://docs.google.com/spreadsheets/d/1seHDwKRwET_H8maRTMmdXG7M1deh23Y613TaJ2Pd3qc/edit?usp=sharing).

### 3. Download to your Computer
When you are done, **export each sheet** as a tsv file (tab separated value) and drop into a subfolder named by your specification (e.g., "[DataCatalog](specifications/Datacatalog)" is a folder in [specifications](specifications). When you are done, you will have something like this:

```
specifications/
├── configuration.yml
└── DataCatalog
    ├── DataCatalog - Authors.tsv
    ├── DataCatalog - Bioschemas.tsv
    ├── DataCatalog - Mapping.tsv
    └── DataCatalog - Specification.tsv
```
(with optionally more than one specification subfolder!)

### 4. Generate the specification files
You now can generate your specification files with the provided Docker container! 

#### Ask for Help
If you need to ask for help, just run the container:

```bash
$ docker run openschemas/schema-builder
Usage:


         docker run <container> [demo|start|help]
         docker run <container> demo
         docker run <container> help
         docker run -v /code/:/data <container> start

         Commands:

                help: show help and exit
                start: generate a specification, with your subdirectory with the
                       specifications top level folder bound to /data
                demo: show a demo generation using files in the container
         
         Options [start]:

            --config CONFIG     configuration.yml file, defaults to configuration.yml in
                                folder
            --folder SPECS      folder with input specification subfolders
            --output OUTFOLDER  folder to write output specification subfolders
            --template TEMPLATE template for Jekyll rendering (use default)
            --repo REPO         repository specification is intended for
                                defaults to openschemas/specifications
         
```

### See a demo
There are files provided in the container (the same demo ones in this folder)
that you can use (without mounting a volume) to see what output should look like:

```bash
$ docker run -it openschemas/schema-builder demo
```

### See an Example
You can next try the local files provided in this repository to learn how to mount
the volume correctly. If you haven't already, clone the repository and go for it!

```bash
$ git clone https://www.github.com/openschemas/schema-builder
$ cd schema-builder
```

Let's also going to set the output folders and input configuration file to
the ones we have locally, because it's likely you might have this setup. Importantly,
since we are binding the $PWD to the container, we need to reference paths in the
$PWD relative to /data in the container!

```
mkdir -p outfiles
$ docker run -v $PWD:/data openschemas/schema-builder start --config /data/specifications/configuration.yml --output /data/outfiles
```

Here are your files!

```bash
tree outfiles/
└── DataCatalog
    ├── DataCatalog.html
    ├── DataCatalog.yml
    ├── examples
    │   └── README.md
    └── README.md
```

Now you know how to do your own! You would want to specify the `configuration.yml` file
via `--config` and then output via `--output` and make sure your container mappings
are correct (as per the example above). If you have any trouble, please 
[open an issue](https://www.github.com/openschemas/schema-builder).

### Contribute to schemas.org

Instructions coming soon! I (@vsoch) have to figure this out.

## Development

Build the container

```bash
$ docker build -t openschemas/schema-builder .
```
