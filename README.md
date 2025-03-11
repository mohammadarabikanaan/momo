#!/bin/bash

# Fonction pour vérifier la connectivité réseau
check_connectivity() {
    local ip_address=$1
    
    if ping -c 4 "$ip_address" > /dev/null 2>&1; then
        echo "Connexion réussie avec $ip_address"
    else
        echo "Échec de la connexion avec $ip_address"
    fi
}

# Vérifier si une adresse IP est fournie en argument
if [ -z "$1" ]; then
    echo "Usage: $0 <adresse_ip>"
    exit 1
fi

# Appel de la fonction avec l'adresse IP fournie
check_connectivity "$1"
