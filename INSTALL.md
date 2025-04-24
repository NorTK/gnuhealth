# Installation instructions

## Build gnuhealth container image

- Move into the gnuhealth container file directory

`cd gnu-health-containerfile`

- Build the container image by running the following command:

`podman build . -f Containerfile -t gnuhealth:v44`

- Verify that the container image has been created locally

```bash
$ podman images
REPOSITORY                               TAG               IMAGE ID      CREATED         SIZE
localhost/gnuhealth                      v44               07d948c82ced  20 minutes ago  2.45 GB
```

## Run the application quadlets

- Create the podman secret for the postgres quadlet

[!NOTE]
The reason for having the secret in a **vulnerable plain text file** is for the solely purpose of not having the password typed in the console and -thus- appear in the command history.
This is an insecure not sanctioned practice and MUST NOT be implemented in productive environments.

`cat postgres_password.txt | podman secret create postgres_password -`

If having the secret creation in the command history is not an issue, the following command may be used alternatively:

`echo gnusolidario | podman secret create postgres_password -`

- Make sure that quadlets directory exists

`mkdir -p $HOME/.config/containers/systemd`

- Move quadlets to systemd directory

```bash
cp *.container $HOME/.config/containers/systemd/
cp *.network $HOME/.config/containers/systemd/
```

- Invoke systemd daemon reload

`systemctl --user daemon-reload`
