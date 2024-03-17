---
tags:
 - resource/script
 - resource/commands
 - resource/git
 - resource/backup
---

[[archival]]

```
sh archival.sh ../../../Private ~/Google\ Drive/Archive
sh archival.sh ../../../Public ~/Google\ Drive/Archive
sh archival.sh ../../../Dropbox ~/Google\ Drive/Archive
```

[[git]] [[backup]]

```bash
sh backup_git.sh ../../family-notes
sh backup_git.sh ../../life-notes
sh backup_git.sh ../../tech-notes
sh backup_git.sh ../../pal-notes
sh backup_git.sh ../../uma-notes

cp -r ../../../Dropbox/.obsidian-pal-mac-intel/* ../../../Dropbox/obsidian-config/.obsidian-pal-mac-intel
cp -r ../../../Dropbox/.obsidian-pal-mac-m1/* ../../../Dropbox/obsidian-config/.obsidian-pal-mac-m1
cp -r ../../../Dropbox/.obsidian-uma/* ../../../Dropbox/obsidian-config/.obsidian-uma
sh backup_git.sh ../../../Dropbox/obsidian-config/

sh backup_git.sh ../../life-resources/
sh backup_git.sh . 
sh backup_git.sh ../../tech-coding/code-practice/
sh backup_git.sh ../../tech-resources/

sh backup_git.sh ../../../Private/family-resources/

```

### git sync plugin
```bash
cp -r ../../../Dropbox/obsidian-config/.obsidian-pal-mac-m1/plugins ../../../Dropbox/.obsidian-pal-mac-intel/plugins/
cp ../../../Dropbox/obsidian-config/.obsidian-pal-mac-m1/community-plugins.json  ../../../Dropbox/.obsidian-pal-mac-intel/community-plugins.json
cat ../../../Dropbox/.obsidian-pal-mac-m1/community-plugins.json
ls ../../../Dropbox/.obsidian-pal-mac-m1/plugins
```
