# filebrowser

change volumes first (docker-compose.yml).


if using external disk, register first:
- get uuid
```sh
sudo blkid
```

- add new line
```sh
sudo nano /etc/fstab
```

with:
```
UUID="1234-5678" /media/deb/New_Volume ntfs defaults,nofail,x-systemd.automount,x-systemd.requires=network.target 0 0
```

then :
```
sudo systemctl daemon-reload
sudo mount -a
reboot
```

```
docker-compose up -d
```