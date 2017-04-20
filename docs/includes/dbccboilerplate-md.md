Suchen nach einem Hardwarefehler. Führen Sie eine Hardwarediagnose aus, und beheben Sie mögliche Probleme. Prüfen Sie zudem die Windows-System- und -Anwendungsprotokolle sowie das SQL Server-Fehlerprotokoll, um anzuzeigen, ob der Fehler in Folge eines Hardwarefehlers aufgetreten ist. Beheben Sie alle durch die Hardware bedingten Probleme, die in den Protokollen enthalten sind.

Lagern Sie verschiedene Hardwarekomponenten aus, um das Problem zu isolieren, falls Beschädigungsprobleme bei permanenten Daten auftreten. Stellen Sie sicher, dass beim System der Schreibcache auf dem Datenträgercontroller nicht aktiviert ist. Wenden Sie sich an Ihren Hardwarehersteller, falls Sie beim Schreibcache das Problem vermuten.

Letztendlich kann es vorteilhaft sein, wenn Sie zu einem neuen Hardwaresystem wechseln. Der Wechsel kann die Neuformatierung der Laufwerke und eine Neuinstallation des Betriebssystems beinhalten.

Wiederherstellen aus einer Sicherung. Stellen Sie die Datenbank von der Sicherung wieder her, wenn das Problem nicht durch die Hardware bedingt und eine fehlerfreie Sicherung verfügbar ist.

Ausführen von DBCC CHECKDB. Führen Sie DBCC CHECKDB ohne eine REPAIR-Klausel aus, um das Ausmaß der Beschädigung festzustellen, falls keine fehlerfreie Sicherung verfügbar ist. DBCC CHECKDB empfiehlt die Verwendung einer REPAIR-Klausel. Führen Sie dann DBCC CHECKDB mit der entsprechenden REPAIR-Klausel aus, um die Beschädigung zu reparieren.

> **ALERT-Tag wird nicht unterstützt!!!!**
> **TR-Tag wird nicht unterstützt!!!!**
> **TR-Tag wird nicht unterstützt!!!!**

Wenn DBCC CHECKDB mit einer der REPAIR-Klauseln ausgeführt wird und das Problem nicht behebt, wenden Sie sich an Ihren primären Unterstützungsanbieter.

