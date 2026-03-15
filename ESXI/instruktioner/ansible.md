# Claude AI förklarar Ansible

Installation på Ubuntu

    sudo apt update
    sudo apt install -y ansible

Verifiera installationen:

    ansible --version


Grundläggande koncept

- **Inventory** – En fil som listar vilka servrar Ansible ska hantera. Kan vara lokala maskinen eller fjärrservrar.
- **Playbook** – En YAML-fil som beskriver vad Ansible ska göra (tasks).
- **Module** – Inbyggda funktioner som Ansible använder för att utföra uppgifter (t.ex. installera paket, kopiera filer, starta tjänster).


Steg 1 – Testa mot localhost

Du behöver inte flera servrar för att lära dig. Kör mot din egna maskin:

    ansible localhost -m ping

Steg 2 – Skapa en enkel inventory-fil
    
    hosts.ini
    [webservers]
    localhost ansible_connection=local

    [dbservers]
    # lägg till fler servrar här senare

Steg 3 – Din första playbook
    
    site.yml
    - name: Min första playbook
    hosts: webservers
    become: true   # kör som sudo

    tasks:
        - name: Se till att curl är installerat
        apt:
            name: curl
            state: present

        - name: Skapa en katalog
        file:
            path: /opt/myapp
            state: directory
            mode: '0755'

        - name: Skriv en textfil
        copy:
            content: "Hej från Ansible!\n"
            dest: /opt/myapp/hello.txt

Kör den:

    ansible-playbook -i hosts.ini site.yml

Steg 4 – Användbara kommandon

Kommando | Vad det gör 
-|-
ansible all -i hosts.ini -m ping | Pinga alla hostar
ansible-playbook site.yml --check | Testkör utan ändringar (dry run)
ansible-playbook site.yml --diff | Visa exakt vad som ändras
ansible-playbook site.yml -v | Verbose output 
ansible-doc apt | Dokumentation för en modul


# Claude förklarar hur jag ska få igång en VM med Ansible

Förutsättningar
På din Ubuntu-VM:

- Ansible installerat
- Python-biblioteket pyVmomi (VMware SDK för Python)
- Eventuellt community.vmware-kollektionen

bash

    pip install pyVmomi
    ansible-galaxy collection install community.vmware

På ESXi-hosten:

- ESXi 8 har API:et aktiverat som standard
- Du behöver ett konto med tillräckliga rättigheter (root eller ett dedikerat servicekonto)


Exempel – Skapa en ny VM
    
    (yaml)

    name: Skapa ny VM på ESXi
    hosts: localhost
    gather_facts: false

    vars:
        esxi_host: "192.168.1.10"
        esxi_user: "root"
        esxi_pass: "dittlösenord"

    tasks:
        - name: Skapa VM
        community.vmware.vmware_guest:
            hostname: "{{ esxi_host }}"
            username: "{{ esxi_user }}"
            password: "{{ esxi_pass }}"
            validate_certs: false        # Sätt till true i produktion
            datacenter: "ha-datacenter"  # Standardnamn på fristående ESXi
            name: "min-nya-vm"
            state: present
            guest_id: ubuntu64Guest
            disk:
            - size_gb: 40
                type: thin
                datastore: "datastore1"
            hardware:
            memory_mb: 2048
            num_cpus: 2
            networks:
            - name: "VM Network"
                device_type: vmxnet3
            cdrom:
            - controller_number: 0
                unit_number: 0
                state: present
                type: iso
                iso_path: "[datastore1] isos/ubuntu-24.04.iso"

Viktiga saker att tänka på

Punkt | Detalj 
-|-
Direkt ESXi vs vCenter | Utan vCenter fungerar de flesta moduler, men några kräver vCenter
validate_certs: false | Nödvändigt om ESXi har självsignerat cert
Datacenter-namn | På fristående ESXi heter det alltid ha-datacenter
ISO-montering | ISO:n måste redan finnas uppladdad på ett datastore

Fler användbara moduler

- vmware_guest_powerstate – starta/stänga av VM
- vmware_guest_snapshot – hantera snapshots
- vmware_datastore_info – lista datastores
- vmware_vm_info – hämta info om befintliga VM:ar