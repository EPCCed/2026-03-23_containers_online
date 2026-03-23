---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
---

Times: Mon-Tue, 23-24 March 2026, 10:00 - 16:00

Location: Online

Instructor: [Juan Herrera (EPCC, University of Edinburgh)](https://www.epcc.ed.ac.uk/about-us/our-team/dr-juan-rodriguez-herrera)

<hr />

This session aims to introduce the use of Docker and Singularity containers with the goal of using them to effect reproducible computational environments. Such environments are useful for ensuring reproducible research outputs, for example.

> ## After completing this session you should:
> - Have an understanding of what containers are, why they are useful and the common terminology used
> - Have a working Docker installation on your local system to allow you to use containers
> - Understand how to use existing Docker and Singularity containers for common tasks
> - Be able to build your own Docker containers by understanding both the role
>   of a `Dockerfile` in building containers, and the syntax used in `Dockerfile`s
> - Understand the key differences between Docker and Singularity containers to allow you to use them
>   effectively
> - Understand how to manage Docker containers on your local system and Singularity containers on a
>   remote HPC system
> - Appreciate issues around reproducibility in software, understand how 
>   containers can address some of these issues and what the limits to
>   reproducibility using containers are
{: .objectives}

The practical work in this lesson will use Docker on your own laptop and Singularity on a remote HPC platform. Beyond your laptop, software container technologies such as Docker can also be used in the cloud and on high performance computing (HPC) systems. Some of the material in this lesson will be applicable to those environments too.

> ## Prerequisites
>
> - You should have basic familiarity with using a command shell, and the lesson text will at times request that you "open a shell window", with an assumption that you know what this means.
>   - Under Linux or macOS it is assumed that you will access a `bash` shell (usually the default), using your Terminal application.
>   - Under Windows, Powershell and Git Bash should allow you to use the Unix instructions. We will also try to give command variants for Windows `cmd.exe`.
> - The lessons will sometimes request that you use a text editor to create or edit files in particular directories. It is assumed that you either have an editor that you know how to use that runs within the working directory of your shell window (e.g. `nano`), or that if you use a graphical editor, that you can use it to read and write files into the working directory of your shell.
{: .prereq}

> ## A note about Docker and Singularity
>
> Docker and Singularity are mature, robust and very widely used application. Nonetheless,
> they are still under extensive development. New versions are released regularly
> often containing a range of updates and new features.
>
> While we do our best to ensure that this lesson remains up to date and the
> descriptions and outputs shown match what you will see,
> inconsistencies can occur.
> 
> If you spot inconsistencies or encounter any problems, please do report them
> by [opening an issue][open a lesson issue] in the [GitHub repository][docker-introduction repository] 
> for this lesson.
{: .callout}

{% include links.md %}

