## Progress

echo "10.1.1.33 chef-server.test" | tee -a /etc/hosts

cp server/secrets/admin.pem .chef/
knife ssl fetch
knife ssl check

knife cookbook upload learn_chef_apache2
knife cookbook list

vagrant ssh-config

knife bootstrap localhost --ssh-port 2200 --ssh-user vagrant --sudo --identity-file ./server/.vagrant/machines/node1-ubuntu/virtualbox/private_key --node-name node1-ubuntu --run-list 'recipe[learn_chef_apache2]'

knife node list
knife node show node1-ubuntu
curl 10.1.1.34

## modify index.html.erb and metadata to 0.2.0

```bash
# upload cookbook to chef-server
knife cookbook upload learn_chef_apache2
knife cookbook list

knife ssh localhost --ssh-port 2200 'sudo chef-client' --manual-list --ssh-user vagrant --identity-file ./server/.vagrant/machines/node1-ubuntu/virtualbox/private_key

curl 10.1.1.34
```

## Use community cookbooks with Berkshelf

berks install
SSL_CERT_FILE='.chef/trusted_certs/chef-server_test.crt' berks upload

## Create a role

mkdir -P roles
knife role from file roles/web.json
knife role list
knife role show web
knife node run_list set node1-ubuntu "role[web]"
knife node show node1-ubuntu --run-list

knife ssh localhost --ssh-port 2200 'sudo chef-client' --manual-list --ssh-user vagrant --identity-file ./server/.vagrant/machines/node1-ubuntu/virtualbox/private_key

knife status 'role:web' --run-list

## Delete from chef-server

```bash
# Delete node and client
knife node delete node1-ubuntu --yes
knife client delete node1-ubuntu --yes

# Delete cookbook
knife cookbook delete learn_chef_apache2 --all --yes

# Delete role
knife role delete web --yes
```
