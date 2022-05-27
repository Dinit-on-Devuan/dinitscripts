## Basic scripts for booting a Devuan with Dinit

## What is this?
These files are scripts for dinit, and you can use them to boot a Devuan using Dinit.

## What is included?
This project includes any script needed to boot a Devuan with Dinit.

| Service name  | Description                                                  | Note                          |
| ------------- |:------------------------------------------------------------:| -----------------------------:|
| boot          | First service started by dinit at boot time                  | Its start other services      |
| pseudofs      | Mounting /proc & other kernel virtual file systems           |                               |
| udevd         | Udev device (/dev) manager                                   | eudev used on Devuan          |
| udev-trigger  | Trigger udev events for already-present devices              |                               |
| udev-sttele   | #ToDo                                                        |                               |
| tmpfs         | Mounting /tmp                                                |                               |
| swap          | Mount swap partition/files                                   | NOT enabled by default!       |
#ToDo