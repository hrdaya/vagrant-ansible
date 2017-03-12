# VagrantをAnsibleで構成する

## VirtualBox
- [ダウンロード](https://www.virtualbox.org/wiki/Downloads)

### ダウンロード・インストールするもの
- platform packages
- Oracle VM VirtualBox Extension Pack

## Vagrant
- [ダウンロード](https://www.vagrantup.com/downloads.html)
- [ドキュメント](https://www.vagrantup.com/docs/)

現状で VirtualBox5.1系 と Vagrant1.9.2 では問題が発生しているので現状では Vagrant1.9.1 をインストールすることをお勧めします。  
参考：[vagrant up で共有ファイルがマウントできなくなった](http://qiita.com/hirdot/items/7057ee1a13468191e184)

### 公式Box
- [CentOS6](https://atlas.hashicorp.com/centos/boxes/6)
- [CentOS7](https://atlas.hashicorp.com/centos/boxes/7)

### 事前にインストールするPlugin

#### vagrant-multiplug
使用するプラグインを Vagrantfile に書いておくことで、自動インストールしてくれる。
```
vagrant plugin install vagrant-multiplug
```

### よく使うPlugins

#### vagrant-vbguest
ホスト(自分のPC)の VirtualBox の Guest Additions バージョンと Box にインストールされている Guest Additions のバージョンが違う場合に、ホスト(自分のPC)の VirtualBox の Guest Additions のバージョンに合わせてくれる。  
公式のBoxには Guest Additions が入っていないのでこのプラグインを入れておくことで自動でインストールしてくれる。(自分で入れるのは面倒な手順が必要)

#### vagrant-proxyconf
Vagrantで作成するゲスト(VirtualBox)にProxy設定をする。  
`yum update` 等ネットワーク接続する際にProxy経由でネットワーク接続できるようにする。

### よく使うVagrant コマンド
- 起動 `vagrant up`
- 再セットアップ `vagrant provision`
- 停止 `vagrant halt`
- 再起動 `vagrant reload`
- 廃棄 `vagrant destroy`

### Vagrantドキュメント意訳
- [【Vagrantドキュメント意訳】05.コマンドライン・インタフェース](http://qiita.com/ringo0321/items/c3720a54855e9c961a91)
- [【Vagrantドキュメント意訳】08.Box](http://qiita.com/ringo0321/items/f76da11503c627205c52)
- [【Vagrantドキュメント意訳】09.プロビジョニング](http://qiita.com/ringo0321/items/38743442a9abfc3be5b2)
- [【Vagrantドキュメント意訳】10.ネットワーク](http://qiita.com/ringo0321/items/4ebc0ac3bb98240f65ce)
- [【Vagrantドキュメント意訳】11.同期フォルダ](http://qiita.com/ringo0321/items/aec4c543cce63e60a529)
- [【Vagrantドキュメント意訳】12.マルチ・マシン](http://qiita.com/ringo0321/items/1a6ebccfb2733f6e2de1)

### オリジナルのBOXを作成する
- [CentOS 7のVagrant BOXを新規にインストールして作成する](http://tmick.net/centos7-vagrant-box/)

## Ansible
- [Ansible実践入門](http://dev.classmethod.jp/server-side/ansible/practice_ansible/)
- [Ansibleを効果的に使うのに欠かせないPlaybookの基本的な書き方まとめ](http://www.atmarkit.co.jp/ait/articles/1607/26/news013.html)
- [Ansibleにおける環境構築やリリース作業でよく使う5つのModule+α](http://www.atmarkit.co.jp/ait/articles/1606/10/news017.html)
- [Ansible Documentation](http://docs.ansible.com/ansible/index.html)
