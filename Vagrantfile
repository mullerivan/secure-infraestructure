# vim: ft=ruby:expandtab:tabstop=2:softtabstop=2:shiftwidth=2

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
#################Nagios
    config.vm.define vm_name = "nagios" do |nagios|#
       # Mount shared folder using nfs because is much faster
       nagios.vm.network "forwarded_port", guest: 80, host: 9088       
       nagios.vm.network :private_network, ip: "10.22.22.10"
       nagios.vm.provision "ansible" do |ansible|
         ansible.playbook = "playbooks/nagios.yml"
         ansible.host_key_checking = false
         ansible.verbose = 'vvvv'

       end 
  
       nagios.vm.provider :virtualbox do |vb|
         vb.customize ["modifyvm", :id, "--memory", "512"]
         vb.customize ["modifyvm", :id, "--cpus", "1"]
       end
   end
#################Servidor de mails
    config.vm.define vm_name = "mail" do |mail|
      mail.vm.network "forwarded_port", guest: 25, host: 9025      
      mail.vm.network :private_network, ip: "10.22.22.20"
      mail.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbooks/mail.yml"
        ansible.host_key_checking = false
      end
      mail.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
    end
################Servidor web
    config.vm.define vm_name = "web" do |web|
      web.vm.network "forwarded_port", guest: 80, host: 9080      
      web.vm.network :private_network, ip: "10.22.22.30"
      web.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbooks/web.yml"
        ansible.host_key_checking = false
      end
      web.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
    end
  
###############wiki server
    config.vm.define vm_name = "wiki" do |wiki|
      wiki.vm.network "forwarded_port", guest: 80, host: 9081      
      wiki.vm.network :private_network, ip: "10.22.22.40"
      wiki.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbooks/wiki.yml"
        ansible.host_key_checking = false
      end
      wiki.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
    end
###################Firewall
    config.vm.define vm_name = "firewall" do |firewall|
      #firewall.vm.network "forwarded_port", guest: 25, host: 9025      
      firewall.vm.network :private_network, ip: "10.22.22.111"
      firewall.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbooks/firewall.yml"
        ansible.host_key_checking = false
      end
      firewall.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "512"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
    end
######################### NfSen
  config.vm.define vm_name = "nfsen" do |nfsen|
  #firewall.network "forwarded_port", guest: 9995, host: 9995   
    nfsen.vm.network :private_network, ip: "10.22.22.50"
    nfsen.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/nfsen.yml"
      ansible.host_key_checking = false
    end
    nfsen.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--cpus", "1"]
    end
  end

end
