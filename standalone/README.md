## Initial environment

sudo apt-get update
sudo apt-get install -y git curl vim
curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P chefdk -c stable

## Configure a resource

chef-client --local-mode hello.rb
chef-client --local-mode goodbye.rb
chef-client --local-mode hello-dir.rb

## Configure a package and service

sudo chef-client --local-mode webserver.rb

## Make your recipe more manageable

mkdir cookbooks
chef generate cookbook cookbooks/learn_chef_apache2
chef generate template cookbooks/learn_chef_apache2 index.html

sudo chef-client --local-mode --runlist 'recipe[learn_chef_apache2]'
sudo chef-client --local-mode --runlist 'recipe[learn_chef_apache2::default]'
