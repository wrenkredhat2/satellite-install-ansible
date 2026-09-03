#

## Prep

Download
https://github.com/RedHatSatellite/satellite-ansible-collection/releases/
sudo ansible-galaxy collection install ~/Downloads/redhat-satellite-5.11.0.tar.gz

ansible-galaxy collection install redhat.satellite
ansible-galaxy collection install theforeman.foreman


ansible-vault create vault.yml
mit:
satellite_url: "https://satellite.example.com"
satellite_username: "admin"
satellite_password: "YourSecurePassword"
satellite_validate_certs: false

> Nano-Exitor


Login-Basic Install
grep -v satellite ~/.ssh/known_hosts >~/.ssh/x_known_hosts && mv ~/.ssh/x_known_hosts ~/.ssh/known_hosts
ssh -i ~/.ssh/hetzner_key root@satellite.wrhammers-xxx.de

installimage -a -n rhel-server -r yes -l 1 -i /root/.oldroot/nfs/images/$(ls /root/.oldroot/nfs/images | grep -i "Alma-9" | head -n 1)

reboot

grep -v satellite ~/.ssh/known_hosts >~/.ssh/x_known_hosts && mv ~/.ssh/x_known_hosts ~/.ssh/known_hosts

ssh -i ~/.ssh/hetzner_key root@satellite.wrhammers-xxx.de

# Import the Red Hat release GPG key
sudo curl -o /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release https://security.access.redhat.com/data/fd431d51.txt

# Add the Convert2RHEL repo (change -9- to -8- if running version 8.x)
sudo curl -o /etc/yum.repos.d/convert2rhel.repo https://cdn-public.redhat.com/content/public/repofiles/convert2rhel-for-rhel-9-x86_64.repo

# Install the tool
sudo dnf install -y convert2rhel

3cac4699-f0d1-4aef-8fdd-9aeca35d4f4a

sudo convert2rhel --org 6340056 --activationkey 3cac4699-f0d1-4aef-8fdd-9aeca35d4f4a




cat ~/Downloads/rhel-10.2-x86_64-dvd.iso | ssh -i ~/.ssh/hetzner_key root@satellite.wrhammers-xxx.de "cat > /root/rhel_10.2.iso"

ssh -L 5900:localhost:5900  root@satellite.wrhammers-xxx.de

qemu-system-x86_64 -enable-kvm -cpu host -m 8192 -smp 4 \
  -drive file=/dev/sda,format=raw,media=disk \
  -drive file=/dev/sdb,format=raw,media=disk \
  -cdrom /root/rhel_10.2.iso -boot d -vnc :0



subscription-manager register --org="6340056" --activationkey="3cac4699-f0d1-4aef-8fdd-9aeca35d4f4a"
subscription-manager repos --enable rhel-10-for-x86_64-appstream-rpms
dnf install -y ansible-core

virt-host-validate


