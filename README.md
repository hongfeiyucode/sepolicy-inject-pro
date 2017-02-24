# Sepolicy Inject Pro

## Install

	sudo apt install libsepol1 libsepol1-dev gcc sepol-utils
	git clone 
	cd sepolicy-inject
	make

## Introduce

Injecting a rule:

	./sepolicy-inject -s shell -t system -c file -p read -P sepolicy

Injecting multiple permissions:

	./sepolicy-inject -s shell -t system -c file -p read,write,open -P sepolicy

Add a type_attribute to a domain:

	./sepolicy-inject -s su -a mlstrustedsubject -P sepolicy

Injecting a permissive domain:

	./sepolicy-inject -Z shell -P sepolicy

Change a permissive domain to non-permissive:

	./sepolicy-inject -z shell -P sepolicy 

Test a SELinux type exists:

	./sepolicy-inject -e -s shell -P sepolicy 

Test a SELinux class exists:

	./sepolicy-inject -e -c service_manager -P sepolicy 

Add a transition:

	./sepolicy-inject -s su_daemon -f device -c file -t su_device -P sepolicy

Add a filename transition:

	./sepolicy-inject -s su_daemon -f device -c file -g "socket" -t su_device -P sepolicy

All options can add -o <output file> to output to another file

## Add auto allow patch support
The patch will work like this:

./sepolicy-inject --auto -P sepolicy
This will allow all possible transition (just like selinux disabled)

./sepolicy-inject --auto -s su -P sepolicy
This will allow all transitions from su to any type

./sepolicy-inject --auto -t su -P sepolicy
This will allow all transitions from any type to su

./sepolicy-inject --auto -c file -P sepolicy
This will allow any transitions involving the class file

./sepolicy-inject --auto -s su -t system_data_file -P sepolicy
This will allow all transitions from su to system_data_file

## TODO

- [ ] permissive $domain;
- [ ] unconfined_domain($domain)  
- [ ] 删除功能
- [ ] 删除多余，重复，矛盾的语句。确保文件小于之前