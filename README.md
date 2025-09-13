# mps-cis-debian13

## Motivation

An official ansible-lockdown version for Debian13 is not yet available
and DEBIAN12-CIS does not run on Debian13 without modifications.
This repository bridges the gap to make Debian13 CIS compliant
until an official ansible-lockdown release is available.

## Getting Started

- Clone this repo
- Clone <https://github.com/ansible-lockdown/DEBIAN12-CIS>
- Copy repo contents to DEBIAN12-CIS folder
- Create a inventory file
- Use defaults/main.yml to adjust to your system if needed (Optional)
- Install ansible
- Run the site.yml playbook with Ansible
- Enjoy!

## Example

```

# Params
SSH_PORT=22
SSH_USER=deployuser
HOSTNAME=testhost
TARGET_DIR=~/ansible-lockdown

# Change PWD
mkdir -p $TARGET_DIR
cd $TARGET_DIR || exit 1

# Clone this repository
rm -rf mps-cis-debian13
git clone https://github.com/mpsffap/mps-cis-debian13

# Clone ansible-lockdown for Debian12
rm -rf DEBIAN12-CIS
git clone https://github.com/ansible-lockdown/DEBIAN12-CIS

# Copy Diff
cp -r mps-cis-debian13/* DEBIAN12-CIS

# Inventory
mkdir DEBIAN12-CIS/inventory
printf "[all]\n$HOSTNAME ansible_port=$SSH_PORT ansible_user=$SSH_USER\n" \
  > DEBIAN12-CIS/inventory/hosts

# Run
cd DEBIAN12-CIS
sudo apt install ansible
ansible-playbook -i inventory/hosts site.yml

```

