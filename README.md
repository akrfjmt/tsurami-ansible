# tsurami-ansible

tsurami.com個人開発環境を構築するためのPlaybook

## 行うこと

### できていること

* nginxのインストール

### TODO

* MYSQLのインストール
* PHPのインストール
* SSLの設定

## 利用手順

### 1. 仮想マシン作成

以下の構成で仮想マシンを作成する。

| 名前            | IPアドレス    | 説明            |
|-----------------|---------------|-----------------|
| tsurami-control | 192.168.56.10 | Control Machine |
| tsurami-local   | 192.168.56.20 | 開発環境        |

### 2. tarballの用意

Playbookの実行に必要なtarballをそれぞれ以下のパスに配置する。

| 項目  | ファイルパス                                                                  |
|-------|-------------------------------------------------------------------------------|
| MySQL | `tsurami-ansible/roles/mysql/files/mysql-5.7.16-linux-glibc2.5-x86_64.tar.gz` |
| nginx | `tsurami-ansible/roles/nginx/files/nginx-1.11.8.tar.gz`                       |

### 3. 必要なソフトウェアのインストール

tsurami-localにpythonをインストールする。

```bash
apt install -y python
```

tsurami-controlにansibleをインストールする。

```bash
apt-add-repository -y ppa:ansible/ansible
apt update
apt install -y ansible=2.2.0.0*
```

### 4. playbook実行

tsurami-controlでplaybookを実行する。

```bash
cd /home/tsurami-ansible
ansible-playbook -i inventories/local_hosts.ini playbooks/tsurami-local.yml
```
