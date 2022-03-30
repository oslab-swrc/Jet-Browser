# Jet Browser

## Jet Journal  +  <img src="https://raw.githubusercontent.com/filebrowser/logo/master/banner.png" width="150"/>

![Preview](https://user-images.githubusercontent.com/5447088/50716739-ebd26700-107a-11e9-9817-14230c53efd2.gif)

[![Build](https://github.com/filebrowser/filebrowser/actions/workflows/main.yaml/badge.svg)](https://github.com/filebrowser/filebrowser/actions/workflows/main.yaml)
[![Go Report Card](https://goreportcard.com/badge/github.com/filebrowser/filebrowser?style=flat-square)](https://goreportcard.com/report/github.com/filebrowser/filebrowser)
[![Documentation](https://img.shields.io/badge/godoc-reference-blue.svg?style=flat-square)](http://godoc.org/github.com/filebrowser/filebrowser)
[![Version](https://img.shields.io/github/release/filebrowser/filebrowser.svg?style=flat-square)](https://github.com/filebrowser/filebrowser/releases/latest)
[![Chat IRC](https://img.shields.io/badge/freenode-%23filebrowser-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23filebrowser)

* Filebrowser provides a file managing interface within a specified directory and it can be used to upload, delete, preview, rename and edit your files. It allows the creation of multiple users and each user can have its own directory. It can be used as a standalone app or as a middleware.
* Jet-Journal is a novel scalable per-core journal, and it can easily replace JBD2, the generic journal layer. In order to use Jet-Browser, you need to import a Jet-Journal from another repository and change the kernel to this.
* The File Browser follows [Apache-2.0 License](https://github.com/oslab-swrc/Jet-Browser/blob/master/LICENSE)

## Features

Please refer to our docs at [https://filebrowser.org/features](https://filebrowser.org/features)

## Install

For installation instructions please refer to our docs at [https://filebrowser.org/installation](https://filebrowser.org/installation).

### How to use jet-journal

- Download and build e2fsprocs for zjournal.

```
git clone https://github.com/J-S-Kim/e2fsprog-zj.git
cd e2fsprog-zj
./configure
make
```

- Clone jet-journal source code from jet-journal repository

```
git clone https://github.com/oslab-swrc/jet-journal.git
```

- And then install the kernel in jet-journal directory, and reboot to the kernel you installed.
- When installing, configure should be set as below.
- After rebooting, verify that ext4mj and zj modules are installed successfully.

```
File systems  --->
    [M] The Extended 4 (ext4mj) filesystem
```

- Format the storage device and mount it with the command shown below.
- At this point, the number of journals is the same as the current number of online cores.

```
sudo ./e2fsprog-zj/misc/mke2fs -t ext4 -J multi_journal -F -G 1 /dev/<block device>
sudo ./e2fsprog-zj/misc/tune2fs -o journal_data /dev/<block device>
sudo mount -t ext4mj /dev/<block device> <mount point>
```

- Finally, the file browser runs as follows

```
docker run -v <mount point>:/srv filebrowser/filebrowser
```

## Configuration

[Authentication Method](https://filebrowser.org/configuration/authentication-method) - You can change the way the user authenticates with the filebrowser server

[Command Runner](https://filebrowser.org/configuration/command-runner) - The command runner is a feature that enables you to execute any shell command you want before or after a certain event.

[Custom Branding](https://filebrowser.org/configuration/custom-branding) - You can customize your File Browser installation by change its name to any other you want, by adding a global custom style sheet and by using your own logotype if you want.

## Contributing

If you're interested in contributing to this project, our docs are best places to start [https://filebrowser.org/contributing](https://filebrowser.org/contributing).
