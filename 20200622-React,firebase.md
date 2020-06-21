# firebaseStorage

## Storageへのファイル保存


### putメソッド

```JavaScript
    put(File)
```
これがストレージにファイルを保存するためのメソッド。
引数にはFile,Blobインスタンスを指定する必要がある。
このputメソッドを実施するために必要な知識を以下で説明。

### File()
https://developer.mozilla.org/ja/docs/Web/API/File/File

```JavaScript
    new File('①配列','②name','③option')
```

①ではinputタグのtype='file'で取得した配列を追加した。<br>
②はよくわからないけど、.pngとした。<br>
③はここでは必須項目。typeを指定しないと、ファイルの種類がapplication/octet-streamになり、firebaseストレージ内でファイルの種類が特定されなかった。ここではtype:image/pngと指定した。


```JavaScript
    const file = new File(this.file.current.files,'.png',{type:'image/png'})

```

### ストレージ参照の作成
https://firebase.google.com/docs/storage/web/create-reference<br>
やっていることとしては、ストレージへの通り道を作っているイメージ。<br>

Componentのconstructor内部でrefメソッドを変数に代入して使いやすくしたが、しなくても大丈夫だと思う。下記のように、続けてchildメソッドを実行。引数としてストレージ内部のフォルダ名と、ストレージに保存する画像につける名前をpathの形式で指定。その後に続けて前述のputメソッドを実行することでファイルをストレージに保存できる。<br>
putメソッドはPromiseが返るようなので、thenとcatchで成功失敗に備える。

```JavaScript
  this.storageRef.child('images/images3').put(file)
  .then(snapshot=> console.log('成功'))
  .catch(error => console.log(error))

```


