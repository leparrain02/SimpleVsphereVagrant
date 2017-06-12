# -*- mode: ruby -*-
# vi: set ft=ruby :

vsphere_host = "vcenter-host"
vsphere_user = "vcenter-user"
vsphere_password = "vcenter-password"
template_basedir = "Templates/"

list_attribut = {
  cluster: "CLUSTER_INTDEV_QA_UAT_PREPROD",
  vlan:    "UAT_VLAN30",
  storage: "SAN_LUN3",
  servers: [
     {
       name: "chef-server-marc",
       spec: "spec_linux",
       vm_dir:  "Chef",
       template: "#{template_basedir}vtemplate-Centos7"
     },
     {
       name: "chef-node1-marc",
       spec: "spec_linux",
       vm_dir:  "Chef",
       template: "#{template_basedir}vtemplate-Centos7"
     }
  ]
}

       
       

Vagrant.configure("2") do |config|  
  config.vm.box = "vsphere-dummy"

  list_attribut[:servers].each do |server|
    config.vm.define server[:name] do |env|
      env.vm.hostname = server[:name]
      env.vm.provider :vsphere do |vsphere|
        vsphere.host = vsphere_host
        vsphere.user = vsphere_user
        vsphere.password = vsphere_password
        vsphere.insecure = true

        vsphere.vm_base_path = server[:vm_dir]

        vsphere.name = server[:name]
        vsphere.compute_resource_name = list_attribut[:cluster]
        vsphere.template_name = server[:template]
        vsphere.customization_spec_name = server[:spec]
        vsphere.vlan = list_attribut[:vlan]
        vsphere.data_store_name = list_attribut[:storage]
      end
    end
  end
end
