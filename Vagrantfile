# yamlファイルから設定の読み込み
require 'yaml'
# =============================================================================
# パラメータは「./playbooks/group_vars/all.yml」で編集
# =============================================================================
params = YAML.load_file("./playbooks/group_vars/all.yml")

# Vagrantの設定
Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-6.8"
  config.vm.box_check_update = true

  # デフォルトでインストールするプラグイン
  config.plugin.add_dependency "vagrant-vbguest"
#  config.plugin.add_dependency "vagrant-proxyconf"

  # VirtualBox固有の設定
  config.vm.provider "virtualbox" do |vb|
    # Vagrant で VirtualBox 5.0 の準仮想化を有効にする
    vb.customize ['modifyvm', :id, '--paravirtprovider', 'kvm']

    # IPv6とDNSでのネットワーク遅延対策
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
  end

  # host名の設定
  config.vm.hostname = params["hostname"]

  # ipaddressの設定(http://labs.septeni.co.jp/entry/20140707/1404670069)
  config.vm.network :private_network, ip: params["ip_address"]

  # ポートの設定
  config.vm.network :forwarded_port, guest: 80, host: params["httpPort"], id: "http", auto_correct: true, host_ip: "127.0.0.1"
  config.vm.network :forwarded_port, guest: 22, host: params["sshPort"],  id: "ssh" , auto_correct: true, host_ip: "127.0.0.1"

  # Proxyの設定
#  if Vagrant.has_plugin?("vagrant-proxyconf")
#    config.proxy.http     = "http://192.168.0.2:3128/"
#    config.proxy.https    = "http://192.168.0.2:3128/"
#    config.proxy.no_proxy = "localhost,127.0.0.1"
#  end

  # フォルダ同期の設定
#  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  config.vm.synced_folder params["host_folda"], params["client_folda"], type: "virtualbox"
#  config.vm.synced_folder "./source", "/var/www/html", create: true, disabled: false, owner: "nginx", group:"nginx", mount_options: ["dmode=775", "fmode=775"], type: "virtualbox"
#  config.vm.synced_folder ホストのフォルダ, ゲストのフォルダ, ホスト上にディレクトリが存在しなかった場合は作成するかどうか, 共有するかどうか, 所有者, 所有グループ, 所有権限(dmode[ディレクトリ], fmode[ファイル]), 共有タイプ

  # Ansibleでの初期設定
  config.vm.provision "ansible_local" do |ansible|
    ansible.inventory_path = "./playbooks/hosts/development"
    ansible.playbook       = "./playbooks/site.yml"
    ansible.limit          = "all"
  end

  # shellで初期設定(ユーザ vagrant で shell を実行。provision 時には sudo を使用して shell が実行されている)
  # yum updateを毎回実行する
  config.vm.provision "shell", inline: "yum update -y", run: "always"

  # httpdが自動起動しない対策
  config.vm.provision "shell", inline: "service httpd restart", run: "always"

#  config.vm.provision "shell", path: "./setup/scripts/move_files.sh", privileged: true

  # ファイルの転送(Vagrantユーザのホームディレクトリに配置される)
#  config.vm.provision "file", source: "./setup/files/host", destination: "php.ini"
end
