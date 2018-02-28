# vagrant
Template set for deploying a ubuntu server and configure it with ansible

## requirements
    - vagrant
    - virtualbox
    - virtualbox extention pack
    - ansible 2.x

## Usage
```bash
cd provision
cp vars.yaml.sample vars.yaml
vim vars.yaml
# change your settings

cd files
cat ~/.ssh/id_rsa.pub > public.rsa.key

cd ../../
vim servers.yaml
# change your settings

vagrant up
```
