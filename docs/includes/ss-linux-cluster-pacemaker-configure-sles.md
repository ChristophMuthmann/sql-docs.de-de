2. Erstellen Sie auf allen Clusterknoten eine Datei zum Speichern von Benutzername und Kennwort für SQL Server für die Pacemaker-Anmeldung. Der folgende Code erstellt und füllt diese Tabelle:

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
   sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. Öffnen Sie auf allen Clusterknoten die Pacemaker-Firewallports. Führen Sie zum Öffnen dieser Ports mit `firewalld` folgenden Befehl aus:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Wenn Sie eine andere Firewall verwenden, in die keine Konfiguration mit hoher Verfügbarkeit integriert ist, müssen die folgenden Ports geöffnet werden, damit Pacemaker mit anderen Knoten im Cluster kommunizieren kann:
   >
   > * TCP: Ports 2224, 3121, 21064
   > * UDP: Port 5405

1. Installieren Sie Pacemaker-Pakete auf jedem Knoten.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. Legen Sie das Kennwort für den Standardbenutzer fest, der beim Installieren von Pacemaker und Corosync-Paketen erstellt wird. Verwenden Sie auf allen Knoten dasselbe Kennwort. 

   ```bash
   sudo passwd hacluster
   ```

   

3. Aktivieren und starten Sie den `pcsd`-Dienst und Pacemaker. So können Knoten dem Cluster nach dem Neustart erneut beitreten. Führen Sie den folgenden Befehl auf allen Knoten aus.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Installieren Sie den FCI-Ressourcenagent für SQL Server. Führen Sie die folgenden Befehle auf allen Knoten aus. 

   ```bash
   sudo yum install mssql-server-ha
   ```
