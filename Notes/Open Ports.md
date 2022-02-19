# Open Ports

## List all ports

```
sudo firewall-cmd --list-all
```

## Open port for Zones

```
sudo firewall-cmd --zone=public --add-port=5000/tcp --permanent
```

## Reload

```
firewall-cmd --reload
```