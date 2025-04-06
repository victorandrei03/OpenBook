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
| **Senzoare** | BME680 | Senzor ambiental (temperatură, umiditate, presiune, VOC) |
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
