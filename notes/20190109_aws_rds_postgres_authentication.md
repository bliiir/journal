*Journal*
Rasmus Groth
*20190108, Utterslev, Copenhagen, Denmark*

---

## [AWS RDS postgres authentication](https://stackoverflow.com/a/26735105/9536012)

Error message:
```
FATAL: Peer authentication failed for user
```

Edit
```
pg_hba.conf
```

Change:
```
local   all             postgres                                peer
```
To:
```
local   all             postgres                                trust
```
Restart postgres
```
sudo service postgresql restart
```

### [Change password for root user](https://aws.amazon.com/premiumsupport/knowledge-center/set-change-root-linux/)
