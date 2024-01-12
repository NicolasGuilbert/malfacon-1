## Cas  Orange OI
```mermaid
sequenceDiagram

  participant SCR
  participant SIGMAL
  participant DPBL
  participant NewMalfaçon-OWF-OI
  participant NewMalfaçon-OWF-OC
  participant SIGMALA toto
  participant UCI
  participant CONTRASTE

  SCR->>SIGMAL: Création  Signalisation
  SIGMAL->>NewMalfaçon-OWF-OI: Création Signalisation (post TT, status = CREATING)
  Note over SCR,SIGMAL: passage par sigmal ou à faire en direct ? point SAE
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OI: contrôle (verif si SIG en cours sur même elt d'infra et délai 24h, autres contrôles métier...), point OWF
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OC: Notification nouvelle signalisation S, status=CREATING
  SIGMAL->>NewMalfaçon-OWF-OI: Ajout de la photo (post Attachment (Sig,PJ))
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OI: contrôle PJ (photo)
  SIGMAL->>NewMalfaçon-OWF-OI: Passage à Acknowledged car complet (patch Sig, status=Acnolwledged)
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OI: contrôle si diffusable à l'OC (point OWF)
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OC: Notification sig, status=Acknowledged
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OI: démarrage du délai de reprise des 30 jours
  NewMalfaçon-OWF-OC->>NewMalfaçon-OWF-OC: contrôle conformité SIG (ex: 24h, contrat, date commande PTO etc... point OWF)
  NewMalfaçon-OWF-OC->>NewMalfaçon-OWF-OI: modification etat, status = In Progress
  NewMalfaçon-OWF-OC->>SIGMALA: notif SIG état= In Progress
  Note over NewMalfaçon-OWF-OC,SIGMALA: il faut attendre 24h pour analyser pour être sûr d'avoir la vue complète sur l'élément d'infra : consigne métier ?
  UCI->>SIGMALA: Analyse technique de la SIG et décision de contestation
  SIGMALA->>NewMalfaçon-OWF-OC: contestation de la SIG, status= Pending, statusCR= contestation
  NewMalfaçon-OWF-OC->>NewMalfaçon-OWF-OC: contrôle conformité contestation (point OWF)
  NewMalfaçon-OWF-OC->>NewMalfaçon-OWF-OI: contestation de la SIG, status= Pending, statusCR= contestation
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OI: verif conformité contestation (point OWF)
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OI: arret compteur de resolution OC, démarrage délai réponse OI
  NewMalfaçon-OWF-OI->>SIGMAL: notif de la contestation
  DPBL->>SIGMAL: analyse de la contestation, et décision de rejet
  SIGMAL->>NewMalfaçon-OWF-OI: rejet de la contestation de la SIG, status= In Progress, statusCR= contestation rejected
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OI: contrôle conformité rejet contestation (point OWF)
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OI: arret compteur de réponse OI, redémarrage compteur de résolution OC
  NewMalfaçon-OWF-OI->>NewMalfaçon-OWF-OC: notif status=In Progress, SR=contestation rejected
  NewMalfaçon-OWF-OC->>NewMalfaçon-OWF-OC: contrôle conformité rejet contestation (point OWF)
  NewMalfaçon-OWF-OC->>Sigmala: notif status=In Progress, SR=contestation rejected




  ```



