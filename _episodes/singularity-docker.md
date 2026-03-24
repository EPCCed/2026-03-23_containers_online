---
title: "Using Docker images with Singularity"
teaching: 5
exercises: 10
questions:
- "How do I use Docker images with Singularity?"
objectives:
- "Learn how to run Singularity containers based on Docker images."
keypoints:
- "Singularity can start a container from a Docker image which can be pulled directly from Docker Hub."
---

## Using Docker images with Singularity

Singularity can also start containers directly from Docker container images, opening up access to a huge number of existing container images available on [Docker Hub](https://hub.docker.com/) and other registries.

While Singularity doesn't actually run a container using the Docker container image (it first converts it to a format suitable for use by Singularity), the approach used provides a seamless experience for the end user. When you direct Singularity to run a container based on a Docker container image, Singularity pulls the slices or _layers_ that make up the Docker container image and converts them into a single-file Singularity SIF container image.

For example, moving on from the simple _Hello World_ examples that we've looked at so far, let's pull one of the [official Docker Python container images](https://hub.docker.com/_/python). We'll use the image with the tag `3.14.3-slim` which has Python 3.14.3 installed on Debian. This image does not contain the common Debian packages contained in the default tag and only contains the minimal Debian packages needed to run `python`.

~~~
remote$ singularity pull python-3.14.3.sif docker://python:3.14.3-slim
~~~
{: .language-bash}

~~~
INFO:    Converting OCI blobs to SIF format
WARNING: 'nodev' mount option set on /tmp, it could be a source of failure during build process
INFO:    Starting build...
Getting image source signatures
Copying blob ec781dee3f47 done
Copying blob 28f4c4271262 done
Copying blob b166afc64daf done
Copying blob fa7570d0dc9b done
Copying config 3876b2cb38 done
Writing manifest to image destination
Storing signatures
2026/03/24 09:37:31  info unpack layer: sha256:ec781dee3f4719c2ca0dd9e73cb1d4ed834ed1a406495eb6e44b6dfaad5d1f8f
2026/03/24 09:37:31  warn xattr{etc/gshadow} ignoring ENOTSUP on setxattr "user.rootlesscontainers"
2026/03/24 09:37:31  warn xattr{/tmp/build-temp-124617440/rootfs/etc/gshadow} destination filesystem does not support xattrs, further warnings will be suppressed
2026/03/24 09:37:32  info unpack layer: sha256:28f4c427126267299d7c407e60ac8b4b001ee92ed6c2ed0c3d0d237ab634a1a7
2026/03/24 09:37:32  warn xattr{var/cache/apt/archives/partial} ignoring ENOTSUP on setxattr "user.rootlesscontainers"
2026/03/24 09:37:32  warn xattr{/tmp/build-temp-124617440/rootfs/var/cache/apt/archives/partial} destination filesystem does not support xattrs, further warnings will be suppressed
2026/03/24 09:37:32  info unpack layer: sha256:b166afc64dafc73acc72490f1ae7b4e4d24f064f91f6b7b4110736bf9ef071e9
2026/03/24 09:37:33  warn xattr{var/log/apt/term.log} ignoring ENOTSUP on setxattr "user.rootlesscontainers"
2026/03/24 09:37:33  warn xattr{/tmp/build-temp-124617440/rootfs/var/log/apt/term.log} destination filesystem does not support xattrs, further warnings will be suppressed
2026/03/24 09:37:33  info unpack layer: sha256:fa7570d0dc9b7cee209516b8eb6a70e2b97cd439a57a3cc4329f76b2b60e1a61
INFO:    Creating SIF file...
~~~
{: .output}

Note how we see Singularity saying that it's "_Converting OCI blobs to SIF format_". We then see the layers of the Docker container image being downloaded and unpacked and written into a single SIF file. Once the process is complete, we should see the python-3.14.3.sif container image file in the current directory.

We can now run a container from this container image as we would with any other Singularity container image.

> ## Running a Python container based on the image that we just pulled from Docker Hub
>
> Try running a Python container. What happens?
> 
> Try running some simple Python statements...
> 
> > ## Running a Python container
> >
> > ~~~
> > remote$ singularity run python-3.14.3.sif
> > ~~~
> > {: .language-bash}
> > 
> > This should put you straight into a Python interactive shell within the running container:
> > 
> > ~~~
> > Python 3.14.3 (main, Mar 16 2026, 23:02:05) [GCC 14.2.0] on linux
> > Type "help", "copyright", "credits" or "license" for more information.
> > >>>

> > ~~~
> > Now try running some simple Python statements:
> > ~~~
> > >>> import math
> > >>> math.pi
> > 3.141592653589793
> > >>> 
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

In addition to running a container and having it run the default run script, you could also start a container running a shell in case you want to undertake any configuration prior to running Python. This is covered in the following exercise:

> ## Open a shell within a Python container
>
> Try to run a shell within a singularity container based on the Python container image. That is, run a container that opens a shell rather than the default Python interactive console as we saw above.
> See if you can find more than one way to achieve this.
> 
> Within the shell, try starting the Python interactive console and running some Python commands.
> 
> > ## Solution
> >
> > Recall from the earlier material that we can use the `singularity shell` command to open a shell within a container. To open a regular shell within a container based on the `python-3.13.2.sif` container image, we can therefore run:
> > ~~~
> > remote$ singularity shell python-3.14.3.sif
> > ~~~
> > {: .language-bash}
> > 
> > ~~~
> > Singularity> echo $SHELL
> > /bin/bash
> > Singularity> cat /etc/issue
> > Debian GNU/Linux 13 \n \l
> > 
> > Singularity> python
> > Python 3.14.3 (main, Mar 16 2026, 23:02:05) [GCC 14.2.0] on linux
> > Type "help", "copyright", "credits" or "license" for more information.
> > >>> print('Hello World!')
> > Hello World!
> > >>> exit()
> > 
> > Singularity> exit
> > $ 
> > ~~~
> > {: .output}
> > 
> > It is also possible to use the `singularity exec` command to run an executable within a container. We could, therefore, use the `exec` command to run `/bin/bash`:
> > 
> > ~~~
> > remote$ singularity exec python-3.14.3.sif /bin/bash
> > ~~~
> > {: .language-bash}
> > 
> > ~~~
> > Singularity> echo $SHELL
> > /bin/bash
> > ~~~
> > {: .output}
> > 
> > You can run the Python console from your container shell simply by running the `python` command.
> {: .solution}
{: .challenge}


## References

\[1\] [Gregory M. Kurzer. Singularity: Containers for Science, Reproducibility, and HPC. 2017 HPC Advisory Council Stanford Conference](https://www.youtube.com/watch?v=DA87Ba2dpNM)
