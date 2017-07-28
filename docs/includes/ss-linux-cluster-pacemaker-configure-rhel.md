3. Öffnen Sie auf allen Clusterknoten die Schrittmacher Firewallports. Führen Sie zum Öffnen dieser Ports mit `firewalld` folgenden Befehl aus:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Wenn die Firewall nicht über eine integrierte Konfiguration mit hoher Verfügbarkeit verfügt, öffnen Sie die folgenden Ports für Pacemaker.
   >
   > * TCP: Ports 2224, 3121, 21064
   > * UDP: Port 5405

1. Installieren Sie Pacemaker-Pakete auf allen Knoten.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

2. Legen Sie das Kennwort für den Standardbenutzer fest, der beim Installieren von Pacemaker und Corosync-Paketen erstellt wird. Verwenden Sie das Kennwort auf allen Knoten. 

   ```bash
   sudo passwd hacluster
   ```

3. Aktivieren und starten Sie den `pcsd`-Dienst und Pacemaker, um den Knoten nach dem Neustart einen erneuten Beitritt zum Cluster zu erlauben. Führen Sie den folgenden Befehl auf allen Knoten.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Erstellen Sie den Cluster. Führen Sie den folgenden Befehl aus, um den Cluster zu erstellen:

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >Wenn Sie vorher einen Cluster auf denselben Knoten konfiguriert haben, müssen Sie die Option `--force` verwenden, wenn Sie `pcs cluster setup` ausführen. Diese Option entspricht der Ausführung von `pcs cluster destroy`. Führen Sie `sudo systemctl enable pacemaker` aus, um Pacemaker erneut zu aktivieren.

5. Installieren Sie den SQL Server-Ressourcenagent für SQL Server. Führen Sie die folgenden Befehle auf allen Knoten. 

   ```bash
   sudo yum install mssql-server-ha
   ```
