# 日本の法律

**法律全部gitに乗せる**

TODO
- [ ] 法律取得の並列化
- [ ] 法律取得の自動化
  - [ ] 時間かRSSをトリガーにしていい感じにやる
- [ ] 法律取得をDocker内部でやる
- [ ] 法律取得をGithub Actionsで動かす


# 法律バルクデータ全取得コマンド

```
$ curl -sS https://elaws.e-gov.go.jp/download/lawdownload.html|grep lawdata_download|sed -E 's/(.+)([0-9]{3}\.zip)(.+)/\2/'|while read line;do echo https://elaws.e-gov.go.jp/download/$line;done|aria2c -i -
$ unzip *.zip
$ rm *.zip
$ find|grep xml|while read line;do cat $line ;echo xq . $(echo $line | sed -e 's/xml/zip/') ;done
$ find|grep xml|xargs rm
$ find|grep pict|xargs rm -rf
```

# LawNum2FileName.jsonの生成

```
$ find|grep json|while read line;do jq -r .Law.LawNum $line|tr -d '\n';echo " $(basename $line)";done|jq -R 'input | split(" ")| {LawNum:(.[0]), FileName: (.[1])}' > LawNum2FileName.json
```
