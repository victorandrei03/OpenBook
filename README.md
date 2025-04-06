# OpenBook

## 📋 Descriere Proiect
Acest proiect reprezintă o placă electronică (e-board) customizată, proiectată în Autodesk Fusion 360. Include:
- Schematică completă
- Design PCB
- Design 3D al carcasei
- Listă completă de componente (BOM)

## 🛠️ Componente Cheie
| Componentă | Model | Descriere |
|------------|-------|-----------|
| **Microcontroler** | ESP32-C6-WROOM-1-N8 | MCU principal cu WiFi/Bluetooth LE |
| **Ceas RTC** | DS3231SN# | Ceas în timp real cu compensare de temperatură |
| **Senzori** | BME680 | Senzor ambiental (temperatură, umiditate, presiune, VOC) |
| **Management Power** | BD5229G-TR + MCP73831 | Sistem complet de încărcare baterii |

## 📊 Bill of Materials (BOM)

### 🔌 Conectori & Interfețe
| Part Name | Device | Link |
|-----------|--------|------|
| J1 | FH34SRJ-24S-0.5SH_99_ | [Datasheet](https://componentsearchengine.com/part-view/XC6220A331MR-G/Torex) |
| J2 | USB4110-GF-A | [Mouser](https://componentsearchengine.com/part-view/USB4110-GF-A/GCT) |
| J3 | QWIIC_CONNECTORJS-1MM | [SparkFun](https://www.sparkfun.com/products/14417) |

### 💾 Memorie & Storage
| Part Name | Device | Link |
|-----------|--------|------|
| U1 | W25Q512JVEIQ | [Winbond](https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/) |

### ⚡ Power Management
| Part Name | Device | Link |
|-----------|--------|------|
| IC1 | BD5229G-TR | [ROHM](https://componentsearchengine.com/part-view/BD5229G-TR/ROHM) |
| U4 | MAX17048G+T10 | [Analog Devices](https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/) |

### 🎚️ Componente Pasive
| Categorie | Qty | Device | Link |
|-----------|-----|--------|------|
| **Rezistoare** | 25+ | RR0402 100K | [YAGEO](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K/YAGEO) |
| **Condensatoare** | 20+ | CC0402 1µF | [YAGEO](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO) |
| **Inductoare** | 1 | 744043680 | [Würth](https://eu.mouser.com/ProductDetail/Wurth-Elektronik/744043680) |

### 🛑 Protecții & Diodes
| Part Name | Device | Link |
|-----------|--------|------|
| D1 | USBLC6-2SC6Y | [STMicro](https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/) |
| D3-D5 | MBR0530 | [Mouser](https://eu.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0) |

## 🛠️ Descriere Hardware Detaliată

### 1. Microcontroller - ESP32-C6-WROOM-1-N8
**Specificații Avansate:**
- **Arhitectură:** RISC-V single-core cu 160MHz (configurabil dinamic)
- **Memorie:**
  - 320KB SRAM intern (pentru date)
  - 512KB ROM (pentru bootloader)
  - 8MB Flash SPI (W25Q512JVEIQ) - stochează firmware și date utilizator
- **Conectivitate:**
  - **WiFi 6** (802.11ax) cu throughput de până la 300Mbps
  - **Bluetooth 5 LE** cu support Mesh
  - **Zigbee 3.0** pentru IoT industrial
- **Periferice Integrate:**
  - 4× controller SPI (inclusiv Quad-SPI)
  - 2× I²C (software configurable)
  - 2× UART (cu flow control hardware)
  - 1× USB 2.0 OTG Full-Speed

**Management Energie:**
- **Moduri de operare:**
  - Active Mode: 80mA @ 160MHz
  - Light Sleep: 1.5mA (perif. RAM păstrate)
  - Deep Sleep: 20µA (doar RTC activ)
- **Feature-uri speciale:**
  - Wake-up din Deep Sleep prin:
    - GPIO
    - Timer RTC
    - UART
    - Senzor BME680 (via interrupt)
   
---

### 2. Sistem de Alimentare

**Componente Cheie:**
1. **MCP73831**
   - Curent de încărcare programabil: 100-500mA
   - Protecții integrate: Over-voltage, Reverse discharge
   - LED indicator de stare (conectat la GPIO18)

2. **BD5229G-TR**
   - Eficiență 92% @ 500mA load
   - Ripple voltage < 50mV
   - Shutdown current < 1µA

3. **MAX17048G+T10**
   - Precizie măsurare: ±1% SOC
   - Alertă baterie critică (conectat la GPIO15)
   - Consum propriu: 7µA în mod normal

---

### 3. Senzori & Periferice

#### 3.1 Senzor Environmental BME680
**Interfață:** I²C @ 400kHz (adresă 0x76)  
**Caracteristici unice:**
- **Algoritm BSEC** pentru calcul IAQ (Indice Calitate Aer)
- **Compensare automată** a variațiilor de temperatură
- **Calibrare în fabrică** pentru precizie ridicată

**Conexiuni:**
| Pin BME680 | Pin ESP32 | Notă |
|------------|-----------|------|
| VDD        | 3.3V      | Alimentare filtrată |
| GND        | GND       | - |
| SDA        | GPIO1     | Cu pull-up 4.7kΩ |
| SCL        | GPIO2     | Cu pull-up 4.7kΩ |

#### 3.2 Real-Time Clock DS3231SN#
**Precizie:** ±2ppm (echiv. ~1min/an)  
**Backup:** Supercondensator CPH3225A (10F @ 3.3V)  
**Funcționalități:**
- Alarmă programabilă
- Output square wave (1Hz-32kHz)
- Temperatură internă compensată

---

### 4. Interfețe Externe

#### 4.1 Port USB-C
**Implementare:**
- **Controler:** USB PHY integrat în ESP32-C6
- **Protecții:**
  - ESD: USBLC6-2SC6Y (8kV IEC61000-4-2)
  - Current limit: Polyfuse 500mA

**Funcționalități:**
1. Încărcare baterie
2. Serial Console (CDC-ACM)
3. Update firmware (DFU mode)

#### 4.2 Conector Qwiic
**Aplicații:**
- Conectare senzori adiționali
- Debug I²C bus
- Extensii custom

## 🔌 Mapare Pinuri ESP32-C6

| Pin ESP32-C6 | Componentă / Semnal | Motivul Alegerii |
|--------------|----------------------|------------------|
| **GPIO1 (SDA)** | Magistrală I²C (BME680, MAX17048, DS3231) | Permite comunicarea simultană cu multiple dispozitive prin protocol standard |
| **GPIO2 (SCL)** | Semnal de sincronizare I²C | Asigură temporizarea corectă a transferurilor pe magistrala shared I²C |
| **GPIO5** | SPI MISO (E-Paper) | Facilitatează recepția datelor de stare de la display |
| **GPIO6** | SPI MOSI (E-Paper) | Canal dedicat pentru transmiterea imaginilor către ecran |
| **GPIO7** | SPI CLK (E-Paper) | Generează semnalul de ceas pentru sincronizarea datelor SPI |
| **GPIO8** | SPI CS (E-Paper) | Selectează exclusiv display-ul în configurații multi-slave |
| **GPIO9** | E-Paper DC | Determină dacă transferul conține date sau comenzi |
| **GPIO10** | E-Paper RST | Permite resetarea hardware a display-ului în caz de eroare |
| **GPIO11** | E-Paper BUSY | Monitorizează starea de ocupat pentru sincronizare fără polling |
| **GPIO12** | BUTTON_BOOT | Configurat special pentru intrare în modul de programare |
| **GPIO13** | BUTTON_RESET | Asigură resetarea controlată a sistemului |
| **GPIO14** | BUTTON_USER | Permite interacțiunea utilizatorului cu meniul principal |
| **GPIO15** | MAX17048 ALERT | Semnalează stări critice ale bateriei prin interrupt |
| **GPIO16** | USB D+ | Implementare directă a fizicului USB conform specificației |
| **GPIO17** | USB D- | Pereche diferențială obligatorie pentru comunicarea USB |
| **GPIO18** | STATUS_LED | Oferă feedback vizual despre starea sistemului |
| **GPIO19** | SD Card CS | Selectează cardul SD în arhitectura SPI shared |
| **GPIO20** | SD Card MISO | Primește date de la memoria externă |
| **GPIO21** | SD Card MOSI | Transmite comenzi și date către cardul SD |
| **GPIO4** | SD Card CLK | Asigură sincronizarea transferurilor SPI către/storage |
