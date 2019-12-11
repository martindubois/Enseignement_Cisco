
    Autheur  Martin Dubois, ing.
    Produit  Enseignement/Cisco
    Fichier  ExempleComplet/README.md

===== Serveur-PT Admin ======================================================

Ce serveur utilise l'adresse statique 192.168.10.20 et expose un service
HTTP. Il est configure pour utiliser le serveur principal comme DNS.

===== Serveur-PT Google.ca ==================================================

Ce serveur utilise l'adresse statique 8.8.8.8 et expose un service DNS et un
service HTTP.

La configuration du service DNS ne contient que l'adresse de google.ca.

La configuration n'inclue pas de routeur par defaut car pour se serveur,
tous les autres ordinateurs du réseau sont sur un seule réseau local. La
magie du NAT rends les ordinateurs et serveurs invisible pour lui.

===== Serveur-PT Principal ==================================================

Ce serveur utilise l'adresse statique 192.168.10.10 et expose un service DNS
et un service HTTP. Il est configure pour utiliser le serveur google.ca comme
DNS.

La configuration du service DNS contient l'adresse de google.ca car le
simulateur du service DNS ne retransmet pas les requetes qui ne sont pas
resolues localement vers le serveur DNS utilise par le serveur.

===== Tests =================================================================

    [ ] Laptop-PT Admin (20)
        - Command prompt
            ipconfig
            ping 192.168.10.10      Destination host unreachable
            ping 192.168.20.1
            ping 192.168.21.2       Request timed out
            ping 192.168.30.2       Request timed out
            ping admin              Adresse resolue, Destination host unreachable
        - Navigateur
            admin
            google.ca
            principal
    [ ] Laptop-PT Admin (21)
        - Command prompt
            ipconfig
            ping 192.168.10.20      Request timed out
            ping 192.168.21.1
            ping admin              Adresse resolue, Request timed out
        - Navigateur
            admin
            google.ca
            principal
    [ ] Laptop-PT Prod (30)
        - Command prompt
            ipconfig
            ping 192.168.10.10      Request timed out
            ping 192.168.30.1
            ping principal          Adresse resolue, Request timed out
        - Navigateur
            admin                   Request timeout
            google.ca
            principal
    [ ] Serveur-PT Admin
        - Command prompt
            ipconfig
            ping 192.168.10.1
            ping 192.168.10.20
            ping 8.8.8.8            Request timed out
            ping admin
            ping google.ca          Adresse reseolue, Request timed out
            ping principal
        - Navigateur
            admin
            google                  Request timeout
            principal
    [ ] Serveur-PT Principal
        - Command prompt
            ipconfig
            ping 192.168.10.1
            ping 192.168.10.10
            ping 192.168.20.2       Request timed out
            ping admin              could not find host
            ping google.ca          Adresse resolue, Request timed out
            ping principal          could not find host
        - Navigateur
            admin                   Host Name Unresolved
            google.ca               Request timeout
            principal               Host Name Unresolved
