# BUSCO-docker

Forked from chrishah/BUSCO-docker
- When multithreaded BUSCO will sometimes fail with an error reccomending using blast 2.2 instead of 2.6. By using Ubuntu 16.04 we can easiy achieve that.

Docker image containing a full BUSCO install

The image contains a full install of [BUSCO](https://busco.ezlab.org/), including all necessary dependencies. I am not part of the BUSCO team - I just made this image.

In detail, the image is set up with:
 - Ubuntu 16.04
 - Python 3
 - blast 2.2.31-4
 - hmmer
 - Augustus
 - BUSCO 3.1.0
 - R
   - ggplot2 3.1.0

To run [BUSCO](https://busco.ezlab.org/) you can do the following (this will mount the directory `/home/working` of the container to the current working directory on your local machine):
```bash
$ docker run -it --rm -v $(pwd):/home/working -w /home/working chrishah/busco-docker run_BUSCO.py
```

Example for assessing metazoan genome (genome is in file `./genome.fasta`):
```bash
#download metazoa reference set
$ wget -qO- https://busco.ezlab.org/datasets/metazoa_odb9.tar.gz | tar -xvz

#run BUSCO
$ docker run -it --rm -v $(pwd):/home/working -w /home/working chrishah/busco-docker run_BUSCO.py \
--in ./genome.fasta --out genome.BUSCO -l ./metazoa_odb9 --mode genome
```

You can also enter the container environment and work within it. All executables, e.g. `run_BUSCO.py`, `generate_plots.py`, are in the `PATH`.
```bash
$ docker run -it --rm --net=host -v $(pwd):/home/working -w /home/working chrishah/busco-docker /bin/bash
```


