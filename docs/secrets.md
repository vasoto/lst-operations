# Secrets

| Name                                   |        Alias         |          IP           |        User        |        Pwd        | Notes              |
| -------------------------------------- | :------------------: | :-------------------: | :----------------: | :---------------: | ------------------ |
| LST1                                   |        `lst`         |     `161.72.87.1`     |    `CtAlAPaLmA`    |  `cTa-LsT_u53r`   |                    |
| cp* (01, 02)                           |        `cp*`         |                       | `vassil.verguilov` |    {LDAP PWD}     | Jump `lst`         |
| tcs* (01-07)                           |        `tcs*`        | `10.200.10.(101-107)` |     `control`      | `cTa-LsT_C0ntr01` | Jump through `lst` |
| Webserver                              |      `lst1.web`      |    `161.72.87.51`     |       `root`       |    `t1tMepS0`     |
|                                        |                      |                       |       `lst1`       |   `t1twsoLST1`    |                    |
|                                        |                      |                       |       `www`        |    `htSama1c`     |                    |
| Webserver (backup)                     |   `lst.web-backup`   |    `161.72.87.52`     |       --"--        |       --"--       |                    |
| Operator Machines operator* (1-6)      |     `operator*`      |   `10.204.80.(1-6)`   |   `lstoperator`    |    `latootCTA`    | jump through `lst` |
| monitor1=operator5, monitor2=operator6 |                      |                       |                    |                   |                    |
|                                        |                      |                       |       `root`       |    `t1R4msiCC`    |                    |
|                                        |                      |                       |      `admin`       |  `bigtelescope1`  | Webcam passwords   |
| ControlCC                              |   `lst.controlcc`    |    `10.204.80.50`     |       --"--        |       --"--       | Jump through `lst` |
| Spare Operator                         | `lst.operator-spare` |     `10.204.80.7`     |       --"--        |       --"--       | Jump through `lst` |
| Backup                                 |    `lst.backupcc`    |    `161.72.126.66`    |     `ccadmin`      |                   | Jump through `lst` |
| NAS                                    |      `lst.nas`       |    `161.72.87.71`     |       `lst1`       |  `bigtelescope1`  |                    |
| Weather Station/Safety collector       |    `lst.weather`     |      `10.1.12.1`      |       `root`       |    `t1R4PmCTA`    |                    |
