# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'

VERSION = '2'

Vagrant.configure(VERSION) do |config|
    boxes = [
        { :name => 'ubuntu-1804-box', :box => 'generic/ubuntu1804' },
        { :name => 'ubuntu-2004-box', :box => 'generic/ubuntu2004' },
    ]

    boxes.each do |opts|
        config.vm.define opts[:name] do |config|
            config.vm.provider 'libvirt' do |libvirt|
                # Used box image
                config.vm.box = opts[:box]

                # stuff
                libvirt.driver = 'kvm'
                libvirt.memory = 1024
                libvirt.cpus = 1
            end

            if opts[:name] == boxes.last[:name]
                config.vm.provision 'ansible' do |ansible|
                    ansible.playbook = 'playbook.yml'
                    ansible.limit = 'all'
                end
            end
        end
    end
end
