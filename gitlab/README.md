# GitLab Setup

## 1. Prerequisites

### 1.1. GitLab Runner Server

- 10.50.16.7 (gitlab_runner)
- ncloud (gitlab_runner)

### 1.2. GitLab Server

- 10.50.0.6 (gitlab-public)
- 10.50.16.6 (gitlab)
- ncloud (gitlab)

### 1.3. Bastion Host

`ssh -i ~/.ssh/dev-bastion1-key.pem ncloud@27.96.149.181`

### 1.3. Install Ansible

```bash
sudo apt update
sudo apt install ansible-core
```

## 2. Setup

```bash
ansible-playbook -i inventory.ini playbook.yaml

J2@f3g?d-6Dq


# PostgreSQL DB
# host : pg-2voq8s.vpc-cdb-kr.gov-ntruss.com:5432
# db : gitlab
# ID/PW : admin_cr / megazone!2024
psql -h pg-2voq8s.vpc-cdb-kr.gov-ntruss.com -p 5432 -U admin_cr -W gitlab

# bastion-server ( 27.96.149.181, 10.50.0.6 )
# ID/PW : ncloud / J2@f3g?d-6Dq

#ID/PW : ncloud / L3+F6M?hP2t
#Public IP : 27.96.149.206
ssh ncloud@10.50.0.7


# gitlab ( 10.50.16.6 )
# ID/PW : ncloud / T6+?fJiPL9u

# gitlab-runner ( 10.50.16.7 )
# ID/PW : ncloud / A6?riuq%nPf

# gitlab-public: 27.96.149.206, 10.50.0.5



```

## volume mount

```bash
sudo rsync -av /opt/ /tmp/opt-backup/

sudo fdisk /dev/vdb
sudo mkfs.ext4 /dev/vdb1
sudo mount /dev/vdb1 /opt
sudo rsync -av /tmp/opt-backup/ /opt/
sudo vi /etc/fstab
  /dev/vdb1 /opt ext4 defaults 0 2


```

## GitLab initial setup

id: root

Password: You didn't opt-in to print initial root password to STDOUT.
Password stored to /etc/gitlab/initial_root_password. This file will be cleaned up in first reconfigure run after 24 hours.

```bash
sungyong@gitlab-public:~$ docker exec -it a664f0258881 bash
root@gitlab-public:/# cat /etc/gitlab/initial_root_password
# WARNING: This value is valid only in the following conditions
#          1. If provided manually (either via `GITLAB_ROOT_PASSWORD` environment variable or via `gitlab_rails['initial_root_password']` setting in `gitlab.rb`, it was provided before database was seeded for the first time (usually, the first reconfigure run).
#          2. Password hasn't been changed manually, either via UI or via command line.
#
#          If the password shown here doesn't work, you must reset the admin password following https://docs.gitlab.com/ee/security/reset_user_password.html#reset-your-root-password.

Password: rD+NlTC3cQJEUpBtTSa8KpdO4M7sN8r6cxd8aIHQbv4=

# NOTE: This file will be automatically deleted in the first reconfigure run after 24 hours.
root@gitlab-public:/# 
```

<http://27.96.149.206>

### reset password

```bash
 docker exec -it gitlab /bin/bash
      gitlab-rails console -e production
           user = User.find_by(username: 'root')
     user.password = 'newpassword'
     user.password_confirmation = 'newpassword'
user.save!
```

## 국방망

- docker를 Offline 설치
- 필요한 설치

## sshuttle

```bash
sshuttle -r ncloud@27.96.149.181 -x 10.50.0.0/24 10.50.16.0/24
sudo sshuttle -r ncloud@bastion 0.0.0.0/0

```
