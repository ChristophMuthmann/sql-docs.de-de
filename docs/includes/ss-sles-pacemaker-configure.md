1. **Erstellen Sie auf beiden Clusterknoten eine Datei zum Speichern von Benutzername und Kennwort für SQL Server für die Pacemaker-Anmeldung**. Der folgende Code erstellt und füllt diese Tabelle:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **Alle Clusterknoten müssen in der Lage sein, über SSH aufeinander zugreifen**. Tools wie „hb_report“ oder „crm_report“ (zur Problembehandlung) und Hawk's History Explorer erfordern kennwortlosen SSH-Zugriff zwischen den Knoten, andernfalls können sie nur Daten vom aktuellen Knoten sammeln. Falls Sie keinen nicht-standardmäßigen SSH-Port verwenden, nutzen Sie die Option „-X“ (siehe Hauptseite). Wenn Ihr SSH-Port z.B. 3479 ist, rufen Sie hb_report mit Folgendem auf:

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    Weitere Informationen finden Sie unter [System Requirements and Recommendations in the SUSE documentation (Systemanforderungen und Empfehlungen in der SUSE-Dokumentation)](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html).

3. **Installieren Sie die Erweiterung für hohe Verfügbarkeit**. Um die Erweiterung zu installieren, befolgen Sie die Schritte im folgenden SUSE-Thema:
    
    [Installation and Setup Quick Start (Installation und Setup – Schnellstart)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **Installieren Sie den FCI-Ressourcenagent für SQL Server**. Führen Sie die folgenden Befehle auf beiden Knoten aus:

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **Richten Sie den ersten Knoten automatisch ein**. Im nächsten Schritt wird ein ausgeführter Cluster mit einem Noten durch Konfigurieren des ersten Knotens, SLES1, eingerichtet. Befolgen Sie den Anweisungen im SUSE-Thema [Setting Up the First Node (Einrichten des ersten Knotens)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node).

    Abschließend überprüfen Sie den Status des Clusters mit `crm status`:
    ```bash
    crm status
    ```

    Es sollte angezeigt werden, dass ein Knoten, SLES1, konfiguriert wurde.

6. **Hinzufügen von Knoten zu einem vorhandenen Cluster**. Als Nächstes fügen Sie den SLES2-Knoten dem Cluster hinzu. Befolgen Sie den Anweisungen im SUSE-Thema [Adding the Second Node (Hinzufügen des zweiten Knotens)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node).
    
    Abschließend überprüfen Sie den Status des Clusters mit **crm status**. Wenn Sie einen zweiten Knoten erfolgreich hinzugefügt haben, sieht die Ausgabe ähnlich der folgenden aus:
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** ist die virtuelle IP-Clusterressource, die während der anfänglichen Einrichtung des Clusters mit einem Knoten konfiguriert wird.

7.    **Vorgehensweisen zum Entfernen**. Wenn Sie einen Knoten aus dem Cluster entfernen möchten, verwenden Sie das Bootstrap-Skript **ha-cluster-remove**. Weitere Informationen finden Sie unter [Overview of the Bootstrap Scripts (Übersicht über die Bootstrap-Skripts)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap).  

