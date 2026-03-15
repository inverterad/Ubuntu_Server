# ESXi - VMware vSphere Hypervisor 8.0U3e

Vi börjar från början. Jag går just nu en kurs om Endpoint Security och min lärare Walter gav mig förslaget att installera ESXi på mitt hemmalabb för att öka på lite erfarenhet i det området. Och det är inte alls en dålig idé. Jag kör alla mina VM-labb idag på min ordinarie stationära. Att kunna flytta över ett gäng eller starta andra labb-konstellationer utan att störa min ordinarie dator känns som en bra idé.

Så jag laddade hem senaste tillgängliga versionen, VMware vSphere Hypervisor 8.0U3e, och fixade i ordning en bootable USB så att jag kan installera.

Sedan följde jag den här guiden mer eller mindre för att komma igång: https://www.starwindsoftware.com/blog/how-to-install-vmware-esxi-and-create-your-first-vm/

Jag pluggade ur min [Ubuntu servers](https://github.com/inverterad/Homelab/tree/main/FysiskUbuntuServer) SSD och stoppade in en 1tb HDD för att testa det här. Så allt är beläget i min server. Kan bli så att jag pensionerar min Ubuntu för att ha den som en VM framöver, vi får se.

Purfärsk. Ska konfigurera lite och börja installera en VM snart.

![Fresh install](images/esxi_fresh.png)

## Ubuntu Server

Vi börjar med en Ubuntu Server-VM. Det är något jag gjort förr trots allt.

Jag installerar openssh istället för att använda ESXi:s egna konsoll, även om den verkar rätt ok så är det skönt att kunna copy-paste:a osv.

Jag ska försöka få igång Ansible och lära mig lite om det. Efter jag har lite koll så tänkte jag försöka få igång en ny VM med hjälp av Ansible, jag kommer använda Claude AI för att försöka få ordning på detta.

Vi börjar med att bara installera Ansible och försöker automatisera något, i värsta fall får jag fixa upp en till VM manuellt för konfiguration genom Ansible.

Jag följer [Claudes instruktioner](instruktioner/ansible.md).

Efter att jag förstått lite av Ansible genom att testa uppdatera lite på localhost så ska jag installera en till VM på ESXi:n som jag ska prova konfigurera med Ansible.




