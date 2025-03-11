# momo

#!/bin/bash

# Vérifier si une adresse IP est passée en argument
if [ -z "$1" ]; then
    echo "Usage: $0 <adresse_ip>"
    exit 1
fi

# Adresse IP fournie en argument
IP="$1"

# Vérification de la connectivité avec ping (3 paquets, timeout 2s)
ping -c 3 -W 2 "$IP" > /dev/null 2>&1

# Vérification du statut de la commande ping
if [ $? -eq 0 ]; then
    echo "Connexion réussie à $IP"
else
    echo "Échec de la connexion à $IP"
fi
