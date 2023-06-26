$setup_timezone = <<-SCRIPT
echo "Setting up timezone data"
SCRIPT

$setup_postgres_db = <<-'SCRIPT' 
echo "Setting up PostgreSQL database" 
sudo apt-get install wget ca-certificates
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ focal-pgdg main"> /etc/apt/sources.list.d/pgdg.list'
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo dpkg --configure -a
sudo apt-get update 
export LANGUAGE=en_US.UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
locale-gen en_US.UTF-8
sudo dpkg-reconfigure locales
sudo DEBIAN_FRONTEND=noninteractive apt install -y postgresql-8.4
SCRIPT

Vagrant.configure("2") do |config|
  
  config.vm.box = "focal"
  #config.vm.box_version = "6.1"
  config.vm.provision :shell, inline: $setup_timezone

  config.vm.define "postgres" do |postgres|
    postgres.vm.provision :shell, inline: $setup_postgres_db
  end
end