---
tags:
 - tech/script
 - tech/commands
 - 
---

[[archival]]

```
sh archival.sh ../../../Private ~/Google\ Drive/Archive
sh archival.sh ../../../Public ~/Google\ Drive/Archive
sh archival.sh ../../../Dropbox ~/Google\ Drive/Archive
```

[[git]] [[backup]]

```bash
sh backup_git.sh ../../../Dropbox/family-notes
sh backup_git.sh ../../../Dropbox/life-notes
sh backup_git.sh ../../../Dropbox/tech-notes
sh backup_git.sh ../../../Dropbox/pal-notes
sh backup_git.sh ../../../Dropbox/uma-notes

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
cp -r ../../../Dropbox/obsidian-config/.obsidian-pal-mac-intel/plugins ../../../Dropbox/.obsidian-pal-mac-m1/plugins/
cp ../../../Dropbox/obsidian-config/.obsidian-pal-mac-intel/community-plugins.json  ../../../Dropbox/.obsidian-pal-mac-m1/community-plugins.json
cat ../../../Dropbox/.obsidian-pal-mac-m1/community-plugins.json
ls ../../../Dropbox/.obsidian-pal-mac-m1/plugins
```
