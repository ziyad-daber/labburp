# labburp
1. verification etat burpsuit
<img width="1359" height="714" alt="image" src="https://github.com/user-attachments/assets/e9b77bac-4061-4e7b-ad48-c4391bb45496" />
2.verification du proxy
<img width="1171" height="709" alt="image" src="https://github.com/user-attachments/assets/1bbd9f99-93cb-4962-8aae-5c857a94da39" />
3.Premier test : capturer du HTTP (validation de base)
<img width="1359" height="723" alt="image" src="https://github.com/user-attachments/assets/79d2b8b7-de3b-442c-8b6f-4c562e765cb5" />
4.Lire une requête comme un analyste
<img width="1025" height="319" alt="image" src="https://github.com/user-attachments/assets/48121c7c-ae82-4e61-b669-1cf455b46627" />
5.Interception contrôlée
<img width="1359" height="736" alt="image" src="https://github.com/user-attachments/assets/224c42b8-23d0-4e70-b084-83d7007bda9b" />

Fiche de trace — Burp Proxy ↔ Android Emulator (Lab)
Périmètre

Environnement : émulateur Android de laboratoire

Cible autorisée / test : Chrome uniquement

URL de test (proxy Burp) : http://192.168.137.1:8080/

Configuration

Date : 2026-02-20

Émulateur : Pixel 6

Burp Suite : Proxy listener sur 8080, bind All interfaces

Paramètres réseau utilisés

IP hôte / proxy : 192.168.137.1

Port proxy : 8080

Proxy configuré côté émulateur

Mode : Manual

Hostname : 192.168.137.1

Port : 8080

Preuves (observé)
1) Historique Burp (1–2 requêtes)

Requêtes visibles dans Proxy → HTTP history depuis l’émulateur.

Exemple observé :

GET http://192.168.137.1:8080/cert

2) Détails d’une requête (URL + headers)

Requête (extrait “Raw”) :

Méthode / chemin : GET /cert HTTP/1.1

Host : 192.168.137.1:8080

Headers notables :

Upgrade-Insecure-Requests: 1

User-Agent: ... Android 10 ... Chrome/133.0.0.0 Mobile ...

Referer: http://192.168.137.1:8080/

Accept-Language: en-US,en;q=0.9

Cookies : non observés sur cette requête

Authorization : non observé sur cette requête

Paramètres URL (query string) : non observés sur cette requête

Analyse
Données qui transitent (observé)

URL complète et headers HTTP visibles dans Burp.

Sur la requête /cert observée : pas de cookies, pas d’Authorization, pas de paramètres.

Risques potentiels (généraux, liés à ce type de transit)

Si des tests ultérieurs incluent des sessions/auth :

risque de fuite si tokens apparaissent en URL

risque si cookies de session non durcis côté serveur (Secure, HttpOnly, SameSite)

Recommandations défensives

Minimiser les données : éviter les identifiants/tokens en URL ; réduire les paramètres transmis.

Cookies côté serveur : activer Secure, HttpOnly, SameSite quand des sessions existent.

Bonnes pratiques Android : ne pas bypass TLS en dehors du lab ; garder une config réseau stricte en prod.

Remarque (qualité d’audit)

Séparer :

Observé : ce qui est prouvé par l’historique + headers

Supposé : non inclus ici (aucune hypothèse ajoutée)

Recommandé : actions défensives générales, applicables si auth/session apparaît
