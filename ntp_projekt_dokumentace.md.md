# Projekt: Nastavení NTP démona v Linuxu

### Obchodní akademie, Vyšší odborná škola a Jazyková škola s právem státní jazykové zkoušky Uherské Hradiště  
 
### Řešitelé: Martin Rygulski, Ondřej Malůš, Marek Zalubil

### Datum zpracování: 30. května 2025


## Úvod
Synchronizace času v počítačových systémech představuje klíčový prvek pro zabezpečený a spolehlivý provoz mnoha aplikací a služeb. Operační systémy, servery, databáze i bezpečnostní protokoly často vyžadují přesný a synchronizovaný systémový čas. I drobná odchylka může způsobit problémy například při autentizaci uživatelů (Kerberos), analýze logů či řízení časově citlivých operací. Projekt se zaměřuje na implementaci řešení tohoto problému pomocí NTP (Network Time Protocol) démona v prostředí Linuxu.

Projekt spočívá v instalaci, konfiguraci a testování služby `ntpd` (NTP daemon), která zajišťuje průběžnou synchronizaci času se vzdálenými časovými servery. Součástí bude i úvaha nad možností provozovat NTP server lokálně pro další zařízení v síti. 

Realizace bude dokumentována krok za krokem včetně použitých příkazů a testovacích nástrojů (`ntpq`, `timedatectl`, `systemctl`). Výsledkem bude funkční konfigurace, kterou lze opakovaně použít nebo rozšířit. Projekt přispěje k pochopení praktických principů správy času v systémech a je vhodný pro každého, kdo spravuje servery nebo více zařízení v síti.

## Co je cílem projektu?
- Nainstalovat a nakonfigurovat NTP démon (`ntpd`) v prostředí Linuxu.
- Synchronizovat systémový čas s údaji z řady veřejných serverů.
- Otestovat synchronizaci a ověřit funkčnost služby.


## K čemu je to dobré v praxi?
- Zajištění přesného času v logovacích a monitorovacích systémech.
- Správné fungování autentizačních protokolů (např. Kerberos).
- Synchronizace databázových operací a systémových úkolů (cron).
- Soulad s bezpečnostními normami a certifikacemi.

## Jaké materiály plánujete použít?
- Operační systém Linux (např. Ubuntu 22.04, Debian, CentOS)
- Balíček `ntp`, editor `nano`
- Konfigurační soubor `/etc/ntp.conf`
- Údaje servery `*.cz.pool.ntp.org`
- Nástroje `ntpq`, `systemctl`, `timedatectl`, `journalctl`

## Ověřitelné cíle
- `systemctl status ntp` ukazuje aktivní službu.
- `ntpq -p` zobrazí servery a hodnoty offset/delay.
- `timedatectl` vrací `System clock synchronized: yes`.
- Služba se spouští automaticky po startu.

## Postup řešení
1. Instalace balíčku NTP pomocí správce balíčků (`apt` / `dnf`).
2. Úprava konfiguračního souboru `/etc/ntp.conf`.
3. Zajištění spouštění služby pomocí `systemctl enable/start ntp`.
4. Testování pomocí nástrojů `ntpq -p`, `timedatectl`, `journalctl`.

## Dokumentace testování / ověření cílů
- Po instalaci a spuštění služby proběhl test příkazem `ntpq -p`, který potvrdil navázání komunikace se servery z `cz.pool.ntp.org`.
- `timedatectl` potvrdil synchronizaci.
- `systemctl is-enabled ntp` vracel `enabled`, což ověřuje automatické spouštění.


## Rozdělení práce
- Malůš : Testování ntp daemon
- Zalubil : Vytvoření dokumentace
- Rygulski : Instalace ntp daemon

## Závěr
Projekt se podařilo úspěšně realizovat. Většina cílů byla splněna dle plánu, synchronizace fungovala spolehlivě a byla ověřena. 

Nepovedla se implementace lokálního serveru v síti kvůli chybějícím oprávněním v testovací infrastruktuře. 

Zaskočil nás pomalejší čas, který `ntpd` potřebuje k navázání plné synchronizace po startu. Jinou variantou by bylo použití `chronyd`, který je modernější a rychlejší, avšak v projektu jsme zůstali u klasického `ntpd` z důvodu zadání.

Pro další testování by bylo vhodné otestovat i synchronizaci mezi systémy v izolovaném LAN prostředí.

## Použité zdroje

2. "Debian NTP Documentation" – 
      https://wiki.debian.org/NTP
4. Konverzace s AI ChatGPT, OpenAI, 2025.
5. Oficiální web NTP: [https://www.ntp.org/](https://www.ntp.org/)

Citace v souladu s normou ČSN ISO 690.
