[Co dodělat ]: #
[pojmy ]: #

# Výběr řídící jednotky pro různé aplikace

$${\color{#FFA500}E9 \space \color{#4682B4}A1 }$$

## Cíle

- **Kategorizovat a porovnat** architektury řídicích systémů (MCU, MPU, embedded systémy, PLC, iPC, programovatelná relé) podle výkonu, paměti, determinismu a spolehlivosti.
- **Analyzovat provozní prostředí a vnější vlivy** (krytí IP, teplotní rozsah, EMC rušení, vibrace) a stanovit požadavky na mechanickou a elektrickou odolnost hardware.
- **Sestavit I/O bilanci** a navrhnout optimální řídicí jednotku z reálných katalogů výrobců pro konkrétní průmyslovou či IoT aplikaci včetně projektové rezervy.
- **Vypracovat vícekriteriální rozhodovací matici** a obhájit zvolenou platformu z technického a ekonomického hlediska (pořizovací cena, náročnost vývoje, údržba a spolehlivost).
- **Provést kritický technický audit (troubleshooting)** nevhodného návrhu řízení, identifikovat bezpečnostní a provozní rizika a navrhnout certifikované řešení v souladu s průmyslovými standardy.

## Ověření cílů

Výběr řídící jednotky pro různé aplikace

1. Příklady řídících jednotek
2. Jejich základní vlastnosti z hlediska výpočetního výkonu a velikosti paměťového prostoru
3. A z hlediska odolnosti
4. Příklady použití v praxi (kde se používají MCU, a kde ř. j. s MPU)


%% 1. Správné vysvětlení pojmů, architektur a zkratek z oblasti řídicích systémů. %%
%% 2. Schopnost posoudit vliv prostředí na výběr hardwaru a dešifrovat IP kód. %%
%% 3. Vypracování rozhodovací matice pro volbu vhodné platformy (MCU vs. PLC vs. iPC). %%
%% 4. Návrh konkrétní konfigurace řídicí jednotky na základě zadané I/O bilance a provozních podmínek. %%
%% 5. Kritická technická oponentura (audit) nevhodně navrženého řešení. %%

---

## Úlohy


### 1. Základní pojmy a architektury řídicích jednotek

*Časová dotace: 10–15 minut | Úvodní orientační úloha*

Doplňte do níže uvedené tabulky význam zkratek, základní princip a typický příklad reálného nasazení nebo zástupce:

| Zkratka / Pojem | Co zkratka znamená (česky / anglicky) | Základní charakteristika (architektura, kde běží program) | Typický zástupce (konkrétní rodina / model) | Příklad reálného nasazení |
| :--- | :--- | :--- | :--- | :--- |
| **MCU** | Microcontroller Unit / Mikrořadič | Integrovaný čip (CPU + RAM + Flash na jednom substrátu), deterministický běh bez OS nebo RTOS | ESP32, PIC16LF1xxx, RP2040, STM32F4 | Chytry elektroměr, řízení bezkartáčového motoru, nositelná elektronika |
| **MPU** | Microprocessor Unit / Mikroprocesor | Samostatný procesor vyžadující externí RAM a úložiště, zpravidla běží plnohodnotný OS (Linux) | NXP i.MX8, Broadcom BCM2711 (Raspberry Pi 4), TI Sitara | Průmyslové HMI panely, IoT brány (Gateway), kamerové systémy |
| **Embedded** | Embedded System / Vestavěný systém | Účelově zaměřený HW i SW systém vestavěný do většího zařízení, běží na bare-metal, RTOS i Linuxu | Embedded PLC (Beckhoff CX), Single Board Computer (SBC) | Bílá technika, bankomaty, regulace kotlů, lékařské přístroje |
| **PLC** | Programmable Logic Controller / Programovatelný logický automat | Průmyslový automat pro cyklické deterministické řízení procesů, vysoká odolnost, modulární/kompaktní | Siemens S7-1200/1500, Schneider Modicon, Allen-Bradley ControlLogix | Řízení balicí linky, automobilová montážní linka, ČOV |
| **iPC** | Industrial PC / Průmyslové PC | Průmyslově odolný počítač (x86/ARM) s vysokým výpočetním výkony pod OS Windows/Linux s reálným časem (SoftPLC) | Beckhoff C6030, Advantech UNO, Siemens Simatic IPC | Strojové vidění, řízení komplexních CNC strojů, SCADA / MES servery |
| **Programovatelné relé** | Programmable Relay / Smart Relay (Chytré relé) | Zjednodušené kompaktní PLC pro méně náročné úlohy, nahrazuje časovací relé a stykačové kombinace | Siemens LOGO!, Eaton easyE4, Schneider Zelio Logic | Automatická vjezdová závora, řízení osvětlení a rolet, čerpání jímky |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **SoC (System on Chip):** Integrovaný obvod sdružující všechny klíčové elektronické obvody a komponenty celého počítače či elektronického systému na jediném křemíkovém čipu. 
> 	 Systém na čipu. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-06-07 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Syst%C3%A9m_na_%C4%8Dipu
> - **DSP (Digital Signal Processor):** Specializovaný mikroprocesor architektury Harvard optimalizovaný pro matematické výpočty v reálném čase (rychlá Fourierova transformace FFT, filtrace šumu, digitální vektorové řízení střídavých motorů). 
> 	Digitální signálový procesor. In: _Wikipedia: otevřená encyklopedie_ [online]. St. Petersburg (Florida): Wikimedia Foundation, 2006, poslední editace 28. 2. 2026 [cit. 2026-09-14]. Dostupné z: [Digitální signálový procesor – Wikipedie](https://cs.wikipedia.org/wiki/Digit%C3%A1ln%C3%AD_sign%C3%A1lov%C3%BD_procesor)
> - **FPGA (Field-Programmable Gate Array):** Programovatelné logické hradlové pole, jehož vnitřní struktura logických bloků a propojení je konfigurovatelná až u zákazníka. Umožňuje masivní paralelní zpracování s hardwarovou latencí v řádu nanosekund. 
> 	Programovatelné hradlové pole. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-01-10 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Programovateln%C3%A9_hradlov%C3%A9_pole


<details>
<summary> :bulb: Tip k doplnění tabulky: </summary>
<p>Zaměřte se na čas náběhu a architekturu: U MCU je kód ve vnitřní paměti Flash procesoru a vykonává se okamžitě po přivedení napájení (řádově milisekundy). U systémů s MPU a iPC musí BIOS/bootloader nejprve zavést jádro operačního systému (OS Linux, Windows) z disku/eMMC/SD karty do operační paměti RAM, což trvá desítky sekund.</p>
</details>

:star2: **Bonusová otázka k úloze 1:**
Proč se u kritických aplikací v letectví (např. systém řízení letu Fly-by-Wire) nebo v jaderné energetice stále upřednostňují jednoduché deterministické mikrořadiče s několika desítkami kilobajtů paměti nebo obvody FPGA před moderními vícejádrovými gigahertzovými procesory s gigabajty RAM?

*Vaše odpověď:*
Jednoduché mikrořadiče a obvody FPGA nabízejí 100% předvídatelné (deterministické) chování bez latencí způsobených plánovačem OS, správou paměti nebo vyrovnávací pamětí (cache). Jejich kód je řádově jednodušší, což umožňuje provést kompletní formální verifikaci a certifikaci softwaru dle přísných bezpečnostních norem (např. DO-178C / DO-254 pro letectví). Neobsahují skryté chybové stavy (race conditions) a vykazují extrémní spolehlivost bez rizika zamrznutí operačního systému.

---

### 2. Parametry, paměti a provozní odolnost (IP krytí)

*Časová dotace: max. 15 minut | Mírně náročnější úloha propojující parametry a praxi*

1. **Typy pamětí v řídicích jednotkách:**
   - Doplňte porovnání pamětí z hlediska stálosti dat a rychlosti:
     - **RAM:** 
	     - Je volatilní (energeticky závislá)? `Ano`
	     - Rychlost zápisu: `Velmi vysoká (řádově nanosekundy)` 
	     - K čemu se využívá v PLC/MCU: `Ukládání dočasných provozních proměnných, běhový zásobník (stack), mezipaměť a procesní obraz vstupů/výstupů.`
     - **Flash (ROM):** 
	     - Je volatilní? `Ne`
	     - K čemu se využívá v PLC/MCU: `Trvalé uložení vykonávaného řídicího programu (firmware), konfiguračních tabulek a konstant.`
     - **EEPROM / NVRAM:** 
	     - Je volatilní? `Ne`
	     - K čemu se využívá v PLC/MCU: `Ukládání provozních parametrů, kalibračních dat, počítadel motohodin a remanentních proměnných.`
   - *Otázka z praxe:* Kam se v průmyslovém PLC ukládají aktuální provozní proměnné (např. čítače vyrobených kusů nebo motohodiny), aby se při nečekaném výpadku napájení neztratily (tzv. remanentní / retain data)?
     - Odpověď: `Ukládají se do remanentní paměti – NVRAM, MRAM, FRAM nebo do statické RAM (SRAM) zálohované baterií či superkondenzátorem (případně se při výpadku napětí přenesou pomocí kapacity zdroje do EEPROM/Flash).`

2. **Reálný čas a determinismus (Hard vs. Soft Real-Time):**
   - Proč pro reakci na nouzové zastavení lisu (požadavek reakce do 5 ms) použijeme PLC či mikrokontrolér s RTOS, a nikoliv běžné Raspberry Pi s operačním systémem Raspberry Pi OS (standardní Linux)?
     - Odpověď: `Běžný Raspberry Pi OS s obecným Linuxovým jádrem využívá preempivní plánovač, který optimalizuje průměrný datový průchod, nikoliv garantovaný reakční čas. Neplánované procesy na pozadí, obsluha přerušení nebo správa paměti mohou způsobit zpoždění (jitter) v řádu desítek až stovek milisekund. PLC/RTOS garantuje přesně definovanou maximální dobu odezvy (deterministický Hard Real-Time limit), což je pro bezpečnost lisu klíčové.`

3. **Odolnost vůči vlivům prostředí a dešifrování kódu IP:**
   - Dešifrujte kód **IP68**:
     - První číslice (6): `Úplná ochrana před dotykem jakýmkoliv pomůckou a úplná prachotěsnost.`
     - Druhá číslice (8): `Ochrana proti trvalému ponoření do vody za podmínek určených výrobcem zařízení.`
   - Jaké minimální krytí IP musí mít rozváděč umístěný ve venkovním nekrytém prostředí, kde na něj přímo dopadá déšť a fouká polétavý prach?
     - Označte správnou volbu: `[ ] IP20` | `[ ] IP44` | `[X] IP65` | `[ ] IP00`
     - Zdůvodnění: `Rozváděč musí být zcela prachotěsný (první číslice 6) a musím odolávat tryskající vodě ze všech směrů při dešti a větru (druhá číslice 5). Krytí IP44 chrání pouze proti stříkající vodě a tělesům > 1 mm, což pro polétavý prach a přívalový déšť nestačí.`

4. **Konstrukční rozdíly kancelářského PC vs. průmyslového iPC:**
   - Vyberte a doplňte hlavní odlišnosti:
     - *Chlazení:* 
	     - Kancelářské PC: `Aktivní větráky (nasávají prach a podléhají mechanickému opotřebení)` 
	     - vs. iPC: `Pasivní chlazení (bezventilátorové / fanless, využití celokovového šasi jako chladiče)`
     - *Napájecí napětí a filtrace:* 
	     - Kancelářské PC: `Standardní ATX zdroj 230 V AC bez speciální filtrace` 
	     - vs. iPC: `Širokorozsahové napájení 24 V DC (18–30 V) s galvanickým oddělením a EMC filtrací`
     - *Odolnost proti otřesům a vibracím:* `Kancelářské PC využívá plastové západky a není testováno na otřesy. iPC má celokovovou robustní konstrukci, komponenty odpružené nebo přímo pájené na PCB a místo HDD využívá výhradně SSD/eMMC Flash úložiště.`
     - *Způsob montáže:* 
	     - Kancelářské PC: na stůl/pod stůl 
	     - vs. iPC: `Montáž na DIN lištu do rozváděče, VESA držák nebo panelová montáž (Panel PC)`

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Determinismus (Real-Time):** Vlastnost systému, která zaručuje, že odezva na vstupní událost proběhne vždy v přesně definovaném a předvídatelném čase (deadline). V *Hard Real-Time* systémech znamená nedodržení časového limitu fatální havárii celého procesu. 
> 	Operační systém reálného času. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-05-12 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Opera%C4%8Dn%C3%AD_syst%C3%A9m_re%C3%A1ln%C3%A9ho_%C4%8Dasu
> - **Krytí IP (Ingress Protection):** Mezinárodní standard dle normy **ČSN EN 60529** určující stupeň ochrany krytem před vniknutím pevných cizích těles včetně prachu (1. číslice 0–6) a vniknutím vody (2. číslice 0–9K).
> 	ČESKÝ NORMALIZAČNÍ INSTITUT. *ČSN EN 60529 (33 0330) Stupně ochrany krytem (krytí - IP kód)*. Praha: Český normalizační institut, 1993. Třídící znak 330330.
> - **Remanentní paměť (Retain):** Paměťový prostor v PLC, jehož obsah zůstává zachován i po přerušení napájecího napětí (využívá zálohovací baterii, superkondenzátor nebo zápis do FRAM/MRAM/EEPROM).

<details>
<summary> :bulb: Tip k otázce determinismu: </summary>
<p>Běžný Linux je <b>preemptivní víceúlohový systém</b>, který se snaží spravedlivě rozdělit čas procesoru mezi stovky procesů. Může se stát, že kvůli obsluze disku, správě paměti nebo síťovému provozu se proces řízení pozdrží na desítky milisekund. PLC naproti tomu vykonává cyklus v pevném taktu bez zpoždění vyvolaného aplikacemi na pozadí.</p>
</details>

:star2: **Bonusová otázka k úloze 2:**
Co označuje doplňkové písmeno **K** v kódu krytí **IP69K** a v jakém průmyslovém odvětví je toto krytí bezpodmínečně vyžadováno?

*Vaše odpověď:*
Písmeno **K** označuje specifikaci dle normy DIN 40050-9 pro ochranu před **vysokotlakým a vysokoteplotním čištěním** (tlak vody 8–10 MPa / 80–100 barů, teplota +80 °C). Toto krytí je bezpodmínečně vyžadováno v **potravinářském průmyslu, farmaceutickém průmyslu a zemědělství**, kde probíhá pravidelná chemická a tlaková dezinfekce/mytí strojů (hygienické zóny).

---

### 3. Rozhodovací matice platforem (MCU vs. PLC vs. iPC) 

*Časová dotace: 20–25 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jste v pozici nezávislého konzultanta automatizace. Tři různí zákazníci požadují navrhnout optimální kategorii řízení.

#### Příklad aplikace (vzorové řešení):
- **Vzorová aplikace 0 – Automatická vjezdová závora na parkoviště:** Jednoduchý jednoúčelový systém s indukční detekční smyčkou vozidla, bezpečnostní optozávorou, koncovými spínači polohy ramene, motorem závory (vpřed/vzad) a výstražným semaforem (červená/zelená). Požadavek na jednoduchou správu správcem objektu a spolehlivý chod v rozváděči u vjezdu.

#### Popis zadaných aplikací pro studenty:
1. **Aplikace A – Chytrý pokojový termostat (IoT):** Bateriově napájený přístroj měřící teplotu a vlhkost v místnosti, zobrazující údaje na e-ink displeji a odesílající data přes protokol ZigBee/Wi-Fi do domácí brány. Plánovaná sériová výroba: 10 000 kusů ročně.
2. **Aplikace B – Automatická balicí linka:** Průmyslová linka ve výrobní hale. Obsahuje 28 optických snímačů, 14 pneumatických válců, 3 dopravníkové pásy s asynchronními motory a bezpečnostní světelnou závoru. Vyžaduje se nepřetržitý provoz 24/7 a snadná údržba podnikovým elektrikářem.
3. **Aplikace C – Kontrolní stanice optické jakosti svarů:** Pracoviště se 2 vysokorychlostními průmyslovými GigE kamerami snímajícími svary na karoserii automobilu. Snímky v rozlišení 4K jsou analyzovány neuronovou sítí v reálném čase, vady jsou označeny a ukládány do podnikové relační databáze (SQL / MES).

#### Váš úkol:
Vyplňte rozhodovací matici. Jako vzor poslouží vyplněný sloupec pro **Vzorovou aplikaci 0**. Přiřaďte každé aplikaci nejvhodnější platformu (**MCU / Embedded SoC**, **Kompaktní/modulární PLC**, **Průmyslové PC – iPC**) a doplňte multikriteriální posouzení:

| Kritérium hodnocení | **Vzorová aplikace 0 (Vjezdová závora - VZOR)** | Aplikace A (Pokojový termostat) | Aplikace B (Balicí linka) | Aplikace C (Kamerová kontrola svarů) |
| :--- | :--- | :--- | :--- | :--- |
| **Doporučená platforma** *(MCU / PLC / iPC)* | **Programovatelné relé / kompaktní PLC** *(např. Siemens LOGO!, Eaton easyE4)* | **MCU / Embedded SoC** *(např. ESP32-C3, nRF52840, STM32)* | **Modulární PLC** *(např. Siemens S7-1200 / S7-1500, Schneider M241)* | **Průmyslové PC – iPC** *(s akcelerací GPU/NPU, např. Beckhoff C6030)* |
| **Pořizovací cena HW na 1 kus** *(nízká < 500 Kč / střední 5–30 tis. Kč / vysoká > 50 tis. Kč)* | **Střední** *(cca 3 500 – 6 000 Kč)* | **Nízká** *(cca 80 – 250 Kč za čip/desku při sérii 10 000 ks)* | **Střední až vysoká** *(cca 15 000 – 35 000 Kč dle modulů)* | **Vysoká** *(cca 60 000 – 120 000 Kč včetně GPU a karet)* |
| **Primární programovací jazyk** *(C/C++/MicroPython vs. IEC 61131-3 ST/LAD vs. Python/C#/C++ pod OS)* | **FBD / LAD** *(grafické funkční bloky nebo liniové schéma dle IEC 61131-3)* | **C / C++ / MicroPython** *(využití SDK od výrobce, např. ESP-IDF)* | **IEC 61131-3** *(převážně LAD / FBD / ST)* | **Python / C++ / C#** *(pod OS Linux/Windows s OpenCV/PyTorch)* |
| **Klíčový technický argument pro volbu** *(např. spotřeba, determinismus, grafický výkon)* | Montáž přímo na DIN lištu v rozváděči, integrovaný displej pro nastavení časovačů přímo na místě, robustní reléové výstupy pro motor a semafor, napájení 24 V DC / 230 V AC bez nutnosti vývoje vlastního plošného spoje. | Extrémně nízká spotřeba energie (deep-sleep režimy pro bateriový provoz), integrovaná RF část (ZigBee/Wi-Fi), miniaturní rozměry a velmi nízká kusová cena při masové sérii. | Vysoký determinismus reálného času, modularita (rozšíření o I/O moduly), vysoká odolnost EMC v průmyslu 24/7, snadný servis provozním elektrikářem v LAD. | Obrovský výpočetní výkon pro analýzu 4K obrazu neuronovou sítí v reálném čase, vysokorychlostní PCIe/GigE sběrnice a přímá SQL/MES konektivita. |
| **Hlavní riziko při volbě špatné platformy** *(proč by neuspěly ostatní dvě varianty)* | **MCU:** Nutnost vývoje vlastní desky, nízká odolnost vůči venkovnímu rušení a obtížný servis údržbou.<br>**iPC:** Zbytečně extrémní cena (> 30 tis. Kč), dlouhý start po výpadku napájení a vysoká spotřeba. | **PLC / iPC:** Vysoký příkon (nelze provozovat z baterie), obrovské rozměry, vysoká cena zmaří ekonomiku masového produktu. | **MCU:** Neuchopitelný servis elektrikáři, riziko rušení.<br>**iPC:** Zbytečně drahé, dlouhé naběhnutí po výpadku napájení, riziko pádu OS. | **MCU / PLC:** Nemají dostatek paměti RAM, chybí GPU výpočetní výkon pro AI a nepodporují GigE kmitočty ani ukládání do SQL databází. |

> **Kritéria hodnocení úlohy 3 (bodování a známka):**
> - :star: **Správnost technického přiřazení platforem (30 %):** Stoprocentně logické a obhajitelné přiřazení všech 3 technologií.
> - :star: **Inženýrská a ekonomická argumentace (40 %):** Zohlednění ekonomiky sériovosti (kusová vs. masová výroba), spotřeby energie, náročnosti vývoje a schopností servisního personálu.
> - :star: **Analýza rizik nevhodné platformy (30 %):** Věcné zdůvodnění, proč je v daném případě jiná platforma neefektivní, příliš drahá nebo neschopná úlohu odbavit.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Norma ČSN EN 61131-3:** Mezinárodní standard pro programovací jazyky PLC automatů. Definuje dva textové jazyky (ST – strukturovaný text, IL – seznam instrukcí) a tři grafické jazyky (LD – příčkový diagram / kontaktní schéma, FBD – funkční blokové schéma, SFC – sekvenční funkční schéma).
> 	ČESKÝ NORMALIZAČNÍ INSTITUT. *ČSN EN 61131-3 ed. 3 (18 0080) Programovatelné řídicí jednotky - Část 3: Programovací jazyky*. Praha: Úřad pro technickou normalizaci, metrologii a státní zkušebnictví, 2014. Třídící znak 180080.
> - **GigE Vision:** Komunikační standard rozhraní pro průmyslové kamery využívající gigabitový Ethernet, umožňující přenos nekomprimovaného videa vysokou rychlostí na velké vzdálenosti.

<details>
<summary> :bulb: Tip pro Aplikaci A vs. B vs. C: </summary>
<p>U aplikace A rozhoduje kusová cena a odběr proudu z baterie (PLC ani iPC z baterie nerozběhnete). U aplikace B potřebujete vyměnitelný modul na DIN lištu s diagnostickými LED, který přeprogramuje běžný údržbář v jazyce LAD. U aplikace C potřebujete obrovský výpočetní výkon pro AI a ovladače pro průmyslové kamery, což MCU ani běžné PLC nezvládne.</p>
</details>

:star2: **Bonusová otázka k úloze 3:**
Co je to tzv. **SoftPLC** a jak umožňuje průmyslovému PC (iPC) kombinovat výhody operačního systému Windows/Linux a deterministického řízení reálného času v jediném fyzickém počítači?

*Vaše odpověď:*
**SoftPLC** je softwarové řešení (např. Beckhoff TwinCAT, CODESYS), které běží na průmyslovém PC s využitím real-time hypervisoru. Hypervisor vyhradí jedno nebo více procesorových jader výhradně pro deterministický běh řídicího programu reálného času (Hard Real-Time), zatímco na zbylých jádrech běží standardní operační systém (Windows/Linux) pro HMI, databáze a komunikaci. Tím je zaručeno, že pád nebo vytížení Windows nijak neovlivní přesnost řízení strojního procesu.

---

### 4. Návrh a konfigurace řídicí jednotky pro čerpací stanici

*Časová dotace: 25–30 minut | Klasifikovaná inženýrská úloha na známky*

Projekt řízení obecní přečerpávací stanice odpadních vod ve venkovním prostředí (-20 °C až +45 °C).

---

#### Zadání technologického procesu a periferií

- **Snímače a vstupy:**
  - 3× plovákový hladinový spínač (havarijní spodní hladina, zapínací hladina, havarijní přepad) – bezpotenciálový kontakt 24 V DC.
  - 1× hydrostatická ponorná sonda výšky hladiny v jímce – analogový signál 4–20 mA.
  - 1× termistorové ochranné relé přehřátí motoru čerpadla – poruchový kontakt 24 V DC.
- **Akční členy a výstupy:**
  - 2× stykač pro spouštění motorů hlavního a záložního čerpadla – spínání cívky 230 V AC / 0,5 A.
  - 1× opticko-akustický výstražný maják – napájení 24 V DC / 0,3 A.
  - 1× řízení otáček frekvenčního měniče hlavního čerpadla – analogový signál 0–10 V.
- **Komunikace a přenos dat:**
  - Odesílání údajů o hladině a poruchách na dispečink vodáren (Ethernet / Modbus TCP nebo GSM/LTE modul).
- **Provozní podmínky:**
  - Venkovní nekrytý terén, rozváděč vystaven dešti, prachu a teplotám **-20 °C až +45 °C**.

---

#### 1. I/O bilance (+20 % rezerva)

| Typ signálu | Požadavek (ks) | Popis v aplikaci | Počet s rezervou (+20 %) |
| :--- | :--- | :--- | :--- |
| **DI** (Digitální vstup) | **4** | 3× plovák, 1× ochrana motoru (přehřátí) | **5** *(4 × 1,2 = 4,8 -> zaokrouhleno nahoru)* |
| **DO** (Reléový výstup) | **2** | 2× cívka stykače čerpadel (230 V AC) | **3** *(2 × 1,2 = 2,4 -> zaokrouhleno nahoru)* |
| **DO** (Tranzistorový výstup) | **1** | 1× výstražný maják (24 V DC) | **2** *(1 × 1,2 = 1,2 -> zaokrouhleno nahoru)* |
| **AI** (Analogový vstup) | **1** | 1× ponorná sonda hladiny (4–20 mA) | **2** *(1 × 1,2 = 1,2 -> zaokrouhleno nahoru)* |
| **AO** (Analogový výstup) | **1** | 1× řízení frekvenčního měniče (0–10 V) | **2** *(1 × 1,2 = 1,2 -> zaokrouhleno nahoru)* |

---

#### 2. Výběr hardwaru

- **Řídicí jednotka (CPU):** Siemens SIMATIC S7-1200, CPU 1212C DC/DC/Relé
- **Objednací kód (Part Number):** `6ES7212-1HE40-0XB0`
- **Rozšiřující moduly:**
  - `SB 1232 AQ 1x13-bit` (`6ES7232-4HA30-0XB0`) – deska pro analogový výstup 0–10 V (pro frekvenční měnič).
  - `SM 1231 AI 4x13-bit` (`6ES7231-4HD32-0XB0`) – modul pro analogový vstup 4–20 mA (pro hydrostatickou sondu).
  - `CP 1243-7 LTE` (`6GK7243-7KX30-0XE0`) – LTE modul pro SMS alarmy a přenos dat na dispečink.
- **Napájení:** 24 V DC (např. spínaný zdroj Siemens LOGO!Power 24V / 2,5A).
- **Odesílání dat na dispečink:** Integrovaný Ethernet port (Modbus TCP) + LTE modul pro přenos dat na SCADA dispečink a zasílání havarijních SMS.
- **Odkaz na datasheet:** [Siemens Industry Online Support](https://support.industry.siemens.com/cs/document/109742283/)

---

#### 3. Technické ověření

- **Provoz při -20 °C:**
  - Novější revize Siemens S7-1200 (od firmware V4.4) mají v datasheetu garantovaný rozsah provozních teplot **-20 °C až +60 °C**.
- **Spínání cívky stykače 230 V AC:**
  - Cívka se spíná **přes pomocné mezipatrové relé** na DIN lištu (např. Finder). 
  - **Zdůvodnění:** Cívka stykače je indukční zátěž, která při vypnutí vytváří napěťové špičky a opaluje kontakty. Pomocné relé stojí pár korun a dá se snadno vyměnit v patici, zatímco oprava vypáleného výstupu na PLC je drahá a složitá.

---

#### 4. Krytí a řešení rozváděče

- **Krytí rozváděče:** **IP65** (prachotěsné a odolné proti tryskající dešťové vodě) s krycí stříškou proti dešti.
- **Teplotní management:**
  - **Zima (-20 °C):** Odporové topné těleso s termostatem (např. STEGO 50 W nastavené na +5 °C). Slouží proti mrazu a hlavně **zabraňuje kondenzaci vlhkosti** na elektronice.
  - **Léto (+45 °C):** Stříška proti slunci, dvojitá stěna nebo větrací mřížky s filtrem IP54 (případně ventilátor s termostatem).

> **Kritéria hodnocení úlohy 4 (bodování a známka):**
> - :star: **Správnost I/O bilance a dimenzování (30 %):** Správný součet všech signálů, korektní rozlišení reléových vs. tranzistorových výstupů a správné započtení rezervy min. 20 %.
> - :star: **Reálnost výběru a kompatibilita HW (40 %):** Zvolený přístroj skutečně existuje na trhu, konfigurace plně pokrývá všechny vstupy/výstupy (včetně analogů 4–20 mA a 0–10 V) a komunikaci.
> - :star: **Posouzení provozních podmínek a instalace (30 %):** Správná volba krytí rozváděče (min. IP65), vyřešení vytápění/ventilace pro mráz a spolehlivé galvanické oddělení výkonových akčních členů.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Proudová smyčka 4–20 mA:** Průmyslový standard pro přenos analogových signálů ze senzorů. Výhodou oproti napěťovému signálu 0–10 V je vysoká odolnost proti elektromagnetickému rušení, nezávislost na odporu dlouhého vedení a detekce přetržení vodiče (pokud je proud roven 0 mA, jde o poruchu vedení – tzv. živá nula / live zero).
> 	Proudová smyčka. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2023, 2023-04-18 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Proudov%C3%A1_smy%C4%8Dka
> - **Galvanické oddělení:** Elektrické oddělení dvou elektrických obvodů (např. pomocí optočlenů nebo relé), které zabraňuje přenosu rušení, rozdílům zemních potenciálů a chrání citlivé vstupy řídicí jednotky před zničením přepětím.
> - **Bezpotenciálový kontakt** (označovaný také jako **dry contact**) je elektrický kontakt, který sám o sobě nemá žádné vlastní napětí ani neposkytuje žádný proud. Funguje čistě jako mechanický nebo elektronický spínač (jako klasický vypínač na zdi), který pouze spojí nebo rozpojí dva vodiče v externím obvodu.

<details>
<summary> :bulb: Tip pro výběr modulů: </summary>
<p>Pozor na analogové vstupy: Základní kompaktní jednotky (např. LOGO! nebo S7-1200) mívají integrované analogové vstupy pouze pro napětí 0–10 V. Vstupní signál 4–20 mA ze sondy vyžaduje buď speciální rozšiřující modul pro proudové signály, nebo zařazení přesného paralelního odporu 500 Ω (převod 4–20 mA na 2–10 V).</p>
</details>

:star2: **Bonusová otázka k úloze 4:**
Proč se u čerpadel v čistírnách odpadních vod a jímkách striktně upřednostňuje měření hladiny pomocí proudového signálu 4–20 mA před napěťovým signálem 0–10 V a proč se do jímky nepoužívá ultrazvukový senzor, pokud v ní vzniká hustá pěna?

*Vaše odpověď:*
Signal 4–20 mA se upřednostňuje kvůli odolnosti proti rušení na dlouhém vedení a kvůli detekci přerušeného vodiče (proud < 4 mA znamená poruchu vedení – živá nula). Ultrazvukový senzor nelze v pěnících jímkách použít, protože hustá pěna pohlcuje a rozptyluje akustické ultrazvukové vlny. Sonda tak měří falešný odraz od povrchu pěny nebo signál zcela ztratí, což vede ke špatnému vyhodnocení výšky hladiny kapaliny.

---

### 5. Technický audit a oponentura nevhodného návrhu

*Časová dotace: 20–25 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jako vedoucí inženýr jste převzal projekt po nezkušeném brigádníkovi, který navrhl řízení automatizovaného tvářecího a lisovacího stroje v prašné kovářské dílně následovně:
- **Řídicí deska:** Běžná vývojová deska **Arduino Uno (Rev3)** s mikrokontrolérem ATmega328P.
- **Pouzdro a umístění:** Plastová krabička vytištěná na 3D tiskárně z materiálu **PLA**, přišroubovaná přímo na těleso vibrujícího hydraulického lisu.
- **Napájení:** 5V USB nabíječka na mobilní telefon zapojená do prodlužovacího kabelu 230 V.
- **Spínání zátěže:** 4kanálový hobby reléový modul z čínského e-shopu propojený s Arduinem tenkými nepájenými vodiči (DuPont propojky). Modul přímo spíná 400V ventily hydrauliky.
- **Bezpečnost (Safety):** Nouzové stop tlačítko (E-Stop) je zapojeno přímo do digitálního pinu D2 Arduina jako softwarové přerušení (interrupt), které v kódu nastaví výstupy na `LOW`.

#### Váš úkol:

1. **Zpracujte písemný audit rizik (minimálně 4 fatální technická selhání):**
   Vyplňte protokol o zjištěných vadách a popište konkrétní fyzikální mechanismus, jak daná chyba způsobí havárii stroje či ohrožení lidského života:

| Oblast auditu | Zjištěná vada v amatérském návrhu | Fyzikální mechanismus selhání (proč to selže) | Následek pro stroj nebo obsluhu |
| :--- | :--- | :--- | :--- |
| **Elektromagnetická kompatibilita (EMC)** | Absence odrušení, nestíněné vodiče, hobby relé bez snubberů spínající indukční zátěž. | Spínáním hydraulických ventilů vzniká silná indukční napěťová špička ($V = L \frac{di}{dt}$), která se naindukuje do nepájených DuPont vodičů a vyvolá restart nebo zamrznutí procesoru ATmega328P. | Stroj se nekontrolovaně zastaví v půli cyklu nebo provede nechtěný pohyb, což může způsobit havárii lisu nebo úraz obsluhy. |
| **Mechanická a teplotní odolnost** | PLA plast a montáž na těleso lisu | PLA podléhá skelnému přechodu již při cca 60 °C a mechanické vibrace lisu způsobí únava materiálu, praskání PLA krabičky a mikrotrhliny v plošném spoji Arduina. | Rozpad krabičky, uvolnění desky, zkrat s kostrou stroje a kompletní destrukce řídicí elektroniky. |
| **Konektivita a propojení vodičů** | DuPont propojovací kabely bez aretace | Nástrčné DuPont konektory nemají žádné mechanické zajištění. Vibracemi lisu dojde k vyklepání spojů, oxidačnímu opotřebení kontaktů a vzniku přechodových odporů. | Nahodilé ztráty signálu, výpadky napájení, spínání nesprávných ventilů a neovladatelnost stroje. |
| **Funkční bezpečnost (Safety)** | Nouzový stop řešený softwarově v čipu | Pokud mikrořadič zamrzne (působením EMC rušení nebo zacyklením softwaru), procesor přerušení neobslouží a výstupy zůstanou v náhodném stavu (HIGH). | **Fatální bezpečnostní riziko:** Tlačítko Central Stop po stisknutí neodpojí stroj, lis pokračuje v pohybu a dojde k těžkému či smrtelnému úrazu obsluhy. |

2. **Návrh profesionálního nápravného řešení:**
   - Navrhněte, jakými certifikovanými průmyslovými komponenty tento celek nahradíte při zachování minimálního rozpočtu:
     - *Náhrada řídicí jednotky:* `Certifikované průmyslové programovatelné relé (např. Siemens LOGO! 24RCE nebo Eaton easyE4) umístěné v samostatném oceloplechovém rozváděči IP65 mimo těleso lisu.`
     - *Náhrada napájecího zdroje:* `Průmyslový stabilizovaný spínaný zdroj 24 V DC na DIN lištu (např. Mean Well MDR-20-24) s integrovanou ochranou proti přetížení, přepětí a s EMC filtrem.`
     - *Způsob zapojení bezpečnostního okruhu (Safety):* Jak musí být podle norem zapojeno tlačítko Emergency Stop (E-Stop)? Smí být spoléháno pouze na software mikrokontroléru? Zdůvodněte: `Podle ČSN EN ISO 13849-1 NESMÍ být E-Stop závislý na softwaru. Tlačítko E-Stop (dvoukanálové s NC kontakty) musí být zapojeno natvrdo do certifikovaného bezpečnostního relé (např. Pilz PNOZ nebo Schneider Preventa). Toto relé při stisku galvanicky a nekompromisně odpojí silové napájení ventilů a motoru lisu na hardwarové úrovni nezávisle na jakémkoliv mikrokontroléru!`

> **Kritéria hodnocení úlohy 5 (bodování a známka):**
> - :star: **Odborná úroveň identifikace závad (35 %):** Přesná technická terminologie (např. elektromagnetická indukce, absence odrušovacích varistorů, skelný přechod PLA plastu při 60 °C, studené spoje a vyklepání konektorů vibracemi).
> - :star: **Pochopení norem funkční bezpečnosti Safety (35 %):** Znalost základního principu bezpečnosti strojních zařízení – nouzové zastavení musí být řešeno hardwarově přes certifikované bezpečnostní relé s nuceně vedenými kontakty, nikoliv pouhým softwarovým vstupem MCU.
> - :star: **Kvalita a realizovatelnost nápravného řešení (30 %):** Návrh odpovídá robustní průmyslové praxi s montáží do oceloplechového rozváděče na DIN lištu.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Funkční bezpečnost (Safety) vs. Kybernetická bezpečnost (Security):** *Safety* (dle ČSN EN ISO 13849-1) zajišťuje, že strojní zařízení nezpůsobí úraz člověku ani při vnitřní poruše řídicího systému (využívá redundantní obvody, bezpečnostní relé, optické závory, kategorii spolehlivosti PL a až PL e / SIL 3). *Security* řeší ochranu dat a systému před úmyslným napadením zvenčí (hackeři, malware).
> - **EMC (Elektromagnetická kompatibilita):** Schopnost zařízení spolehlivě pracować v prostředí s elektromagnetickým rušením (odolnost / imunita) a současně nezpůsobovat nepřípustné rušení jiným zařízením (emise).
> 	Elektromagnetická kompatibilita. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2023, 2023-11-20 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Elektromagnetick%C3%A1_kompatibilita

<details>
<summary> :bulb: Tip k bezpečnostnímu okruhu (Safety): </summary>
<p>Základní pravidlo bezpečnosti: <strong>Software může selhat, zacyklit se nebo zamrznout.</strong> Bezpečnostní okruh nouzového zastavení (červený hřib) musí být vždy dvoukanálový, zapojený do hardwarového bezpečnostního relé (např. Pilz, Schneider Preventa, Siemens SIRIUS), které odpojí silové napájení stykačů ventilů přímo na hardwarové úrovni nezávisle na procesoru!</p>
</details>

:star2: **Bonusová otázka k úloze 5:**
Proč hobby reléové moduly s optočleny určené pro Arduino v průmyslovém rozváděči často shoří nebo způsobí trvalé sepnutí zátěže (tzv. přivaření kontaktů), i když jmenovitý proud relé je 10 A a cívka stykače odebírá jen 0,5 A?

*Vaše odpověď:*
Indukční zátěž (cívka stykače či solenoid) při rozpojení generuje obrovské napěťové špičky a při spínání vyvolává proudový náraz. Hobby relé používají nekvalitní slitinové kontakty s malým odskokem a nemají integrované odrušovací členy (RC člen / varistor). Vniklý elektrický oblouk způsobený vysokým napětím speče a fyzicky přivaří kontakty k sobě (tzv. přivaření kontaktů / contact welding), což způsobí trvalé sepnutí zátěže.

---

### 6. Rozšiřující inženýrská výzva: TCO a životní cyklus v automatizaci

*Časová dotace: 15–20 minut | :star2: Bonusová výzva pro pokročilé studenty*

V průmyslové automatizaci nákupní cena řídicí jednotky (CAPEX) často tvoří méně než 15 % celkových nákladů na životní cyklus zařízení (OPEX / TCO).

Představte si, že management firmy rozhoduje mezi dvěma variantami řízení pro sérii 50 kusů výrobních linek s plánovanou životností 15 let:
- **Varianta 1 (Nízkonákladová na pořízení):** Využití levných embedded mikrokontrolérových desek s vlastním zákaznickým návrhem plošného spoje (cena HW: 2 500 Kč / kus, vývoj firmwaru v C/C++ od externího programátora bez dokumentace).
- **Varianta 2 (Průmyslový standard):** Využití modulárního PLC renomovaného výrobce (Siemens / Rockwell / Schneider) s cenou 22 000 Kč / kus, programováno v normovaném jazyce LAD/ST dle IEC 61131-3.

#### Váš úkol:
1. Srovnejte obě varianty v níže uvedené tabulce a uveďte předpokládaná skrytá rizika a náklady v horizontu 10–15 let:

| Aspekt životního cyklu | Varianta 1 (Custom Embedded MCU) | Varianta 2 (Průmyslové PLC) |
| :--- | :--- | :--- |
| **Dostupnost náhradních dílů za 10 let** | **Nulová až kritická.** Součástky se přestanou vyrábět (EOL), custom desku nikdo nedodá, nutnost nákladného kompletního redesignu HW. | **Garantovaná.** Výrobci průmyslových PLC garantují dostupnost náhradních dílů a zpětnou kompatibilitu po dobu 10–20 let. |
| **Servisovatelnost podnikovým elektrikářem** | **Nemožná.** Běžný údržbář nemá C/C++ vývojové prostředí, zdrojový kód ani HW programátor. Vyžaduje externího vývojáře. | **Vysoká.** Běžný provozní elektrikář zná IEC 61131-3 (LAD), dokáže se připojit k PLC, diagnostikovat vadný vstup/výstup a vyměnit modul. |
| **Doba odstávky linky při poruše CPU** | **Dny až týdny.** Nutnost shánět specifikované komponenty, ručně pájet desku nebo čekat na externího programátora. | **Desítky minut.** Výměna modulární jednotky na DIN liště "kus za kus", nahrání zálohy projektu z paměťové karty (SD). |
| **Cena vývojových nástrojů a licencí IDE** | **Nízká.** Využití open-source IDE (GCC, VS Code), ovšem s obrovskými skrytými náklady na čas vývojáře. | **Střední až vysoká.** Nákup průmyslové licence (např. Siemens TIA Portal cca 30–80 tis. Kč), vývoj je ale dramaticky rychlejší díky knihovnám. |
| **Závěrečné doporučení (kterou variantu vybrat a proč)** | **ZAMÍTNOUT.** Výhodná pouze zdánlivě při nákupu (CAPEX). Riziko extrémních nákladů na odstávky a ztráty podpory v budoucnu. | **VYBRAT VARIANTU 2.** Vyšší počáteční investice se vrátí v minimálních nákladech na údržbu, rychlém servisu a zaručené životnosti 15 let (nízké TCO). |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **CAPEX (Capital Expenditure)**: Zjednodušeně jde o jednorázové kapitálové výdaje na pořízení samotného zařízení (hardware, licence).
> - **OPEX (Operating Expense)**: Zjednodušeně jde o průběžné provozní náklady nutné k udržení zařízení v chodu (energie, servis, podpora).
> - **TCO (Total Cost of Ownership):** Finanční odhad celkových přímých i nepřímých nákladů spojených s pořízením, provozem, servisem, údržbou a likvidací produktu po celou dobu jeho životnosti. Zjednodušeně je to součet CAPEX + OPEX za celou dobu životnosti zařízení. 
> 	Total cost of ownership. *Wikipedia: The Free Encyclopedia* [online]. St. Petersburg (Florida): Wikimedia Foundation, 2024, 2024-08-14 [cit. 2026-09-17]. Dostupné z: https://en.wikipedia.org/wiki/Total_cost_of_ownership
> - **Vendor Lock-in:** Stav závislosti zákazníka na konkrétním dodavateli produktů nebo služeb, kdy je přechod k jiné platformě spojen s neúměrně vysokými finančními i časovými náklady.

<details>
<summary> :bulb: Tip k úvaze o TCO: </summary>
<p>Když za 7 let odejde custom deska z Varianty 1 a původní vývojář již ve firmě nepracuje a čip se nevyrábí, musí firma vyvinout celou řídicí elektroniku znovu od nulas. Hodina odstávky automobilové linky přitom stojí desítky až stovky tisíc korun.</p>
</details>

:star2: **Bonusová otázka k úloze 6:**
Co znamená pojem **MTBF (Mean Time Between Failures)** v datasheetech průmyslových řídicích jednotek a jaký vliv má okolní teplota v rozváděči na tuto hodnotu (tzv. Arrheniovo pravidlo)?

*Vaše odpověď:*
**MTBF (Střední doba mezi poruchami)** udává předpokládanou provozní dobu zařízení v hodinách, po kterou pracovat bez poruchy. Podle **Arrheniovy rovnice (pravidlo 10 °C)** platí, že nárůst provozní teploty o každých 10 °C nad nominální hodnotu zdvojnásobuje rychlost degradace polovodičů a kondenzátorů, což zkracuje hodnotu MTBF na **polovinu**. Proto je správné chlazení rozváděče zásadní pro zachování spolehlivosti.
