# Singularity Tools for Continuous Integration

This repository shows a simple example of how to use the [stools](https://www.github.com/singularityhub/stools)
(Singularity Tools) container to run [Clair OS](https://github.com/coreos/clair) security checks on your container.

## Travis CI

[![Build Status](https://travis-ci.org/singularityhub/stools-clair.svg?branch=master)](https://travis-ci.org/singularityhub/stools-clair)

The `travis.yml` file in the repository sets up the build to pull and use the container `vanessa/stools-clair`. 

### Continuous Vulnerability Testing
A cool feature of Travis is the ability to use cron jobs to run a build at a particular frequency, meaning that
we can set up regularly scheduled testing of our containers. Cool! How to do that?

 - Navigate to the project settings page, usually at `https://travis-ci.org/[organization]/[repo]/settings`
 - Under "Cron Jobs" select the branch and interval that you want the checks to run, and then click "Add"

That's it!


### Change the recipe file
If you have a Singularity recipe in the base of your repository, you should not need to change this file. If you want to change
it to include one or more recipes in different locations, then you will want to change this line:

```bash
# Perform the build from your Singularity file, we are at the base of the repo
- docker exec -it clair-scanner singularity build container.simg Singularity
```

Where is says `Singularity` you might change it to path/in/repo/Singularity. 

### Add another recipe file
You aren't limited to the number of containers you can build and test! You can build more than one, and test the resulting containers, like this:

```bash
 - docker exec -it clair-scanner singularity build container1.simg Singularity
 - docker exec -it clair-scanner singularity build container2.simg Singularity.two
 - docker exec -it clair-scanner sclair container1.simg container2.simg
```

### Pull a container
If you don't want to build here, you can use Continuous Integration just for testing. Let's say we have a
repository with just a travis file, we can actually use it to test all of our Docker images (converted to Singularity) or
containers hosted on Singularity Hub. That might look like this:

```bash
 - docker exec -it clair-scanner singularity pull --name vsoch-hello-world.simg shub://vsoch/hello-world
 - docker exec -it clair-scanner singularity pull --name ubuntu.simg docker://ubuntu:16.04
 - docker exec -it clair-scanner sclair vsoch-hello-world.simg ubuntu.simg
```

### Rename the Output
You might also change the name of the output image (container.simg). Why? Imagine that you are using Travis to
build, test, and then upon success, to upload to some container storage. 


## Feedback Wanted!

 1. Under what conditions might we want a build to fail testing?
 2. How many users prefer using CircleCI to Docker? Or vice versa?
 3. Is it worth having some kind of message sent back to Github (would require additional permissions)?
 4. Circle has support for artifacts. How might you want results presented?

Please [let me know](https://www.github.com/singularityhub/stools/issues) your feedback!
