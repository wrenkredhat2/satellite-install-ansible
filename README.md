# Ansilbe suite to setup a VMProvisioner 

## Execute

## Setup VM:
ANSIBLE_HOST_KEY_CHECKING=False; ansible-playbook setup_satellite_server.yaml -i ./inventory.ini  --vault-password-file .vault_pass


## Setup SatelliteServer in VM:
ANSIBLE_HOST_KEY_CHECKING=False  ansible-playbook create_satellite_server_in_vm.yaml -i ./inventory.ini --vault-password-file .vault_pass


## Configure Contentviews, repos, etc:
ANSIBLE_HOST_KEY_CHECKING=False  ansible-playbook add_kvm_vm_provisionier.yaml -i ./inventory.ini --vault-password-file .vault_pass

ANSIBLE_HOST_KEY_CHECKING=False  ansible-playbook provision_kvm_host.yaml -i ./inventory.ini --vault-password-file .vault_pass

# get IP of VM on host
virsh domifaddr satellite-server


# Create Tunnel on Notebook:
ssh -D 9900 -i ~/.ssh/hetzner_key root@satellite.wrhammers-xxx.de
--> Firefox setting proxy SOCKS-Proxy 127.0.0.1 port 9900
URL http[s]://<Ip-of-vm>virsh