# Singularity Tools for Continuous Integration

This repository shows a simple example of how to use the [stools](https://www.github.com/singularityhub/stools)
(Singularity Tools) container to run [Clair OS](https://clair-os.org) security checks on your container.


## Travis CI
The `travis.yml` file in the repository sets up the build to pull and use the container `vanessa/stools-clair`. One
cool feature of Travis is the ability to use cron jobs to run a build at a particular frequency, meaning that
we can set up regularly scheduled testing of our containers. Cool!


### Under Development
 
 - interactive artifacts for the scan results
 - Circle CI integration examples
 - option to fail at particular level?
 - messages back to Github?
