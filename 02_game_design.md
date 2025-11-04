# Game Design

## Základní tabulka statů zaměstnanců 

<img width="591" height="153" alt="image" src="https://github.com/user-attachments/assets/f7880706-9140-41ac-9fc1-677fc74d4348" />

- HP / Speed - Zdraví / rychlost pohybu a útoku
- SP / Work speed - Mentální výdrž / rychlost vykonání práce
- FEAR / WS - Strach zaměstnance (míra strachu ovlivňuje násobitel SP poškození) / Úspěšnost práce (bonusová šance na úspěch práce)
- FAITH - Víra zaměstnance - šance na vzdor mentálního zhroucení (když se SP dostane na 0, při úspěchu se vrátí na 20 % SP) / Šance na permanentní negativní atribut 




### XP tabulky

<img width="340" height="68" alt="image" src="https://github.com/user-attachments/assets/cb00ff47-4fd0-4f75-a915-8b0624bcaa47" />

<img width="420" height="68" alt="image" src="https://github.com/user-attachments/assets/a9545469-46d3-4eed-b227-6c908cb179bb" />

- Postavy získávají XP zkoumáním monster
- Nebezpečnější monstra poskytují více XP
- Postava má 4 vlastnosti 
- Každá vlastnost má vlastní úroveň a získává do nich XP plněním specifickou prací (pokud postava vykoná práci typu "Fulfill" dostane XP do HP/Speed atributu) 

## Layout mapy

<img width="1867" height="829" alt="image" src="https://github.com/user-attachments/assets/797727cc-844c-4dcb-9601-e3bd97612b6e" />

- Žlutá barva označuje hlavní místnosti
- Černá (nevyplněná) místnost je chodba která slouží k pohybu mezi místnostmi
- Červená barva označuje místnost s monstry
- Zelená barva označuje výtah mezi místnostmi a chodbami
- Oranžová čára označuje časový průchod (postava musí počkat určenou dobu než může projít)
- Šipka označuje jednostraný průchod (postava může projít jen jedním směrem)


## Save and Load
Hračovo postup se uloží na konci výpravy a proto na dalšim loadu do sceny musíme zaměstnance spawnout uplně znova
takže si nemyslete to že se klonují jako chyba protože na konci dne se stejně po save všichni zabiji/zničí tím padem ke klonování ve finalní verzi nedojde.


Menší ukázka jak funguje náš save/load system: 





https://github.com/user-attachments/assets/857337b5-3639-408c-aabd-5a13aed53cd6



v ukázce změním max health a sp našeho zaměstnance to se uloží (bohužel jsem zapomněl to ukazat) a spawneho na stejné lokaci jako kde skončil (to trošku upravíme ať se spawne v odílu kam patří ale na to potřebujeme nejdříve mapu takže prozatím to je nastavené na jeho poslední lokaci) a jak už jsem vysvětlil ke klonování má dojít to je učelem.


