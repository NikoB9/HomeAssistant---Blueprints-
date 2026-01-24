# HomeAssistant---Blueprints

Collection de blueprints pour Home Assistant fournis par @NikoB9.

Ce dépôt contient actuellement 2 blueprints prêts à l'emploi : un contrôleur pour télécommande IKEA STYRBAR/TRÅDFRI via ZHA, et un blueprint pour synchroniser plusieurs interrupteurs/lumières.

---

## Blueprints disponibles

### 1) ZHA – IKEA STYRBAR / TRÅDFRI — Lumière + Température
- Fichier : `STYRBAR-Lights-Controller`
- Description courte :
  Contrôle générique d'une lumière (ou groupe) avec une télécommande IKEA STYRBAR / TRÅDFRI via l'intégration ZHA.
- Fonctionnalités principales :
  - Appui court : incrémente / décrémente la luminosité par pas configurable.
  - Appui long : variation progressive (répétée) tant que le bouton est maintenu.
  - Contrôle de la température de couleur avec les flèches gauche/droite.
  - Optionnel : allume un interrupteur d’alimentation (`power_switch`) si la lumière est hors tension avant d'appliquer les changements.
  - Paramètres configurables : pas de luminosité (court/long), pas de température couleur, intervalle pour l'appui long.
- Détails techniques :
  - Domain : automation
  - Mode : restart
  - Utilise des triggers device ZHA pour short_press, long_press, long_release.
- Ajout rapide (import via URL raw) :  
  [![Ajouter dans Home Assistant](https://img.shields.io/badge/Ajouter%20dans%20Home%20Assistant-Importer-blue?style=for-the-badge&logo=home-assistant)](https://raw.githubusercontent.com/NikoB9/HomeAssistant---Blueprints/main/STYRBAR-Lights-Controller)

---

### 2) Synchronize multiple Switches/Lights
- Fichier : `Multiple-switches`
- Description courte :
  Synchronise plusieurs entités (switch ou light) pour qu'elles agissent en unisson.
- Fonctionnalités principales :
  - Empêche la désynchronisation en envoyant l'action (on/off) aux autres entités lorsque l'une change d'état.
  - Appels de service parallèles pour rapidité.
  - Protection contre double-press / rebond (debounce configurable en ms).
  - Optimisé pour Zigbee (ZHA) et fonctionne aussi avec d'autres intégrations (ex. Tuya).
- Détails techniques :
  - Domain : automation
  - Mode : restart (max_exceeded: silent)
  - Entrées : liste d'entités à synchroniser, debounce (ms)
- Ajout rapide (import via URL raw) :  
  [![Ajouter dans Home Assistant](https://img.shields.io/badge/Ajouter%20dans%20Home%20Assistant-Importer-blue?style=for-the-badge&logo=home-assistant)](https://raw.githubusercontent.com/NikoB9/HomeAssistant---Blueprints/main/Multiple-switches)

---

## Instructions d'installation

Méthode A — Importer depuis l'URL raw (recommandée)
1. Ouvrir Home Assistant.
2. Aller dans Configuration → Automations & Scenes → Blueprints.
3. Cliquer sur "Import Blueprint".
4. Coller l'URL raw du blueprint :
   - STYRBAR : `https://raw.githubusercontent.com/NikoB9/HomeAssistant---Blueprints/main/STYRBAR-Lights-Controller`
   - Multiple-switches : `https://raw.githubusercontent.com/NikoB9/HomeAssistant---Blueprints/main/Multiple-switches`
5. Vérifier et importer. Ensuite créer une automatisation à partir du blueprint.

Méthode B — Copier localement
1. Créer un dossier dans ta configuration Home Assistant, par exemple :
   `config/blueprints/automation/nikob9/`
2. Copier le contenu des fichiers dans :
   - `config/blueprints/automation/nikob9/styrbar_lights_controller.yaml`
   - `config/blueprints/automation/nikob9/multiple_switches.yaml`
3. Dans Home Assistant → Blueprints, cliquer sur "Refresh" (ou recharger) et utiliser les blueprints importés.

Remarques :
- Si ton instance utilise une autre branche que `main`, remplace `main` dans les URLs raw par le nom de la branche.
- Les fichiers fournis contiennent les inputs (`remote_device`, `light_target`, `power_switch`, etc.) — configure les champs lors de la création d'une automatisation depuis le blueprint.

---

## Exemple d'en-tête YAML (extrait)
Voici le type d'en‑tête que les blueprints contiennent (utile pour documentation ou pour vérifier les métadonnées) :

```yaml
blueprint:
  name: ZHA – IKEA STYRBAR / TRÅDFRI – Lumière + Température
  description: >
    Contrôle générique d'une lumière (ou groupe) avec une télécommande IKEA STYRBAR/TRÅDFRI via ZHA.
  domain: automation
  input:
    remote_device:
      name: Télécommande IKEA (ZHA)
      selector:
        device:
          integration: zha
    light_target:
      name: Lumière ou groupe à contrôler
      selector:
        entity:
          domain: light
    ...
```

---

## Contribuer
- PRs bienvenues : ajoute un blueprint, améliore la documentation ou corrige un bug.
- Avant de soumettre : tester le blueprint sur une instance de développement et respecter la structure YAML pour les blueprints Home Assistant.
- Signale les bugs via les Issues (décrire l'environnement : version HA, intégration utilisée, logs).

---

## Licence
Ce projet est sous licence Apache-2.0 — voir le fichier LICENSE.

---

## Notes
- J'ai laissé les noms de fichiers tels qu'ils sont dans le repo (sans extension). Si tu veux que je renomme les fichiers pour ajouter `.yaml`, je peux aussi le faire dans un commit séparé.