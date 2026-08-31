# Solar-Powered ESP32 Weather Station via LoRa — Research Compilation

> Curated resources and BOM for a terrace-mounted ESP32 weather station communicating via LoRa to a local gateway. Focus on reliability and battery life.

---

## 1. ESP32 Deep Sleep & Power Optimization

These cover the core techniques for getting months of battery life: timer wake-ups, RTC memory, ULP coprocessor, and power budgeting.

- [**ESP32 Deep Sleep: Ultra-Low Power IoT Sensor Node Build** — Zbotic (2026)](https://zbotic.in/esp32-deep-sleep-ultra-low-power-iot-sensor-node-build/) — Comprehensive guide covering wake sources, RTC memory, sensor wiring, firmware, and real battery life estimation for Indian deployment scenarios.
- [**Power Management and Deep Sleep | SiliconWit**](https://siliconwit.com/education/embedded-programming-esp32/power-management-deep-sleep/) — Covers deep sleep modes, ULP coprocessor programming, RTC memory persistence, wake sources, and power budgeting. Specifically mentions solar-ready weather node optimization.
- [**ESP32 Deep Sleep Battery Sensors (2026 Guide) — Esp32.co.uk**](https://esp32.co.uk/esp32-battery-powered-sensors-deep-sleep-low-power-design-guide/) — Explains why USB-powered designs fail on battery, ESPHome deep sleep config, ADC for battery monitoring, and practical low-power design patterns.
- [**ESP32 Deep Sleep Guide: Extend Battery from Days to Months | SolderHub**](https://solderhub.com/articles/esp32-deep-sleep-battery-life-guide) — Practical tips: RTC_DATA_ATTR usage, Serial.flush() before sleep, wake-on-timer vs GPIO.
- [**Deep Sleep Low Power Optimization on ESP32 Dev Boards** — ESP Boards Dev](https://www.espboards.dev/blog/esp32-power-optimisation/) — Covers light sleep vs deep sleep, sensor wake-up capabilities, and balancing responsiveness with power consumption.
- [**Low-Power-Arduino Sketch for a simple weather station using ESP32 with DeepSleep and BME280** — GitHub Gist](https://gist.github.com/Schm1tz1/d5f4d34492509611846862cfdc786b66) — Working sketch that wakes every N microseconds, reads sensors, transmits, sleeps. Good reference for the basic loop.

## 2. Solar Power & Battery Management

- [**Power ESP32/ESP8266 with Solar Panels and Battery | Random Nerd Tutorials**](https://randomnerdtutorials.com/power-esp32-esp8266-solar-panels-battery-level-monitoring/) — TP4056 charger, LiPo battery, level monitoring, caveats about load connections.
- [**Solar Power for ESP32: MPPT and Battery Charging Circuit** — Zbotic](https://zbotic.in/solar-power-for-esp32-mppt-and-battery-charging-circuit/) — TP4056 vs MPPT, 6V solar panel wiring, LiFePO4 vs LiPo considerations.
- [**Powering ESP32 with solar + LiFePO4 — Home Assistant Community**](https://community.home-assistant.io/t/powering-esp32-with-solar-lifepo4/744978) — Community discussion on LiFePO4 for outdoor use (better thermal stability vs LiPo).
- [**Best Solar Charging Modules for IoT (Buying Guide)** — Microcontrollers Lab (2026)](https://microcontrollerslab.com/best-solar-charging-modules-for-iot-buying-guide/) — Compares TP4056, BQ25570 energy harvester, dual-USB solar managers, and LiFePO4-matched chargers.
- [**Project: Solar Powered WiFi Weather Station V2.0 — Hackaday.io**](https://hackaday.io/project/165061/logs?sort=oldest) — Real build logs with TP4056, 18650, and solar panel. Good lessons learned from actual deployment.

## 3. LoRa Communication (ESP32 → Gateway)

- [**ESP32 LoRa without LoRaWAN: long-range sensors to your own cloud** — Nodrix](https://nodrix.live/guides/esp32-lora-gateway) — Covers point-to-point LoRa, duty-cycle limits, honest range expectations, and why skipping LoRaWAN is often the right choice for a custom setup.
- [**ESP32 LoRa Reliable Link** — GitHub (rusilveira)](https://github.com/rusilveira/esp32-lora-reliable-link) — Implements ACK, CRC16, and sequence control on top of LoRa for reliable delivery. Relevant for a beehive monitoring system (same pattern).
- [**ESP32 LoRa 1-CH Gateway** — SparkFun Learn](https://learn.sparkfun.com/tutorials/esp32-lora-1-ch-gateway-lorawan-and-the-things-network/all) — ESP32 LoRa 1-CH board as a gateway. Good for the server-side implementation.
- [**ESP32S3 LoRa: Setup, Range & Meshtastic** — Seeed Studio Blog](https://www.seeedstudio.com/blog/2026/05/26/esp32-lora-guide/) — 2026 overview of ESP32 LoRa capabilities, Meshtastic mesh networks, and practical range considerations.
- [**ESP32 LoRa Remote Sensor Node for Home Assistant** — Esp32.co.uk](https://esp32.co.uk/esp32-lora-remote-sensor-node-for-home-assistant-sx1276/) — Node and gateway design, MQTT topics, YAML sensors, and reliability tips for outdoor garden monitoring.

## 4. LoRa Module & Antenna Selection

- [**SX1262 vs SX1276: Which LoRa Module Is Better?** — Mozelectronics](https://mozelectronics.com/tutorials/sx1262-vs-sx1276-lora-module/) — SX1262 for new designs (better sensitivity, lower power); SX1276 if maintaining existing designs.
- [**LoRa Module: SX1276 vs SX1262 vs SX1280 Compared** — PCBSync](https://pcbsync.com/lora-module-comparison/) — Benchmarks, sensitivity, data rates, and when to use each module.
- [**SX1276 LoRa Module: Range, Sensitivity & Spreading Factor Guide** — Zbotic](https://zbotic.in/sx1276-lora-module-range-sensitivity-spreading-factor-guide/) — Realistic range expectations at +20 dBm, spreading factor tradeoffs, antenna height impact.
- [**LoRa RF Module Sensitivity Benchmarks: Side-by-Side Field Test** — IC Online](https://www.ic-online.com/blog/post/lora-rf-module-sensitivity-and-range-benchmarks-side-by-side-field-test-data-for-sx1262-vs-sx1276) — Field test data for SX1262 vs SX1276, emphasizing power supply, antenna, and protocol design.

## 5. Reliable Weather Sensors

### Environmental (Temp/Humidity/Pressure)
- [**BME280 vs BME680 vs BME688: Which Is Best?** — Esp32.co.uk](https://esp32.co.uk/bme280-vs-bme680-vs-bme688-which-is-best/) — BME280 for reliable temp/humidity/pressure at lowest power; BME680 adds VOC/air quality.
- [**BME280 & BME680 Environmental Sensors: Complete Tutorial** — PCBSync](https://pcbsync.com/bme280-bme680-environmental-sensors/) — Comparison, wiring, ESP32 code, and when to choose each.
- [**Adafruit BME680** — Adafruit](https://www.adafruit.com/product/3660) — Precision sensor with ±3% humidity, ±1 hPa pressure, ±1.0°C temp accuracy. Good reference for quality.

### Wind Speed & Direction
- [**Multi-sensor weather station with ESP32 under $100 — Botmonster Tech**](https://botmonster.com/smart-home/build-weather-station-esphome-wind-rain-uv-sensors/) — Uses **Davis 6410 anemometer** (industrial-grade) with ESPHome. Good reference for reliable wind measurement.
- [**ESP32 with an Anemometer: Measure Wind Speed** — Random Nerd Tutorials](https://randomnerdtutorials.com/esp32-anemometer-wind-speed-arduino/) — Wiring and Arduino code for reed-switch anemometers.
- [**ESP32 Weather Station** — Elektor Magazine](https://www.elektormagazine.com/labs/esp32-weather-station-180468) — Wind vane with resistor-based voltage divider, anemometer with reed switch. Published in Elektor = tested hardware.

### Rainfall
- [**DIY Weather Station With ESP32 — Instructables**](https://www.instructables.com/DIY-Weather-Station-With-ESP32/) — Covers tipping-bucket rain gauge integration with ESP32.

### UV Index
- [**VEML6075 UV Sensor** — Adafruit](https://www.adafruit.com/product/1493) — I2C UV index sensor, used in the Botmonster build referenced above.

## 6. End-to-End Projects & Reference Builds

- [**Build a Solar-Powered Weather Station with LoRa — balena Blog (2020)**](https://blog.balena.io/build-a-simple-solar-powered-weather-station-with-lora-the-things-network/) — Two-part series: solar weather station + LoRa + The Things Stack.
- [**LoRa Based Wireless Weather Station with Arduino & ESP32** — How2Electronics](https://how2electronics.com/lora-based-wireless-weather-station-with-arduino-esp32/) — ESP32 + LoRa-based wireless weather station architecture.
- [**bitrot-alpha/lora-weather-esp32 — GitHub**](https://github.com/bitrot-alpha/lora-weather-esp32) — Full open-source weather station: wind speed/direction, rainfall, environmental sensors with LoRa.
- [**How to Build a Smart Weather Station with Sensors? — Ampheo**](https://www.ampheo.com/blog/how-to-build-a-smart-weather-station-with-sensors) — Practical ESP32-based weather station covering temp, humidity, pressure, rainfall, wind.
- [**DIY LoRaWAN Weather Station for Large Acreage (2026 Guide)** — About Agri](https://aboutagri.com/diy-lorawan-weather-station-large-acreage/) — 2026 guide covering firmware, sensor selection, and large-distance deployments.

## 7. Books & Deep-Dive References

- **"Arduino Weather Projects"** by John Boxall — Covers sensor interfacing, data logging, and outdoor enclosures for weather monitoring.
- **"ESP32 Cookbook"** by Simon Monk — Practical recipes for ESP32 projects including sensors, sleep modes, and wireless communication.
- **"Making Sense of LoRa"** by Paul Borghstede — Dedicated LoRa/LoRaWAN primer: modulation, duty cycles, antenna design, network planning.
- **"IoT Cookbook"** by Simon Monk — Sections on low-power sensor design, solar power, and ESP32 deep sleep patterns.
- **ESP32 Technical Reference Manual** — [Espressif Official Docs](https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual.pdf) — The authoritative source on deep sleep modes, ULP, RTC peripherals, and power domains.

---

## Materials / BOM

### Core Electronics
| Component | Recommendation | Notes |
|---|---|---|
| **MCU** | ESP32-WROOM-32 or ESP32-C3 | ESP32 for Wi-Fi backup; ESP32-C3 for lower deep-sleep current (~6µA) |
| **LoRa Module** | SX1262 (e.g. Ra-02 module) | Better sensitivity (-165 dBm) and lower RX current vs SX1276 |
| **Environmental Sensor** | BME280 | Most reliable: ±1 hPa pressure, ±3% RH. Avoid cheap DHT11/DHT22 |
| **Wind Speed Sensor** | Reed-switch anemometer or Davis 6410 | Davis = industrial grade. Reed-switch = budget but reliable |
| **Wind Direction** | Potentiometer-based vane or magnetic compass (HMC5883L) | Potentiometer: simpler. HMC5883L: no moving parts |
| **Rain Gauge** | Tipping-bucket (e.g. DFRobot or PMS-G010) | Ensure it's mechanical, not IR-based (more reliable outdoors) |
| **UV Sensor** | VEML6075 (I2C) | For UV index measurement |
| **Solar Charger** | TP4056 module (with protection) | For 1S LiPo/18650. For LiFePO4: use a LiFePO4-matched charger |
| **Boost Converter** | MT3608 or AP64532 step-up | If ESP32 3.3V rail needs more current than battery provides directly |

### Power & Battery
| Component | Recommendation | Notes |
|---|---|---|
| **Battery** | 18650 Li-ion (2000-3500 mAh) or LiFePO4 18650 | LiFePO4 for outdoor thermal stability. 3500 mAh gives months of sleep cycles |
| **Solar Panel** | 6V 1-2W poly panel (e.g. 130x100mm) | Minimum ~200mA in good sun. Position facing south, tilted ~30° |
| **Fuse / Protection** | 2A resettable fuse on solar input | Protects against reverse current and shorts |
| **Voltage Divider** | 2x 100k resistors | For battery voltage monitoring via ESP32 ADC (pin 34/35) |

### Antenna & RF
| Component | Recommendation | Notes |
|---|---|---|
| **Antenna** | 868/915 MHz whip antenna (2.5 dBi) | SMA or IPEX connector depending on module. Use a mast, 1-2m above terrace railing |
| **LoRa Antenna Cable** | RG-316 low-loss coax | Keep cable runs <30cm between module and antenna |

### Mechanical & Enclosure
| Component | Recommendation | Notes |
|---|---|---|
| **Enclosure** | IP65 project box (e.g. RamPro or ABB) | Size ~150x100x70mm for sensors + electronics |
| **Sensor Mast** | Stainless steel or PVC pipe | Anemometer on top (40-60cm above enclosure), wind vane below |
| **Weather Shield** | Stevenson screen or equivalent | For BME280 — ventilated enclosure prevents solar heating of sensor |
| **Cable Glands** | IP68 cable glands | For sensor wires entering the enclosure |
| **Screws & Mounting** | 316 stainless steel | Marine-grade, terrace-mountable |

### Wiring & Misc
| Component | Notes |
|---|---|
| **Jumper wires / perfboard** | For prototype wiring |
| **Level shifter (optional)** | If using 5V sensors with 3.3V ESP32 |
| **Breadboard / PCB** | Prototype on breadboard, then solder to perfboard or design a PCB |
| **Heat shrink / waterproof tape** | For outdoor cable connections |

---

## Estimated Power Budget (Order of Magnitude)

| Mode | Current | Duration/day | mAh/day |
|---|---|---|---|
| Deep sleep | ~6µA (ESP32-C3) / ~20µA (WROOM) | 23h 55m | ~0.5 |
| Sensor read (BME280 I2C) | ~0.5mA | 5s | ~0.0 |
| LoRa TX (20dBm, 10s) | ~120mA | 10s per cycle | ~0.3 |
| MCU init/wake | ~50mA | 2s | ~0.0 |
| **Total per cycle** | | | **~0.8 mAh** |

With a 3500 mAh battery: **~4,300 cycles** at 1 cycle/hour = **~6 months** of autonomy. Add 30-50% margin for aging, cold, and cloudy days → **4-6 months real-world**.

---

*Compiled from community guides, official documentation, and open-source projects. Last updated August 2026.*
