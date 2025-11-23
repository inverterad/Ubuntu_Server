# 2025-11-23
Installerar neofetch för att lättare kunna se min hårdvara. <br>
Jag räknar med att drivrutinerna för grafikkortet inte är optimala med tanke på installationen och att jag var tvungen att köra "nomodeset", så nu försöker jag uppdatera drivrutiner med: <br>
<code>sudo ubuntu-drivers autoinstall</code>
<br>
<code>sudo nvidia-smi</code> visar mig att nuvarande drivrutin är <code>Driver Version: 535.274.02</code> <br>
Det kanske är en nog ny drivrutin men det verkar inte vara den senaste. Men nu kan vi se hur det ser ut i GUI:n. <br>
Jag får No Signal på skärmen nu, så något är tokigt. <br>
En reboot med skärmen igång verkar räcka, för nu fungerar skärmen. Så vi fortsätter. Återkommer hit om problemet dyker upp igen. <br>

## Installera Steam Link
Nu ska vi testa installera Steam Link och se om det fungerar eller inte. <br>
Jag börjar med att installera flatpak med: <br> 
<code>sudo apt install flatpak</code>. <br>
<code>sudo flatpak remote-add flathub https://flathub.org/repo/flathub.flatpakrepo</code>
<code>sudo flatpak install flathub com.valvesoftware.SteamLink</code>

Allt verkade fungera fint. Jag slog igång Steam Link på servern och kopplade ihop en xbox-kontroll samt kopplade ihop den med min stationära PC och allt var fint fram till jag startade ett spel, skärmen var bara svart. Kunde inte navigera Steam Big Picture Mode heller. Så nu blir det lite felsökning. <br>

https://help.steampowered.com/en/faqs/view/0689-74B8-92AC-10F2#blackscreen <br>

Första rekommendationen är att uppdatera drivrutiner, så vi går tillbaka dit och tar bort drivrutinerna vi har och installerar den drivrutinen som nvidia själva verkar föreslå. <br>

<code>sudo apt purge nvidia-driver-535</code> <br>
<code>sudo apt-get autoremove</code> <br>
<code>sudo reboot</code> <br>
<code>sudo apt install nvidia-driver-580</code> <br>
<code>sudo reboot</code> <br>
<code>nvidia-smi</code> <br>
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running. <br>
Suck. <br>

Det visade sig dock att driver 535 inte var problemet. Så jag har återställt det som det var och det som löste problemet var att "disable hardware encoding" på min stationära PC. Efter det så verkade allt flyta på fint. Provade spela ett ett par spel och det kändes smidigt. Måste installera Dark Souls eller något där det är noga med precision och testa. <br>

Valde att ställa in så att jag inte behöver skriva in login och lösen varje gång jag startar om servern. Men SSH behåller kravet på lösenord. Jag skapade en fil med lite kod i! <br>
<code>sudo nano /etc/lightdm/lightdm.conf.d/50-autologin.conf</code> <br>
Fyllde i följande: <br>
<code>[Seat:*] <br>
autologin-user=YOUR_USERNAME <br>
autologin-user-timeout=0 </code><br>

Och nu funkar det galant!


# 2025-11-22
Har laddat hem ubuntu-24.04.3-live-server-amd64.<br>
https://ubuntu.com/download/server <br><br>
Tar hem programvaran Rufus för USB-installation.<br>
https://rufus.ie/sv/#download<br>

![Rufus screenshot](<Screenshots/Skärmbild 2025-11-22 Rufus.png>)
<br><br>
Först installerar jag en gammal SSD då ingen var installerad sedan tidigare. Efter det så blev det lite stök med att få igång boot från USB men det löste sig till slut.<br>
Där efter blev det dock rätt stökigt, då jag försöker installera från USB så får jag No Signal från skärmen efter en stund, vilket gör mig rätt låst. Måste starta om flera gånger och remounta USB-stickan flera gånger. För att lösa problemet så behövde jag gå in i en meny efter jag får alternativet att installera Ubuntu. Trycker på e för att komma in i en submeny där jag lägger till "nomodeset" för att den ska skippa att ladda video drivers och efter det fungerar det!
<br><br>
Efter detta kör jag: <br>
<code>sudo apt install xubuntu-desktop</code>

Nu bör jag ha tillgång till en GUI. Testar den och allt ser ut att fungera ok, nu ska jag se till att jag kan fjärrkoppla mig till desktop med hjälp av xrdp på ubuntu-servern. Så jag kör: <br>
<code>sudo apt install xrdp</code>




# 2025-11-15 - Hämta hårdvaran och påbörja

Hämtade hem hårdvaran, ett gammalt chassi som jag använt för hundra år sedan. Innanmätet är jag osäker på vad det är för något idag, ska bli intressant att kolla in när jag får igång den gamla härken.

Dammig och jävlig, men charmig!<br>
![Chassi](Screenshots/chassi.jpg)
