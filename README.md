
# IOT Simon Game 🎮

**Projet réalisé par Yarkin Oner et Matheo Maussant** 👨‍💻👨‍💻

Un jeu **Simon** basé sur ESP32, contrôlé par des boutons et des LEDs, avec notifications sonores via un buzzer et intégration **IoT** pour suivi de scores via MQTT.

---

## Table des matières 📚

- [Description](#description)  
- [Fonctionnalités](#fonctionnalités)  
- [Matériel requis](#matériel-requis)  
- [Logiciel requis](#logiciel-requis)  
- [Installation](#installation)  
- [Configuration](#configuration)  
- [Utilisation](#utilisation)  
- [Structure du projet](#structure-du-projet)  
- [Licence](#licence)  

---

## Description 📝

Ce projet permet de jouer à Simon sur un ESP32 avec :  

- 4 LEDs 💡 indiquant la séquence  
- 4 boutons 🔘 pour reproduire la séquence  
- Un buzzer 🔔 pour les signaux sonores  
- Connexion Wi-Fi 📶 et MQTT pour envoyer les scores à un serveur  
- Appairage simple via MQTT pour associer un utilisateur 👤  

Le jeu suit la séquence classique de Simon et augmente la longueur à chaque round réussi.

---

## Fonctionnalités ⚡

- Génération aléatoire de séquences de LED 🎲  
- Détection des boutons avec anti-rebond 🛡️  
- Indication sonore pour chaque action 🔔 (bonne réponse, début de jeu, fin de jeu, Wi-Fi/MQTT connecté)  
- Transmission du score via MQTT à un serveur distant 🌐  
- Appairage Wi-Fi dynamique via MQTT 🤝  

---

## Matériel requis 🛠️

- ESP32 (n’importe quel modèle avec suffisamment de GPIO) 🖥️  
- 4 LEDs 💡 + résistances  
- 4 boutons poussoirs 🔘  
- Buzzer (PWM) 🔔  
- Câbles de connexion 🔌  
- Alimentation USB pour ESP32 🔋  

---

## Logiciel requis 💾

- [VSCode](https://code.visualstudio.com/)  
- [PlatformIO IDE](https://platformio.org/)  
- Bibliothèques Arduino :  
  - `WiFi` 📶  
  - `PubSubClient` 🌐  
  - `ArduinoJson` 📝  

---

## Installation 🚀

1. Cloner le dépôt :  
   ```bash
   git clone https://github.com/tonusername/IOT_SIMON_GAME.git
   cd IOT_SIMON_GAME
   ```
2. Ouvrir le projet dans **VSCode + PlatformIO**  
3. Vérifier que la carte ESP32 est sélectionnée dans `platformio.ini` :  
   ```ini
   [env:esp32dev]
   platform = espressif32
   board = esp32dev
   framework = arduino
   ```
4. Compiler et téléverser sur l’ESP32 via PlatformIO 💻  

---

## Configuration ⚙️

Dans `src/main.cpp` :  

- **Wi-Fi par défaut** :  
  ```cpp
  const char* DEFAULT_WIFI_SSID = "NomDuWifi";
  const char* DEFAULT_WIFI_PASSWORD = "MotDePasseWifi";
  ```
- **Serveur MQTT** :  
  ```cpp
  const char* MQTT_SERVER = "10.95.140.175"; // Adresse IP du MQTT
  const uint16_t MQTT_PORT = 1883;           // Port du MQTT
  ```
- **Pins** : LEDs, boutons et buzzer configurables via les tableaux `ledPins[]` et `buttonPins[]` 🔌  

---

## Utilisation 🎯

1. Brancher et alimenter l’ESP32 🔋  
2. Connecter le ESP32 au Wi-Fi 📶  
3. Le jeu démarre automatiquement après 5 secondes ⏱️  
4. Suivre la séquence des LEDs 💡 et appuyer sur les boutons 🔘 correspondants  
5. Le buzzer 🔔 indique les bonnes réponses, les tours gagnés et la fin du jeu 💥  
6. Les scores sont publiés sur MQTT sur le topic `simon/scores` 🏆  

**Appairage utilisateur** 🤝 :  
- Envoyer un message MQTT sur le topic `simon/pair` avec :  
  ```json
  {
    "ssid": "MonSSID",
    "password": "MonMotDePasse",
    "username": "NomUtilisateur"
  }
  ```
- L’ESP32 se connectera au Wi-Fi fourni et confirmera via `simon/pair/ack` ✅  

---

## Structure du projet 🗂️

```
IOT_SIMON_GAME/
├── include/            # Headers personnalisés 📄
├── lib/                # Bibliothèques additionnelles 📦
├── src/
│   └── main.cpp        # Code principal 💻
├── test/               # Tests unitaires 🧪
├── platformio.ini      # Configuration PlatformIO ⚙️
└── README.md           # Ce fichier 📝
```

---

## Licence 📝

Ce projet est open-source sous licence MIT 🆓
