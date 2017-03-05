# VagrantをAnsibleで構成する

## VirtualBox
- [ダウンロード](https://www.virtualbox.org/wiki/Downloads)

### ダウンロード・インストールするもの
- platform packages
- Oracle VM VirtualBox Extension Pack

## Vagrant
- [ダウンロード](https://www.vagrantup.com/downloads.html)
- [ドキュメント](https://www.vagrantup.com/docs/)

### 公式Box
- [CentOS6](https://atlas.hashicorp.com/centos/boxes/6)
- [CentOS7](https://atlas.hashicorp.com/centos/boxes/7)

### 事前にインストールするPlugin

#### vagrant-multiplug
使用するプラグインを Vagrantfile に書いておくことで、自動インストールしてくれる。
```
vagrant plugin install vagrant-multiplug
```

### Plugins

#### vagrant-vbguest
ホスト(自分のPC)の VirtualBox の Guest Addition バージョンと Box にインストールされている Guest Addition のバージョンが違う場合に、ホスト(自分のPC)の VirtualBox の Guest Addition のバージョンに合わせてくれる。

#### vagrant-proxyconf
Vagrantで作成するゲスト(VirtualBox)にProxy設定をする。  
`yum update` 等ネットワーク接続する際にProxy経由でネットワーク接続できるようにする。

#### vagrant-hostsupdater
Vagrant を起動するときに、ホスト(自分のPC)の /etc/hosts を Vagrantfile に記述したものに設定してくれる。  
ただし、コマンドプロントを管理者で実行する必要がある。

### Vagrant コマンド
- 起動 `vagrant up`
- 再セットアップ `vagrant provision`
- 停止 `vagrant halt`
- 再起動 `vagrant reload`
- 廃棄 `vagrant destroy`

## Ansible
- [Ansible実践入門](http://dev.classmethod.jp/server-side/ansible/practice_ansible/)
- [Ansibleを効果的に使うのに欠かせないPlaybookの基本的な書き方まとめ](http://www.atmarkit.co.jp/ait/articles/1607/26/news013.html)
- [Ansibleにおける環境構築やリリース作業でよく使う5つのModule+α](http://www.atmarkit.co.jp/ait/articles/1606/10/news017.html)
- [Ansible Documentation](http://docs.ansible.com/ansible/index.html)
