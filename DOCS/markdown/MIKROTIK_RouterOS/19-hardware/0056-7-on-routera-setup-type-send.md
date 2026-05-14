## 7.  On `RouterA` setup type `send` : 

```
/disk/btrfs/transfer add type=send fs=BtrfsDisk ssh-address=RouterB send-subvolumes=Documents-23012025
ssh-user=btrfstransfer ssh-receive-mount=BackupBtrfsDisk/Snapshots
```

Where: 

- `BtrfsDisk` is the Btrfs disk label found under `/disk/btrfs/filesystem print` on `RouterA` - `Documents-23012025` is the snapshots name (not the path) 

1691 

   - `btrsfstransfer` is the SSH user on `RouterB` 

   - `BackupBtrfsDisk` is the Btrfs disk label found under `/disk/btrfs/filesystem print` on `RouterB` 

   - `Snapshots` is the subvolumes under for your snapshots under `BackupBtrfsDisk` 

8.  On `RouterB` setup type `receive` : 

```
/disk/btrfs/transfer/add fs=BackupBtrfsDisk type=receive file=BackupBtrfsDisk/Snapshots
```

Where: 

- `BackupBtrfsDisk` is the Btrfs disk label found under `/disk/btrfs/filesystem print` on `RouterB` - `BackupBtrfsDisk/Snapshots` is the mount path for `Snapshots` subvolume
