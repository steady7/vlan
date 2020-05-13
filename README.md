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
![porty_switche](porty_switche.png)
# Výhody VLAN
Oddělení speciálního provozu.

zvýšení zabezpečení – oddělení komunikace do speciální VLANy, kam není jiný přístup 
(Dáme portu určitý číslo a žádný jiný port přes něj neprojde)

![priklad1](priklad1.png)

 

