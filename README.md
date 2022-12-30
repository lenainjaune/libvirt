RO en attente de la fin de migration















































# libvirt
Mémo des commandes libvirt et virt-manager

# Trouver la ou les IPs d'un domaine depuis l'hôte
```sh
# Peupler arp
user@host~$ nmap -sP 192.168.0.0/24

# lister les domaines
user@host~$ virsh list
 ID    Nom                            État
----------------------------------------------------
 3     buster                en cours d\'exécution

user@host~$ d=buster
user@host~$ for m in $(\
  virsh -q domiflist "$d" | grep -Eo "([0-f]{2}:?){6}" \
 ) ; \
 do \
  arp -n | grep $m |\
   grep -Eo "([0-9]{1,3}\.?){4}" ; done
192.168.0.10
```
