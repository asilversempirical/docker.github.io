---
description: How to install Docker Compose
keywords: compose, orchestration, install, installation, docker, documentation
title: Install Docker Compose
---

You can run Compose on macOS, Windows and 64-bit Linux.

## Prerequisites

Docker Compose relies on Docker Engine for any meaningful work, so make sure you
have Docker Engine installed either locally or remote, depending on your setup.

- On desktop systems like Docker for Mac and Windows, Docker Compose is
included as part of those desktop installs. Skip down to [Install Compose on Mac or Windows systems](#install-compose-on-mac-or-windows-systems).

- On Linux systems, first install the
[Docker](/engine/installation/index.md#server){: target="_blank" class="_"}
for your OS as described on the Get Docker page, then come back here for
instructions on installing [installing Compose on
Linux](#install-compose-on-linux-systems).

## Install Compose on Mac or Windows systems

**Docker for Mac**, **Docker for Windows**, and **Docker Toolbox**
already include Compose along with other Docker apps, so most Mac
and Windows users do not need to install Compose separately.
Docker install instructions for these are here:

* [Get Docker for Mac](/docker-for-mac/install.md)
* [Get Docker for Windows](/docker-for-windows/install.md)
* [Get Docker Toolbox](/toolbox/overview.md) (for older systems)

**If you are running the Docker daemon and client directly on Microsoft
Windows Server 2016** (with [Docker EE for Windows Server 2016](/engine/installation/windows/docker-ee.md), you _do_ need to install
Docker Compose. To do so, follow these steps:

1.  Start an "elevated" PowerShell (run it as administrator).

    Search for PowerShell, right-click, and choose
    **Run as administrator**. When asked if you want to allow this app
    to make changes to your device, click **Yes**.

    In PowerShell, run the following command to download
    Docker Compose, replacing `$dockerComposeVersion` with the specific
    version of Compose you want to use:

    ```none
    Invoke-WebRequest "https://github.com/docker/compose/releases/download/$dockerComposeVersion/docker-compose-Windows-x86_64.exe" -UseBasicParsing -OutFile $Env:ProgramFiles\docker\docker-compose.exe
    ```

    For example, to download Compose version {{ site.compose_current }},
    the command is:

    ```none
    Invoke-WebRequest "https://github.com/docker/compose/releases/download/{{site.compose_current}}/docker-compose-Windows-x86_64.exe" -UseBasicParsing -OutFile $Env:ProgramFiles\docker\docker-compose.exe
    ```
    >  Use the latest Compose release number in the download command.
    >
    > As already mentioned, the above command is an _example_, and
    it may become out-of-date once in a while. Always follow the
    command pattern shown above it. If you cut-and-paste an example,
    check which release it specifies and, if needed,
    replace `$dockerComposeVersion` with the release number that
    you want. Compose releases are also available for direct download
    on the [Compose repository release page on GitHub](https://github.com/docker/compose/releases){:target="_blank" class="_"}.
    {: .important}

3.  Run the executable to install Compose.

## Install Compose on Linux systems

On **Linux**, you can download the Docker Compose binary from the [Compose
repository release page on GitHub](https://github.com/docker/compose/releases){:
target="_blank" class="_"}. Follow the instructions from the link, which involve
running the `curl` command in your terminal to download the binaries. These step
by step instructions are also included below.

1.  Run this command to download Docker Compose, replacing
`$dockerComposeVersion` with the specific version of Compose you want to use:

    ```bash
    curl -L https://github.com/docker/compose/releases/download/$dockerComposeVersion/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    ```

    For example, to download Compose version {{site.compose_current}}, the command
    is:

    ```bash
    curl -L https://github.com/docker/compose/releases/download/{{site.compose_current}}/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    ```

    >  Got a "Permission denied" error?
    >
    If so, your `/usr/local/bin` directory probably isn't writable and
    you'll need to install Compose as the superuser. Run `sudo -i`, then
    run the download and install commands below, then `exit`.

    > Use the latest Compose release number in the download command.
    >
    The above command is an _example_, and it may become out-of-date once
    in a while. Always follow the command pattern shown above it. If
    you cut-and-paste an example, check which release it specifies and,
    if needed, replace `$dockerComposeVersion` with the release number that
    you want. Compose releases are also available for direct download on
    the [Compose repository release page on GitHub](https://github.com/docker/compose/releases){: target="_blank"
    class="_"}.
    {: .important}

    If you have problems installing with `curl`, see
    [Alternative Install Options](install.md#alternative-install-options).

2.  Apply executable permissions to the binary:

    ```bash
    sudo chmod +x /usr/local/bin/docker-compose
    ```

3.  Optionally, install [command completion](completion.md) for the
    `bash` and `zsh` shell.

4.  Test the installation.

    ```bash
    $ docker-compose --version
    docker-compose version {{site.compose_current}}, build 1719ceb
    ```

## Alternative install options

### Install using pip

Compose can be installed from [pypi](https://pypi.python.org/pypi/docker-compose)
using `pip`. If you install using `pip`, we recommend that you use a
[virtualenv](https://virtualenv.pypa.io/en/latest/) because many operating systems
have python system packages that conflict with docker-compose dependencies. See
the [virtualenv tutorial](http://docs.python-guide.org/en/latest/dev/virtualenvs/)
to get started.

```bash
pip install docker-compose
```
if you are not using virtualenv,

```bash
sudo pip install docker-compose
```

> pip version 6.0 or greater is required.

### Install as a container

Compose can also be run inside a container, from a small bash script wrapper.
To install compose as a container run this command. Be sure to replace the version number with the one that you want, if this example is out-of-date:

```bash
$ curl -L --fail https://github.com/docker/compose/releases/download/{{site.compose_current}}/run.sh > /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

>  Use the latest Compose release number in the download command.
>
The above command is an _example_, and it may become out-of-date once in a
while. Check which release it specifies and, if needed, replace the given
release number with the one that you want. Compose releases are also listed and
available for direct download on the [Compose repository release page on
GitHub](https://github.com/docker/compose/releases){: target="_blank"
class="_"}.
{: .important}

## Master builds

If you're interested in trying out a pre-release build you can download a
binary from
[https://dl.bintray.com/docker-compose/master/](https://dl.bintray.com/docker-compose/master/).
Pre-release builds allow you to try out new features before they are released,
but may be less stable.


## Upgrading

If you're upgrading from Compose 1.2 or earlier, you'll need to remove or migrate
your existing containers after upgrading Compose. This is because, as of version
1.3, Compose uses Docker labels to keep track of containers, and so they need to
be recreated with labels added.

If Compose detects containers that were created without labels, it will refuse
to run so that you don't end up with two sets of them. If you want to keep using
your existing containers (for example, because they have data volumes you want
to preserve) you can use compose 1.5.x to migrate them with the following command:

```bash
docker-compose migrate-to-labels
```

Alternatively, if you're not worried about keeping them, you can remove them.
Compose will just create new ones.

```bash
docker rm -f -v myapp_web_1 myapp_db_1 ...
```

## Uninstallation

To uninstall Docker Compose if you installed using `curl`:

```bash
sudo rm /usr/local/bin/docker-compose
```

To uninstall Docker Compose if you installed using `pip`:

```bash
pip uninstall docker-compose
```

> Got a "Permission denied" error?
>
> If you get a "Permission denied" error using either of the above
> methods, you probably do not have the proper permissions to remove
> `docker-compose`. To force the removal, prepend `sudo` to either of the above
> commands and run again.


## Where to go next

- [User guide](index.md)
- [Getting Started](gettingstarted.md)
- [Get started with Django](django.md)
- [Get started with Rails](rails.md)
- [Get started with WordPress](wordpress.md)
- [Command line reference](/compose/reference/index.md)
- [Compose file reference](compose-file.md)
