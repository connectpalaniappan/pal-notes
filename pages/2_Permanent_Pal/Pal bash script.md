	---
tags:
 - resource/script
 - resource/commands
 - resource/git
 - resource/backup
---

```shell
cd ~/Google\ Drive/Dropbox
find . -name "Icon?" -print0 | xargs -0 rm -rf
cd ~/Google\ Drive/Dropbox/artifacts/scripts_bash
```

[[archival]]

```shell
sh archival.sh ../../../Private/family-resources ~/Google\ Drive/Archive
sh archival.sh ../../../Public/life-resources ~/Google\ Drive/Archive
sh archival.sh ../../../Public/tech-resources ~/Google\ Drive/Archive
sh archival.sh ../../../Dropbox ~/Google\ Drive/Archive
```

[[Git]] [[Data Backup]]

#### Notes 
```bash 
sh backup_git.sh ../../tech-notes 
sh backup_git.sh ../../family-notes
sh backup_git.sh ../../life-notes
sh backup_git.sh ../../pal-notes
sh backup_git.sh ../../uma-notes
sh backup_git.sh ../../../Public/tech-coding/code-practice
```

#### Public resources 
```bash 
sh backup_git.sh ../../../Public/tech-resources/
sh backup_git.sh ../../../Public/life-resources/

```

#### Private resources 
```bash 
sh backup_git.sh ../../../Private/family-resources/
```

#### Config backs 
```bash
sh backup_git.sh .

cp -r ../../.obsidian-pal-mac-intel/* ../../obsidian-config/.obsidian-pal-mac-intel
cp -r ../../.obsidian-pal-mac-m1/* ../../obsidian-config/.obsidian-pal-mac-m1
cp -r ../../.obsidian-uma/* ../../obsidian-config/.obsidian-uma
sh backup_git.sh ../../obsidian-config

```

-----

### git sync plugin (Not needed as not using both office laptops)

```bash
cp -rf ../../../Dropbox/obsidian-config/.obsidian-pal-mac-m1/plugins/ ../../../Dropbox/.obsidian-pal-mac-intel/plugins/
cp ../../../Dropbox/obsidian-config/.obsidian-pal-mac-m1/community-plugins.json  ../../../Dropbox/.obsidian-pal-mac-intel/community-plugins.json
cat ../../../Dropbox/.obsidian-pal-mac-m1/community-plugins.json
ls ../../../Dropbox/.obsidian-pal-mac-m1/plugins
```



```shell
```