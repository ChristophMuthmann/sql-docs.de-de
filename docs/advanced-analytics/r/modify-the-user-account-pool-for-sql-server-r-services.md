---
title: "Ändern des Benutzerkontenpools für SQL Server R Services | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 33e22f7edec807d046798d89a9cd5daa642e8d3b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="modify-the-user-account-pool-for-sql-server-r-services"></a>Ändern des Benutzerkontenpools für SQL Server R Services
  Im Rahmen des Installationsprozesses für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] wird ein neuer Windows-*Benutzerkontenpool* erstellt, um die Ausführung von Aufgaben vom [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienst zu unterstützen. Der Zweck dieser Workerkonten ist es, das gleichzeitige Ausführen von R-Skripts von verschiedenen SQL-Benutzern zu isolieren. 

In diesem Thema wird die Standardkonfiguration, -sicherheit und -kapazität der Workerkonten beschrieben; außerdem wird beschrieben, wie Sie die Standardkonfiguration ändern können.

## <a name="worker-accounts-used-by-r-services"></a>Von R Services verwendete Workerkonten   

Die Windows-Kontengruppe wird vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup für jede Instanz erstellt, auf der R-Services installiert ist. Daher gibt es mehrere Benutzergruppen, wenn Sie mehrere Instanzen installiert haben, die R unterstützen.

-   In einer Standardinstanz ist der Gruppenname **SQLRUserGroup**. 
-   In einer benannten Instanz erhält der Standardgruppenname den Instanznamen als Suffix, z.B. **SQLRUserGroupMyInstanceName**. 

Standardmäßig enthält der Benutzerkontenpool 20 Benutzerkonten. In den meisten Fällen sind 20 Konten mehr als ausreichend, um R-Sitzungen zu unterstützen; wenn nötig können Sie die Anzahl der Konten anpassen.
-  In einer Standardinstanz haben die einzelnen Konten Namen von **MSSQLSERVER01** bis **MSSQLSERVER20**.  
-   In einer benannten Instanz sind die Konten nach dem Instanznamen benannt, z.B **MyInstanceName01** bis **MyInstanceName20**.  

### <a name = "HowToChangeGroup"> </a> Anpassen der Anzahl von R-Workerkonten

Sie müssen die Eigenschaften des [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienstes wie unten beschrieben ändern, um die Anzahl der Benutzer im Kontenpool zu ändern.  
  
Die jeweiligen Kennwörter der Benutzerkonten werden nach dem Zufallsprinzip generiert. Sie können Sie zu einem späteren Zeitpunkt ändern, nachdem die Konnten erstellt wurden.  
  
1. Klicken Sie im SQL Server Configuration Manager auf **SQL Server-Dienste**.
2. Doppelklicken Sie auf den Launchpad-Dienst von SQL Server und beenden Sie den Dienst, wenn er ausgeführt wird. 
3.  Achten Sie darauf, dass der Startmodus auf der Registerkarte **Dienst** auf „Automatisch“ festgelegt ist. Wenn Launchpad nicht ausgeführt wird, schlagen R-Skripts fehl.
4.  Klicken Sie auf die Registerkarte **Erweitert**, und bearbeiten Sie den Wert von **External Users Count** (Anzahl externer Benutzer), wenn nötig. Diese Einstellung steuert, wie viele verschiedene SQL-Benutzer gleichzeitig Abfragen in R ausführen können. Der Standard sind 20 Konten.
5. Sie können die Option **Reset External Users Password** (Kennwörter externer Benutzer zurücksetzen) auch wahlweise auf _Ja_ festlegen, wenn Ihre Organisation eine Richtlinie zum regelmäßigen Ändern des Kennworts hat. Damit werden die verschlüsselten Kennwörter erneut generiert, die Launchpad für die Benutzerkonten verwaltet. Weitere Informationen finden Sie unter [Enforcing Password Policy (Erzwingen der Kennwortrichtlinie)](#bkmk_EnforcePolicy).    
6.  Starten Sie den Dienst neu.  

## <a name="managing-r-workload"></a>Verwalten von R-Arbeitsauslastungen

Die Anzahl von Konten in diesem Pool bestimmt, wie viele R-Sitzungen gleichzeitig aktiv sein können.  Standardmäßig werden 20 Konten erstellt, d.h., dass 20 verschiedene Benutzer zur gleichen Zeit aktive R-Sitzungen haben können. Wenn Sie vorhersagen können, dass mehr Benutzer gleichzeitig R-Skripts ausführen werden, können Sie die Anzahl von Workerkonten erhöhen. 

Wenn der gleiche Benutzer mehrere R-Skripts gleichzeitig ausführt, verwenden alle von diesem Benutzer ausgeführten Sitzungen das gleiche Workerkonto. Ein einzelner Benutzer kann z.B. 100 verschiedene R-Skripts gleichzeitig mit einem einzelnen Workerkonto ausführen – solange die Ressourcen die zulassen.

Die Anzahl von Workerkonten, die Sie unterstützen können, und die Anzahl von gleichzeitigen R-Sitzungen, die ein einzelner Benutzer ausführen kann, werden nur durch Serverressourcen eingeschränkt.  Für gewöhnlich ist der Arbeitsspeicher der erste Engpass beim Verwenden der R-Laufzeit.

In R Services werden die Ressourcen, die von R-Skripts verwendet werden können, von SQL Server gesteuert. Es wird empfohlen, dass Sie die Ressourcenauslastung mit SQL Server DMVs überwachen oder sich Leistungsindikatoren im verknüpften Windows-Auftragsobjekt anschauen; so können Sie die Arbeitsspeicherauslastung des Servers entsprechend anpassen. 
 
Wenn Sie SQL Server Enterprise Edition verwenden, können Sie Ressource für das Ausführen von R-Skripts zuweisen, indem Sie einen [externen Ressourcenpool](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md) konfigurieren. 

Weitere Informationen zur Verwaltung von R-Skriptkapazitäten finden Sie in folgenden Artikeln:

- [SQL Server-Konfiguration für R Services](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
-  [Leistungsfallstudie für R Services](../../advanced-analytics/r-services/performance-case-study-r-services.md)

## <a name="security"></a>Sicherheit

Jede Benutzergruppe wird mit dem [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienst auf einer bestimmten Instanz verknüpft und kann keine R-Aufträge unterstützen, die auf anderen Instanzen ausgeführt werden.

Während die Sitzung aktiv ist, wird für jedes Workerkonto ein temporärer Ordner zum Speichern von Skriptobjekten, Zwischenergebnissen und anderen von R und SQL Server während der Ausführung eines R-Skripts verwendeten Informationen erstellt. Auf diese Arbeitsdateien im Ordner „ExtensibilityData“ können nur Administratoren zugreifen. Sie werden von SQL Server bereinigt, nachdem das Skript abgeschlossen wurde. 

Weitere Informationen finden Sie unter [Sicherheitsübersicht](../../advanced-analytics/r-services/security-overview-sql-server-r.md).

### <a name="bkmk_EnforcePolicy"></a> Kennwortrichtlinie erzwingen

Wenn Ihre Organisation eine Richtlinie hat, die das regelmäßige Ändern von Kennwörtern erfordert, müssen Sie möglicherweise den Launchpad-Dienst zwingen, die verschlüsselten Kennwörter erneut zu generieren, die Launchpad für seine Workerkonten verwaltet.  

Öffnen Sie den Bereich **Eigenschaften** für den Launchpad-Dienst in SQL Server Configuration Manager, klicken Sie auf **Erweitert**, und ändern Sie **Reset External Users Password** (Kennwörter externer Benutzer zurücksetzen) in **Yes** (Ja). Wenn Sie diese Änderung übernehmen, werden die Kennwörter sofort für alle Benutzerkonten erneut generiert. Sie müssen den Launchpad-Dienst neu starten, um R-Skripts nach dieser Änderungen verwenden zu können; nun werden auch die neu generierten Kennwörter gelesen. 

Sie können dieses Flag entweder manuell festlegen oder dazu ein Skript verwenden.

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>Zusätzliche Berechtigung für das Unterstützen eines Remoterechenkontexts erforderlich

Standardmäßig hat die Gruppe von R-Workerkonten **keine** Anmeldeberechtigung auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, mit der sie verknüpft ist. Dies kann zu einem Problem führen, wenn R-Benutzer von einem Remoteclient eine Verbindung mit SQL Server herstellen, um R-Skripts auszuführen, oder wenn ein Skript DBC verwendet, um zusätzliche Daten zu erhalten. 

Der Datenbankadministrator muss der Gruppe von R-Workerkonten die Anmeldeberechtigung für die SQL Server-Instanz erteilen, in der R-Skripts ausgeführt werden sollen (**Connect to**-Berechtigung (Verbinden mit)), um sicherzustellen, dass diese Szenarios unterstützt werden. Dies wird als *implizite Authentifizierung* bezeichnet, und gibt SQL Server die Möglichkeit, die R-Skripts mit den Anmeldeinformationen des Remotebenutzers auszuführen.

> [!NOTE]
> Diese Einschränkung gilt nicht, wenn Sie SQL-Benutzernamen verwenden, um R-Skripts von einer Remotearbeitsstation auszuführen, da die SQL-Anmeldeinformationen explizit vom R-Client an die SQL Server-Instanz und dann an ODBC übergeben werden.


### <a name="how-to-enable-implied-authentication"></a>Aktivieren der impliziten Authentifizierung

1. Öffnen Sie SQL Server Management Studio als Administrator auf der Instanz, auf der Sie R-Code ausführen werden.

2. Führen Sie das folgende Skript aus: Achten Sie darauf, den Namen der Benutzergruppe zu bearbeiten, wenn Sie die Standardeinstellung geändert haben. Bearbeiten Sie außerdem den Namen des Computers und der Instanz.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ````


  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  

