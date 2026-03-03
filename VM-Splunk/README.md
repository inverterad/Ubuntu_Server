# VM-labb med fokus på Splunk

Jag håller på sätta upp en labbmiljö i Virtualbox för att installera, konfigurera och testa Splunk och samtidigt kunna se mina egna attacker mot mer eller mindre sårbara enheter.

Jag har utgått från [det här repot](https://github.com/avulman/active-directory-project). Men har varit tvungen att modifiera mycket då det fanns en hel del fel i instruktionerna och de var inte alltid speciellt tydliga, så mycket fick man lära sig under tiden.

Såhär ser det ut i dagsläget, de markerade maskinerna är installerade och nästan färdigkonfigurerade. Åtminstone Universal Forwarders är på plats. Jag har lite problem med att indexera både Windows 10 och Windows Server 2022 till 'endpoints'. Men det ska nog gå att lösa snart. WinServ2022 vill fungera och skicka till endpoint, men inte Windows 10. Nedan finns en skärmdump som visar det.

Uppdatering 10 minuter senare, ibland är det smart att lägga upp misstag på Github. Då ser man att man döpt filen till input istället för inputs. Det var antagligen problemet. Men nu är allt ominstallerat och fungerar!

Sedan ska jag konfigurera lite Active Directory-grejer på servern. Förhoppningsvis snart.

![Virtualbox](<Screenshots/Skärmbild 2026-03-03 185905.png>)

![Win10 vill inte](<Screenshots/Skärmbild 2026-03-03 191817.png>)

Och så lyckades jag fixa det!

![Win10 vill!](<Screenshots/Skärmbild 2026-03-03 195844.png>)