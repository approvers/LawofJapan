# 法律バルクデータ全取得

```
$ curl -sS https://elaws.e-gov.go.jp/download/lawdownload.html|grep lawdata_download|sed -E 's/(.+)([0-9]{3}\.zip)(.+)/\2/'|while read line;do echo https://elaws.e-gov.go.jp/download/$line;done|aria2c -i -
```
