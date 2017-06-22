1. **Erstellen Sie auf allen Servern mit SQL Server eine Server-Anmeldung für Pacemaker**. Die folgende Transact-SQL erstellt eine Anmeldung:

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

   Alternativ können Sie die Berechtigungen detaillierter festlegen. Für die Pacemaker-Anmeldung sind die Berechtigungen ALTER, CONTROL und VIEW DEFINITION erforderlich. Weitere Informationen finden Sie unter [Erteilen von Verfügbarkeitsgruppenberechtigungen mit GRANT (Transact-SQL)](http://msdn.microsoft.com/library/hh968934.aspx).

   Die folgende Transact-SQL gewährt nur die erforderliche Berechtigung für die Pacemaker-Anmeldung. In der untenstehenden Anweisung ist „ag1“ der Name der Verfügbarkeitsgruppe, die als Clusterressource hinzugefügt wird.

   ```Transact-SQL
   GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO pacemakerLogin
   ```

1. **Speichern Sie auf allen Servern mit SQL Server die Anmeldeinformationen für die SQL Server-Anmeldung**.

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
