- [vlan](#vlan)
- [Co to je VLAN?](#co-to-je-vlan)
- [Na co VLANy?](#na-co-vlany)
    - [lan vs vlan rozdíl v gifu](#lan-vs-vlan-rozd%c3%adl-v-gifu)
    - [Host A pošle data přes broadcast bez vlany](#host-a-po%c5%a1le-data-p%c5%99es-broadcast-bez-vlany)
    - [Host A pošle data přes broadcast s VLANou](#host-a-po%c5%a1le-data-p%c5%99es-broadcast-s-vlanou)
- [Výhody VLAN](#v%c3%bdhody-vlan)
- [Co je to trunk(IEEE 802.1q tagging)](#co-je-to-trunkieee-8021q-tagging)
- [Shrnutí trunku](#shrnut%c3%ad-trunku)
- [IEEE802.1Q tagování](#ieee8021q-tagov%c3%a1n%c3%ad)
  - [když se rámec dostane do switche, proběhne tkzv. taggovaní](#kdy%c5%be-se-r%c3%a1mec-dostane-do-switche-prob%c4%9bhne-tkzv-taggovan%c3%ad)
- [VLAN Trunking Protocol (VTP)](#vlan-trunking-protocol-vtp)

# vlan
# Co to je VLAN?
• Virtuální LAN slouží k logickému rozdělení sítě nezávisle na fyzickém uspořádání

• pomocí VLAN můžeme síť segmentovat na menší sítě uvnitř fyzické struktury původní sítě

• obvykle bývá realizována na zařízení switch (přepínač)

• důležitou součástí je trunk – port, který je zařazen do více VLAN

• pomocí VLAN můžeme dosáhnout stejného efektu, jako když máme skupinu zařízení připojených do switche a druhou skupinu do jiného switche 
# Na co VLANy?
### lan vs vlan rozdíl v gifu
![rozdil](rozdil.gif)
### Host A pošle data přes broadcast bez vlany
![broadcast](broadcast.gif)
### Host A pošle data přes broadcast s VLANou
![vlan](vlan.gif)
Jak vidíme tak se data dostanou jen do VLAN skupiny 1 a do druhý skupiny ( kde je HOST D) se nedostanou..
Stručněji řečeno, ty síťová zařízení se rozdělí do skupin a data se dostanou jen do pc v dané skupině...
![rozdeleni](rozdeleni.gif)
Co se stane když host A z VLAN10 se pokusí poslat data do VLAN20?
![nejde](nejde.gif)
Dále se pozmění trochu ip adresa
![zmena_ip](zmena_ip.gif)
Dále se na switchi nastaví porty pro vlany aby se komunikovalo jen v ty daný skupině(vlaně)...
VLAN se vytváří na switchi pomocí přiřazení portů na switchi ke konkrétní síti VLAN.
![porty_switche](porty_switche.png)
![porty](porty.png)
# Výhody VLAN
• Oddělení speciálního provozu.
> ..

• zjednodušená správa 
>k přesunu zařízení do jiné sítě stačí překonfigurovat zařazení do VLANy => správce konfiguruje SW a ne HW (fyzické přepojení)

• snížení HW 
> různé podsítě mohou být na stejném switchi 

![sjednoceni](sjednoceni.gif)

• snížení broadcastů 
>hlavní výhodou VLAN je vytvoření více, ale menších, broadcastových domén => zlepšení výkonu sítě snížením provozu (traffic)

![mensi_provoz](mensi_provoz.gif)

• zvýšení zabezpečení 
> oddělení komunikace do speciální VLANy, kam není jiný přístup 
(Dáme portu určitý číslo a žádný jiný port přes něj neprojde)

![priklad1](priklad1.png)
# Co je to trunk(IEEE 802.1q tagging)
• označován také jako trunking protocol nebo dot1q tagging

• standardizovaná metoda, kterou podporují všechny moderní switche s podporou VLAN

Jak uděláme, aby B na switchi 1 komunikoval s D na switchi 2? (viz. obrazek)
![trunk1](trunk1.png)
Toto se vyřeší pomocí tzv. trunku

Tento proces spojování ruzných komunikací VLAN pomoci trunků se nazývá trunkování.

Trunkování funguje díky Trunk portu 

![trunkport](trunkport.png)

Trunk port přidá VLAN tag do ethernetovýho rámce aby identifikoval do jaké VLAN síťe ten rámec patří...

Access port(přistupový port) = přenáší provoz pouze pro jednu VLAN 
![accesport](accesport.png)

# Shrnutí trunku
Jestliže chceme, aby různé VLANové komunikace cestovali skrz 2 switche, potřebujeme trunk.

Trunk je vytvořen konfigurací trunk portů.

Trunk port vyšle (nebo očekává že dostane) tagovanou komunikaci.

Access port pošle (nebo očekává že dostane) netagovanou komunikaci.

![full](full.png)
# IEEE802.1Q tagování
## když se rámec dostane do switche, proběhne tkzv. taggovaní 

Princip taggovaní:
>Hlavička originálního rámce je rozšířena o 4B informaci, první značka je protokol 802.1q, dále následuje priorita dle protokolu, příznak a poslední je číslo VLAN

> protože se změní data, je třeba přepočítat kontrolní součet na konci rámce 

Teď mými slovy:

Když pc A pošle do switche ethernetový rámec, rámec má zdrojovou a cílovou adresu atd., ale neobsahuje žádné informace o VLANě.

Důvodem je to, že počítač nemá tušení že nějaká VLANa existuje a ani nemusí.

Tvorba a řízení VLANy je všechno úkol switche.

Když switch 1 dostane ethernetový rámec od pc A, ví že přišel od pc A, který patří do VLAN 10.

![vlanEX1](vlanEx1.png)

Proto musí poslat tento rámec dalšímu členovy skupiny VLAN 10, který se nachází na switchi 2... takže musí poslat přes trunk xD

![vlanEX2](vlanEx2.png)

Před tím než pošle přes ten trunk, musí udělat jednu duležitou věc!!!!

To jest vložení VLAN tagu do rámce.

![vlozeni](vlozeni.gif)

Tento záhadná tag se dělí na 4 části

•první značka je protokol 802.1q

•dále následuje priorita dle protokolu

•příznak 

•a poslední je číslo VLAN (identifikátor)

![4casti](4casti.png)

OK, teď když se vložila nová část to Ethernetovýho rámce, tak už to není Ethernetový, ale je to IEEE 802.1q rámec

Nyní se pošle přes trunk, jupí!! Jak to ale vypadá uvnitř trunku?

Můžeme si představit trunk jako silnici, každý pruh silnice patří jiný VLAN komunikaci.

![silnice](silnice.png)

Teď dorazil tagovanej rámec do switche 2 !!

Switch 2 ví z toho tagu, že ho má poslat po VLAN10 počítači C.

ALE POZOR!!!!!

U shrnutí trunku jsem řekl že: "Access port pošle (nebo očekává že dostane) netagovanou komunikaci."

To znamená že switch 2 zahotí ten VLAN tag a pošle originální Ethernetový rámec počítači C.....

KONEC TAGOVÁNÍ !! :)
# VLAN Trunking Protocol (VTP) 





 

