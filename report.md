# Report

## about this file

開発中に詰まったところをメモしておく

## sveasy

eguiに倣ってsvg + easyでsveasy(エスブイジー)にしようかな

## egui

Rustで自由度高めのUI作れるcrateを使えるようになりたいから`egui`っていうのを試そう
どうやら`eframe`っていうフレームワークで開発してくのがセオリーっぽい
> [egui](https://github.com/emilk/egui)
> [eframe](https://github.com/emilk/egui/tree/main/crates/eframe)

## wsl
wsl上でデフォルトではなぜかWaylandがディスプレイに設定されて要るっぽいので以下の設定を`.bashrc`に追加した

```bashrc
export XDG_SESSION_TYPE=x11
export WAYLAND_DISPLAY=""
```

## 環境

wsl上で動かしてみる
→やたらと重い。リリースビルドなのに
→よくわからんしwasmにしようかな、デモはかなりスムーズに動いてたし
→ついでにeframe\_templateを採用しよう
→eframe\_templateのwasmめっちゃ軽快に動くわ
→templateのネイティブもめっちゃ軽快に動くんだけど前のゴミみたいな動きは何だったん
→これならネイティブでいいな


## eframe\_template

`eframe`にはテンプレートが用意されていて`eframe_template`をリポジトリのテンプレートとしてスタートした
>[eframe\_template](https://github.com/emilk/eframe_template)

どうやらREADMEにはプロジェクトに応じて変更すべき箇所が書かれているのでそれを変更する

## build

`eframe_template`に書いてある方法に従ってみる

### wsl

`eframe_template`クローンしてきて`cargo run --release`したら動いた。


### wasm

1. `rustup target add wasm32-unknown-unknown`
2. `cargo install --locked trunk`
3. `trunk serve`
4. localhostで`http://127.0.0.1:8080`にサーバーが立つ

>1. Install the required target with rustup target add wasm32-unknown-unknown.
>2. Install Trunk with cargo install --locked trunk.
>3. Run trunk serve to build and serve on http://127.0.0.1:8080. Trunk will rebuild automatically if you edit the project.
>4. Open http://127.0.0.1:8080/index.html#dev in a browser. See the warning below.


wasmは初心者でよくわからんけど、どうやらtrunkっていうツールがよさげらしい？eframeでは使われているっぽい
web assemblyのコンパイルとバンドルをしてサーバーも立ててくれるぽい
なんかwasmはやたらと環境設定が多いイメージだったから意外とシンプルだな
→でも結局ローカルファイルをいじるのにはjavascript叩かんといけないのがしんどそうだな

## svg

仕様読んでるけど結構いろいろできて面白そうだな
rustでは`resvg`っていうsvgレンダーライブラリで使われている`usvg`というのがあるらしいのでそれを使う
>[usvg](https://docs.rs/usvg/0.45.1/usvg/index.html)

