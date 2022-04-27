# Transferring Files Between A Device And Raspberry Pi

To transfer files between the Raspberry Pi and the host device or vice versa we use a simple command called `scp`. Now I like to use a headless Raspbian OS without a GUI on the Raspberry Pi as it saves resources which would be otherwise spent unnecessarily.

# What is SCP?

SCP short for Secure Copy uses SSH (secure shell) to transfer files between 2 devices. In my experience I hae tested this out with movies as big as 3GB. Although yes it does take some time it has been one of the easiest and convenient method for me!

# Syntax

```shell
scp example.mp4 pi@192.168.1.1:/home/pi/Movies
```

For downloading files from the other computer/server to the local machine

```shell
scp username@192.168.1.1:path_to_file path_in_the_local_machine
```

You have to replace `example.mp4` with the file you intend to copy over, replace the `pi@192.168.1.1` with your SSH address and `/home/pi/Movies` with the path you want your movie to be in.

## Additional Points

1) If you are sending a folder don't forget to add a `-r` (recursive tag)
2) You can send multiple files/folders just by adding them one after another (with space) after `example.mp4`