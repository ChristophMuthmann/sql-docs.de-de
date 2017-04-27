
3. Öffnen Sie auf beiden Clusterknoten die Pacemaker-Firewallports. Führen Sie zum Öffnen dieser Ports mit `firewalld` folgenden Befehl aus:

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

   

2. Legen Sie das Kennwort für den Standardbenutzer fest, der beim Installieren von Pacemaker und Corosync-Paketen erstellt wird. Verwenden Sie auf beiden Knoten dasselbe Kennwort. 

   ```bash
   sudo passwd hacluster
   ```

   

3. Aktivieren und starten Sie den `pcsd`-Dienst und Pacemaker. So können Knoten dem Cluster nach dem Neustart erneut beitreten. Führen Sie den folgenden Befehl auf beiden Knoten aus.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Erstellen Sie den Cluster. Führen Sie den folgenden Befehl aus, um den Cluster zu erstellen:

   ```bash
   sudo pcs cluster auth <nodeName1> <nodeName2…> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <nodeName1> <nodeName2…> 
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >Wenn Sie vorher einen Cluster auf denselben Knoten konfiguriert haben, müssen Sie die Option „--force“ verwenden, wenn Sie „pcs cluster setup“ ausführen. Beachten Sie, dass dies der Ausführung von „pcs cluster destroy“ entspricht, und der Peacemaker-Dienst muss erneut mithilfe von „sudo systemctl enable pacemaker“ aktiviert werden.

5. Installieren Sie den SQL Server-Ressourcenagent für SQL Server. Führen Sie die folgenden Befehle auf beiden Knoten aus. 

   ```bash
   sudo yum install mssql-server-ha
   ```
