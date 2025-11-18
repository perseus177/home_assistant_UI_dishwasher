# 🇸🇰 Home Assistant Lovelace Konfigurácia pre Umývačku Riadu Bosch (Hybridné Ovládanie)

### ⚠️ Disclaimer (Vylúčenie Zodpovednosti)

Táto konfigurácia bola vytvorená a optimalizovaná s asistenciou **generatívneho modelu Google Gemini**. Hoci bola kódová báza rozsiahlo testovaná, používateľ preberá plnú zodpovednosť za implementáciu a akékoľvek potenciálne chyby alebo neočakávané správanie vo svojom prostredí Home Assistant.

---

Táto konfigurácia poskytuje pokročilé a vizuálne atraktívne ovládanie a monitoring pre umývačku riadu v prostredí Home Assistant Lovelace. Využíva **hybridný prístup**:

1.  **Stavové dáta a programy** sú získavané z oficiálnej integrácie **Home Connect**.
2.  **Ovládanie hlavného napájania a monitorovanie spotreby** je riešené cez **Smart Zásuvku s Tasmota** pre rýchlu reakciu a spoľahlivé meranie.

Konfigurácia zahŕňa dynamické zobrazenie stavu v slovenčine, výber programov, doplnkové funkcie, priebeh cyklu s animovaným progress barom a prehľad spotreby/zásob.

**Testované na verzii Home Assistant:** `2025.10.4`

### ⚙️ Predpoklady (Preconditions)

Pre správne fungovanie tejto konfigurácie je nevyhnutné mať nainštalované nasledujúce custom doplnky (dostupné cez **HACS**) a zabezpečiť dostupné entity.

#### Custom HACS Doplnky
* **Lovelace Mushroom Cards**: `custom:mushroom-template-card`, `custom:mushroom-chips-card`
* **Lovelace Button Card**: `custom:custom:button-card`
* **Lovelace Card-mod**
* **Browser Mod**

#### Integrácia Zariadenia

Táto konfigurácia je navrhnutá pre umývačku riadu **Bosch SMV88TX46E**.

| Entita (Príklad) | Zdroj | Popis |
| :--- | :--- | :--- |
| `switch.umyvackazasuvka` | **NOUS A1T (Tasmota)** | Hlavný vypínač a ochrana pre celú umývačku. |
| `sensor.umyvackazasuvka_energy_power` | **NOUS A1T (Tasmota)** | Aktuálna spotreba vo W. |
| `sensor.dishwasher_prevadzkovy_stav` | **Home Connect** | Aktuálny stav (run, finished, error, atď.). |
| `select.dishwasher_aktivny_program` | **Home Connect** | Výber a zobrazenie programu. |
| `sensor.dishwasher_sol_takmer_prazdna` | **Home Connect** | Stav zásob soli. |
| *Všetky ostatné `dishwasher_` entity* | **Home Connect** | Stavy dverí, priebeh, diaľkový štart, doplnky. |

### ✨ Vlastnosti a Vizualizácia

#### 1. Hlavný Prehľad (Mushroom Template Card)

* **Dynamický stav:** Okamžité zobrazenie stavu v slovenčine, s logikou priority (Odpojená > Vypnutá > Cyklus).
* **Farebné notifikácie:** Ikona karty mení farbu podľa kritickosti (Modrá pre beh, Červená pre chybu/akciu).
* **Animácia (Card-mod):** Ikona umývačky sa jemne trasie, ak je program v stave `run` (imitácia umývania), a zmení sa na `mdi:dishwasher-alert`.

<img src="https://github.com/user-attachments/assets/9052b0f6-b6b7-41bc-87d7-7d02bd232443" width="40%" alt="Screenshot 1: Prebieha cyklus"/>
<img src="https://github.com/user-attachments/assets/59c396c1-639d-4fed-bb2e-ed88ddfc1c1c" width="40%" alt="Screenshot 2: Umývačka riadu prehľad"/>


#### 2. Detailné Ovládanie (Pop-up Modálne Okno)

* **Sekvenčné Zapnutie:** Podmienené veľké tlačidlá s kruhovým vizuálom pre postupné zapnutie (Zásuvka (Tasmota) -> Umývačka (Home Connect)).
* **Vizuálny Indikátor Programu:** Veľký kruhový indikátor s animovaným krúžkom pri behu. Farba krúžku vizuálne signalizuje potrebnú akciu (napr. **Oranžová** pre "Zatvor dvierka").
* **Rýchly Výber Programov (Chips):** Možnosť rýchlo zvoliť najčastejšie programy s vizuálnym zvýraznením aktívneho.
* **Progress Bar:** Počas behu sa zobrazuje vizuálny progress bar s percentuálnym priebehom.
* **Informačné Riadky:** Prehľad zásob (Soľ, Leštidlo), stavu dvierok, aktuálnej spotreby a predpokladaného konca programu.
<img src="https://github.com/user-attachments/assets/a4472ad7-9d20-4e76-ad6f-ca3128dc77bf" width="20%" alt="Screenshot_20251118_203937_Home Assistant"/>
<img src="https://github.com/user-attachments/assets/4cc93d0e-82cb-4094-b311-c781f979ab76" width="20%" alt="Screenshot_20251118_204029_Home Assistant"/>
<img src="https://github.com/user-attachments/assets/5b52edc6-0e93-416e-b574-bd356eee5461" width="20%" alt="Screenshot_20251118_204015_Home Assistant"/>
<img src="https://github.com/user-attachments/assets/c30e1e5e-54cd-49ea-b55a-807bd6c25e7f" width="20%" alt="Screenshot_20251118_204055_Home Assistant"/>
<img src="https://github.com/user-attachments/assets/116e1c24-ef6c-477c-ad5c-a236b90e33ba" width="20%" alt="Screenshot_20251118_204041_Home Assistant"/>
<img src="https://github.com/user-attachments/assets/6130001c-0e5b-4d14-b5fa-d48d614d0129" width="20%" alt="Screenshot_20251118_205739_Home Assistant"/>
<img src="https://github.com/user-attachments/assets/87907fea-2476-491c-bc59-4c76c4d6bf91" width="20%" alt="Screenshot_20251118_205350_Home Assistant"/>
<img src="https://github.com/user-attachments/assets/2923bb13-3fbf-4c94-a1ae-f2f76c75c4d1" width="20%" alt="Screenshot_20251118_204240_Home Assistant"/>





---

### 📋 YAML Kód

Kompletný YAML kód konfigurácie je súčasťou tohto repozitára.
