http://www.gnu.org/software/libtool/manual/html_node/Updating-version-info.html
  * Finalise human-readable changelog! (ChangeLog)
  * Report any important code changes (NEWS)
  * Commit all these files
```
export LIBNFC_RELEASE=1.7.1
git add NEWS ChangeLog configure.ac CMakeFiles.txt
git commit -m"Prepare $LIBNFC_RELEASE version"
git push
```
  * Check tarball distribution:
```
cd /tmp
git clone https://code.google.com/p/libnfc/
cd libnfc
autoreconf -is
./configure
make distcheck
cd ..
rm -rf libnfc/
```
  * Add a git tag
```
git tag -s libnfc-$LIBNFC_RELEASE -m"libnfc $LIBNFC_RELEASE"
git push origin libnfc-$LIBNFC_RELEASE
```
  * Build tarball archive
```
cd /tmp
git clone https://code.google.com/p/libnfc/
cd libnfc
sh make_release.sh
```
  * Backup archives
```
scp libnfc-*$LIBNFC_RELEASE* libnfc:~/libnfc/
```

  * Upload archives to https://bintray.com/nfc-tools/sources/libnfc/

  * Update API at http://www.libnfc.org/api/
```
ssh libnfc
update-api.sh libnfc/libnfc-doc-$LIBNFC_RELEASE.zip
```

  * Announce on forum http://www.libnfc.org/community/forum/1/news-announcements/