# vagrant tricks
some tricks to use with vagrant
#usage
```
git clone https://github.com/is-daimonos/vagrant_tricks
```

to create multiple virtual machines, customized, in a single iteration cycle use the create_vms
```
cd create_vms
```
add or edit the scripts for each virtual machines, for example in this scripts
```
$ansible_packages= <<SCRIPT
yum install -y epel-release && yum update -y \
&& yum -y install ansible
SCRIPT
```
you can define a variable and add what you consider necessary

```
$some_var = <<SCRIPT
yum install -y nmap
SCRIPT
```
now you will have to add this variable in the corresponding block
```
vms = {
  "ansible" => { :ip => "192.168.10.10", :cpus => 1, :mem => 1024, :packages => $ansible_packages },
  "pxeboot" => { :ip => "192.168.10.11", :cpus => 1, :mem => 1024, :packages => $pxeboot }
  "test" => { :ip => "192.168.10.12", :cpus => 1, :mem => 1024, :packages => $some_var }
}
```

now run 
```
vagrant up
and the magic will come to you...
```
