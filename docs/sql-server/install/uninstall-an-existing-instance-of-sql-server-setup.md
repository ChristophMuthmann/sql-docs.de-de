---
title: "Deinstallieren einer vorhandenen SQL Server-Instanz (Setup) | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Entfernen von Instanzen von SQL Server"
  - "Deinstallieren von Instanzen von SQL Server"
  - "Entfernen von SQL Server"
  - "Instanzen von SQL Server, deinstallieren"
  - "Deinstallieren von SQL Server"
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
caps.latest.revision: 74
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 73
---
# Deinstallieren einer vorhandenen SQL Server-Instanz (Setup)
  In diesem Artikel wird beschrieben, wie eine eigenständige Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deinstalliert wird. Mit den Schritten in diesem Thema wird das System außerdem für die erneute Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorbereitet.  
  
> [!IMPORTANT]  
>  Sie müssen ein lokaler Administrator sein und über die Berechtigung verfügen, sich als Dienst anzumelden, um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deinstallieren zu können.  
  
> [!NOTE]  
>  Zur Deinstallation eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failovercluster verwenden Sie die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup bereitgestellte Funktion Knoten entfernen, um jeden Knoten einzeln zu entfernen. Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
 Beachten Sie vor der Deinstallation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die folgenden wichtigen Szenarien:  
  
-   Bevor Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten von einem Computer entfernen, der die Mindestanforderungen für den physischen Arbeitsspeicher erfüllt, müssen Sie sicherstellen, dass die Auslagerungsdatei ausreichend groß ist. Die Auslagerungsdatei muss zwei Mal so groß sein wie der physische Speicher. Unzureichender virtueller Arbeitsspeicher kann dazu führen, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nur unvollständig entfernt wird.  
  
-   Wenn Sie mehrere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert haben, wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser automatisch deinstalliert, sobald die letzte Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] deinstalliert ist.  
  
     Um alle Komponenten von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]zu deinstallieren, müssen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserkomponente in der **Systemsteuerung** unter **Programme und Funktionen**manuell deinstallieren.  
  
1.  Beim Deinstallieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden tempdb-Datendateien gelöscht, die während des Installationsvorgangs hinzugefügt wurden. Dateien mit dem Namensmuster „tempdb_mssql_*.ndf“ werden gelöscht, wenn sie im Verzeichnis der Systemdatenbank vorhanden sind.  
  
### Vor der Deinstallation  
  
1.  **Sichern Sie die Daten.** Obwohl dieser Schritt nicht zwingend erforderlich ist, verfügen Sie möglicherweise über Datenbanken, die Sie in ihrem aktuellen Zustand speichern möchten. Möglicherweise möchten Sie auch an den Systemdatenbanken vorgenommene Änderungen speichern. Wenn einer dieser Fälle zutrifft, stellen Sie sicher, dass die Daten vor dem Deinstallieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gesichert werden. Speichern Sie alternativ eine Kopie aller Daten- und Protokolldateien in einem anderen Ordner als dem MSSQL-Ordner. Der MSSQL-Ordner wird während der Deinstallation gelöscht.  
  
     Die Dateien, die Sie speichern müssen, umfassen die im Folgenden aufgeführten Datenbankdateien:  
  
    -   Master.mdf  
  
    -   Mastlog.ldf  
  
    -   Model.mdf  
  
    -   Modellog.ldf  
  
    -   Msdbdata.mdf  
  
    -   Msdblog.ldf  
  
    -   Mssqlsystemresource.mdf  
  
    -   Mssqlsustemresource.ldf  
  
    -   Tempdb.mdf  
  
    -   Templog.ldf  
  
    -   ReportServer[$InstanceName] (Dies stellt die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Standarddatenbank dar.)  
  
    -   ReportServer[$InstanceName]TempDB (Dies stellt die temporäre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Standarddatenbank dar.)  
  
2.  **Löschen Sie die lokalen Sicherheitsgruppen.** Löschen Sie vor dem Deinstallieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die lokalen Sicherheitsgruppen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponenten.  
  
3.  **Beenden Sie alle**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Dienste.** Beenden Sie alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste vor dem Deinstallieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten. Aktive Verbindungen können eine erfolgreiche Deinstallation verhindern.  
  
4.  **Verwenden Sie ein Konto mit den entsprechenden Berechtigungen.** Melden Sie sich am Server an, indem Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto oder ein Konto mit entsprechenden Berechtigungen verwenden. Beispielsweise können Sie sich mit einem Konto beim Server anmelden, das Mitglied der lokalen Administratorgruppe ist.  
  
### Sie müssen ein lokaler Administrator sein und über die Berechtigung verfügen, sich als Dienst anzumelden, um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Um den Deinstallationsvorgang zu starten, wechseln Sie in der **Systemsteuerung** zu **Programme und Funktionen**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** , und wählen Sie **Deinstallieren**. Klicken Sie auf **Entfernen**. Dadurch wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installations-Assistent gestartet.  
  
     Unterstützungsregeln für Setup werden ausgeführt, um die Computerkonfiguration zu überprüfen. Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
3.  Wählen Sie im Dropdownfeld auf der Seite Instanz auswählen die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus, die Sie entfernen möchten, oder legen Sie fest, dass nur die freigegebenen Funktionen sowie die Verwaltungstools von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt werden sollen. Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
4.  Geben Sie auf der Seite Funktionen auswählen die Funktionen an, die aus der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt werden sollen.  
  
     Entfernungsregeln werden ausgeführt, um zu überprüfen, dass der Vorgang erfolgreich abgeschlossen werden kann.  
  
5.  Überprüfen Sie auf der Seite **Deinstallation kann jetzt ausgeführt werden** die Liste der Komponenten und Funktionen, die deinstalliert werden sollen. Klicken Sie auf **Entfernen** , um mit der Deinstallation zu beginnen.  
  
6.  Unmittelbar nach der Deinstallation der letzten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz sind die anderen Programme, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugeordnet sind, in der Programmliste in **Programme und Funktionen**weiterhin sichtbar. Wenn Sie **Programme und Funktionen**jedoch schließen, wird die Programmliste beim nächsten Öffnen von **Programme und Funktionen**aktualisiert, sodass nur die Programme angezeigt werden, die weiterhin installiert sind.  
  
### Falls die Deinstallation einen Fehler verursacht  
  
1.  Wenn der Deinstallationsvorgang nicht erfolgreich abgeschlossen wird, versuchen Sie, das Problem, das den Deinstallationsfehler verursacht hat, zu beheben. Die folgenden Artikel sollen helfen, den Ursachen für die fehlgeschlagene Deinstallation auf den Grund zu gehen:  
  
    -   [Identifizieren von SQL Server 2008-Setupproblemen in den Setupprotokolldateien](http://support.microsoft.com/kb/955396/en-us)  
  
    -   [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
2.  Falls sich die Ursache für den Deinstallationsfehler nicht beheben lässt, können Sie sich an den [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Support wenden. In einigen Fällen, z. B. falls wichtige Dateien versehentlich gelöscht wurden, muss vor der Neuinstallation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u. U. das Betriebssystem auf dem Computer neu installiert werden.  
  
## Siehe auch  
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  