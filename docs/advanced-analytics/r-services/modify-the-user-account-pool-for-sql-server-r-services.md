---
title: "&#196;ndern des Benutzerkontenpools f&#252;r SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# &#196;ndern des Benutzerkontenpools f&#252;r SQL Server R Services
  Als Teil des Installationsprozesses für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], einen neuen Windows *Konto Benutzerpool* wird erstellt, um die Ausführung von Aufgaben unterstützen die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] Service. Diese Konten dient zum Isolieren gleichzeitiger Ausführung des R-Skripts von verschiedenen Benutzern von SQL.
  
  Die Anzahl von Benutzerkonten in diesem Pool bestimmt, wie viele R-Sitzungen gleichzeitig aktiv sein können.   Wenn derselbe Benutzer mehrere R-Skripts gleichzeitig ausgeführt wird, wird lediglich die Sitzungen von diesem Benutzer ausgeführt dasselbe workerkonto verwenden. Infolgedessen wird möglicherweise ein einzelner Benutzer 100 verschiedene R-Skripts, die gleichzeitig solange Ressourcen ausgeführt.

## Standardkonfiguration   
-   In einer Standardinstanz der Gruppenname ist **SQLRUserGroup**. 
-   Der Standardname ist in eine benannte Instanz mit dem Instanznamen Formatangabe: z. B. **SQLRUserGroupMyInstanceName**. 
-   Konten: Konto Benutzerpool enthält standardmäßig 20 Benutzerkonten, die mit dem Namen **MSSQLSERVER01** über **MSSQLSERVER20** für die Standardinstanz.  
-   Für eine benannte Instanz, die Benutzerkonten werden mit dem Namen unter Verwendung der Instanz: z. B. **MyInstanceName01** über **MyInstanceName20**.  


## Verwalten die Benutzergruppe für jede Instanz
Die Windows-Gruppe wird erstellt, indem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup für jede Instanz auf dem R-Services installiert ist, der, wenn Sie mehrere Instanzen, die Unterstützung von R installiert haben, mehrere Benutzergruppen werden.
Jedoch jede Benutzergruppe zugeordnet ist die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] auf eine bestimmte Instanz und unterstützt keine R-Aufträge, die auf anderen Instanzen ausgeführt.

Standardmäßig die Gruppe ist **nicht** über die Login-Berechtigung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz, dem es zugeordnet ist. Wenn Sie die Ausführung des R-Skripts von Benutzern aktivieren zu müssen, muss der Datenbankadministrator Bereitstellen dieser Gruppe mit **Herstellen einer Verbindung mit** Berechtigungen.  

### Ändern der Anzahl der Konten in der Windows-Benutzergruppe

Um die Anzahl der Benutzer im Pool Konto zu ändern, müssen Sie die Eigenschaften Bearbeiten der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service wie unten beschrieben.  
  
Jedes Benutzerkonto zugehörigen Kennwörter werden nach dem Zufallsprinzip generiert, aber Sie können diese später ändern, nachdem die Konten erstellt werden.  
  
1. Öffnen Sie SQL Server-Konfigurations-Manager, und wählen Sie **SQL Server-Dienste**.
2. Doppelklicken Sie auf die SQL Server Launchpad-Dienst, und beenden Sie den Dienst, falls er ausgeführt wird. 
3.  Auf der **Service** Registerkarte, stellen Sie sicher, dass der Startmodus auf automatisch festgelegt ist. R-Skripts schlägt fehl, wenn das LaunchPad nicht ausgeführt wird.
4.  Klicken Sie auf die **Erweitert** Registerkarte, und bearbeiten Sie den Wert der **Anzahl der externen Benutzer** bei Bedarf. Diese Einstellung steuert, wie viele verschiedene SQL-Benutzer Abfragen gleichzeitig in r ausgeführt werden können Der Standardwert ist 20 Konten, die in den meisten Fällen ist mehr als ausreichend, um R-Sitzungen zu unterstützen.
5. Optional können Sie die Option festlegen **externe Benutzerkennwort zurücksetzen** zu _Ja_ verfügt Ihre Organisation eine Richtlinie, die erforderlich sind, Ändern von Kennwörtern alle 90 Tage. Auf diese Weise wird die verschlüsselte Kennwörter erneut generieren, die LaunchPad für die Benutzerkonten verwaltet.    
6.  Starten Sie den Dienst neu.  

## Zusätzliche Berechtigungen erforderlich sind, für die Remoteausführung von Skripts
Bei Ausführung der R-Skripts mit dem SQL Server-Computer als eine compute-Kontext, dieser workergruppe benötigt die Berechtigung zur Anmeldung der SQL Server-Instanz, in dem R-Skripts ausgeführt werden.

Weitere Informationen finden Sie unter [häufig gestellte Fragen zu Aktualisierung und Installation](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md). 

  
## Siehe auch  
 [Konfiguration (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  