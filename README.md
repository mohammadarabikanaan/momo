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



# Fonction pour scanner les ports ouverts
detect_open_ports() {
    local ip="$1"
    local start_port=1
    local end_port=1024  # Plage de ports à tester

    echo "Scanning ports on $ip..."
    
    for ((port=$start_port; port<=$end_port; port++)); do
        nc -z -v -w1 "$ip" "$port" 2>&1 | grep -q "succeeded" && echo "Port $port is open"
    done
}

# Vérification des arguments
if [ "$#" -ne 1 ]; then
    echo "Usage: $0 <IP_ADDRESS>"
    exit 1
fi

# Appel de la fonction detect_open_ports avec l'IP fournie
detect_open_ports "$1"
