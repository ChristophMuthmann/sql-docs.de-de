Das **SA**-Konto ist ein Systemadministrator auf der SQL Server-Instanz, der beim Setup erstellt wird. Nach dem Erstellen Ihres SQL Server-Containers wird die von Ihnen festgelegte `MSSQL_SA_PASSWORD` Umgebungsvariable sichtbar, wenn Sie sie in dem Container ausführen`echo $MSSQL_SA_PASSWORD`. Ändern Sie aus Sicherheitsgründen ihr SA-Kennwort.

1. Wählen Sie ein sicheres Kennwort für den SA-Benutzer aus.

1. Verwenden Sie `docker exec` in Transact-SQL **sqlcmd** zum Ausführen und Ändern des Kennworts. Ersetzen Sie `<YourStrong!Passw0rd>` und `<YourNewStrong!Passw0rd>` mit Ihren eigenen Kennwortwerten.

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
