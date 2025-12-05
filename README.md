# Définir le template pour l'envoi (optionnel mais recommandé)
template(name="remote_log_format" type="string" string="<%PRI%>%TIMESTAMP:::date-rfc3339% %HOSTNAME% %syslogtag%%msg%\n")

# Définir l'action d'envoi vers la Supervision (192.168.255.2:514)
action(
    type="omfwd"
    target="192.168.255.2"
    port="514"
    protocol="tcp"             # Utiliser TCP pour garantir l'ordre
    Template="remote_log_format"

    # PARAMÈTRES DE RÉSILIENCE POUR LA DIODE
    queue.filename="qMBlogs"           # Nom du fichier sur disque pour la file d'attente
    queue.maxdiskspace="1g"            # Taille max de la file d'attente (1 GB)
    queue.retryperiod="30"             # Tenter de renvoyer toutes les 30 secondes
    action.resumeRetryCount="-1"       # Retenter indéfiniment
)
