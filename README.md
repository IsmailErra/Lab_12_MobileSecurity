# LAB 12 : Bypass de la Détection de Root Android

## Objectif
Démontrer la vulnérabilité des mécanismes de détection de root côté client sur Android, en utilisant l'instrumentation dynamique via Frida et le framework Medusa.

---

## 1. Préparation de l'environnement

Afin d'interagir avec l'application cible, l'environnement de test (Frida et ADB) doit être opérationnel sur la machine hôte et sur l'émulateur.

**Action :** Vérification des installations locales et de la communication avec l'appareil.
![Preuve d'installation](screenshots/preuve_installation.png)

**Action :** Lancement de `frida-server` sur l'appareil avec privilèges root et listage des processus pour validation.
![Déploiement Frida](screenshots/deploiement_frida.png)

---

## 2. Bypass via le framework Medusa (Méthode principale)

L'outil Medusa permet d'automatiser l'injection de scripts de contournement sans nécessiter le développement manuel de hooks.

**Action :** Lancement de Medusa, sélection du module `universal_root_detection_bypass` et injection au démarrage (spawn) de l'application Diva.
![Console Medusa Bypass](screenshots/medusa_console.png)

---

## 3. Bypass via Script Frida (Alternative)

En cas de défaillance du module automatisé, un script JavaScript spécifique a été injecté pour intercepter manuellement les API Java (ex: `Build.TAGS`, `File.exists()`).

**Action :** Injection du script `bypass_root.js` directement dans le processus actif via la commande `frida -U "Diva" -l bypass_root.js`.
![Console Frida Custom](screenshots/frida_console.png)

---

## 4. Validation du Contournement

Une fois les hooks appliqués (via Medusa ou le script manuel), l'application cible est incapable d'identifier l'état compromis de l'appareil.

**Action :** Exécution de la vérification de root dans l'application Diva.
![Résultat Bypass](screenshots/app_bypassed.png)

---

## Conclusion
Ce laboratoire prouve qu'une validation de sécurité (comme la détection de root ou de jailbreak) effectuée exclusivement sur le terminal client n'est pas fiable. L'instrumentation dynamique permet de modifier à la volée les réponses du système d'exploitation et de contourner facilement ces restrictions.
