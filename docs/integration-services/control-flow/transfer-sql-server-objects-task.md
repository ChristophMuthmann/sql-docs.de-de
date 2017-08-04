---
title: "Übertragen von SQL Server Objects Task | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfersqlserverobjectstask.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 45fec32beee153afea5f862c21cc607a2f807ce1
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-sql-server-objects-task"></a>SQL Server-Objekte kopieren (Task)
  Mit dem Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ wird mindestens ein Typ von Objekten in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank zwischen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]übertragen. Der Task kann z. B. Tabellen und gespeicherte Prozeduren kopieren. Je nach [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version, die als Quelle verwendet wird, stehen verschiedene Objekttypen zum Kopieren zur Verfügung. Nur eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank enthält z.B. Schemas und benutzerdefinierte Aggregate.  
  
## <a name="objects-to-transfer"></a>Objekte für die Übertragung  
 Serverrollen, Rollen und Benutzer aus der angegebenen Datenbank können kopiert werden sowie die Berechtigungen für die übertragenen Objekte. Indem die verknüpften Benutzer, Rollen und Berechtigungen zusammen mit den Objekten kopiert werden, können die übertragenen Objekte am Zielserver sofort ausgeführt werden.  
  
 Die folgende Tabelle enthält eine Liste der Objekttypen, die kopiert werden können.  
  
|Objekt|  
|------------|  
|Tabellen|  
|Sichten|  
|Gespeicherte Prozeduren|  
|Benutzerdefinierte Funktionen|  
|Standardwerte|  
|Benutzerdefinierte Datentypen|  
|Partitionsfunktionen|  
|Partitionsschemas|  
|Schemas|  
|Assemblys|  
|Benutzerdefinierte Aggregate|  
|Benutzerdefinierte Typen|  
|XML-Schemasammlung|  
  
 Für benutzerdefinierte Typen, die in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wurden, bestehen Abhängigkeiten mit CLR-Assemblys. Wenn Sie den Task [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen zum Übertragen von benutzerdefinierten Typen verwenden, müssen Sie den Task auch für die Übertragung abhängiger Objekte konfigurieren. Um abhängige Objekte zu übertragen, legen Sie die **IncludeDependentObjects** -Eigenschaft auf **TRUE**fest.  
  
### <a name="table-options"></a>Tabellenoptionen  
 Beim Kopieren von Tabellen können Sie die Typen der tabellenbezogenen Elemente angeben, die beim Kopiervorgang berücksichtigt werden sollen. Die folgenden Elementtypen können zusammen mit der verbundenen Tabelle kopiert werden:  
  
-   Indizes  
  
-   Trigger  
  
-   Volltextindizes  
  
-   Primärschlüssel  
  
-   Fremdschlüssel  
  
 Sie können auch angeben, ob das vom Task generierte Skript im Unicode-Format vorliegen soll.  
  
## <a name="destination-options"></a>Zieloptionen  
 Sie können den Task " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen" so konfigurieren, dass die Schemanamen, Daten, erweiterten Eigenschaften der übertragenen Objekte und die abhängigen Objekte bei der Übertragung berücksichtigt werden. Beim Kopieren der Daten können die bereits vorhandenen Daten ersetzt oder angefügt werden.  
  
 Einige Optionen gelten nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. So unterstützt z.B. nur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Schemas.  
  
## <a name="security-options"></a>Sicherheitsoptionen  
 Der Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankbenutzer und -Datenbankrollen aus der Quelle, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen sowie Berechtigungen für übertragene Objekte enthalten. Beispielsweise kann die Übertragung die Berechtigungen für die übertragenen Tabellen enthalten.  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>Übertragen von Objekten zwischen den Instanzen von SQL Server  
 Der Task ' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen' unterstützt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quelle bzw. ein -Ziel.  
  
## <a name="events"></a>Ereignisse  
 Der Task löst ein Informationsereignis aus, das das übertragene Objekt meldet, sowie ein Warnungsereignis, wenn ein Objekt überschrieben wird. Es wird auch ein Informationsereignis für Aktionen ausgelöst, z. B. das Kürzen von Datenbanktabellen.  
  
 Der Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ meldet keinen schrittweisen Fortschritt der Objektübertragung, sondern nur 0 % und 100 % der Ausführung.  
  
## <a name="execution-value"></a>Ausführungswert  
 Der in der **ExecutionValue** -Eigenschaft des Tasks gespeicherte Ausführungswert gibt die Anzahl der übertragenen Objekte zurück. Indem der **ExecValueVariable**-Eigenschaft des Tasks „SQL Server-Objekte übertragen“ eine benutzerdefinierte Variable zugewiesen wird, können Informationen über die Objektübertragung anderen Objekten im Paket zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Protokolleinträge  
 Der Task "SQL Server-Objekte übertragen" enthält die folgenden benutzerdefinierten Protokolleinträge:  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects: Dieser Protokolleintrag meldet, dass die Übertragung begonnen hat. Der Protokolleintrag enthält die Startzeit.  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects: Dieser Protokolleintrag meldet, dass die Übertragung abgeschlossen ist. Der Protokolleintrag enthält die Beendigungszeit.  
  
 Außerdem meldet ein Protokolleintrag für ein **OnInformation** -Ereignis die Anzahl der Objekttypen, die für die Übertragung ausgewählt wurden, die Anzahl der Objekte, die übertragen wurden, sowie Aktionen wie die Kürzung von Tabellen bei der Übertragung von Daten mit Tabellen. Für jedes Objekt am Ziel, das überschrieben wird, wird ein Protokolleintrag für das **OnWarning** -Ereignis erstellt.  
  
## <a name="security-and-permissions"></a>Sicherheit und Berechtigungen  
 Der Benutzer muss über die Berechtigung zum Durchsuchen von Objekten auf dem Quellserver verfügen sowie über die Berechtigung zum Löschen und Erstellen von Objekten auf dem Zielserver. Außerdem muss der Benutzer Zugriff auf die angegebene Datenbank und die Datenbankobjekte haben.  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>Konfigurieren des Tasks 'SQL Server-Objekte übertragen'  
 Der Task ' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen' kann so konfiguriert werden, dass alle Objekte eines Typs oder nur bestimmte Objekte eines Typs übertragen werden. Sie können z. B. wählen, ob Sie nur ausgewählte Tabellen in die AdventureWorks-Datenbank kopieren möchten.  
  
 Wenn der Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ Tabellen überträgt, können Sie die Typen tabellenbezogener Objekte angeben, die Sie mit den Tabellen kopieren möchten. So können Sie z. B. angeben, dass die Primärschlüssel mit den Tabellen kopiert werden.  
  
 Zum Verbessern der Funktionalität der übertragenen Objekte können Sie den Task ' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen' so konfigurieren, dass die Schemanamen, Daten, erweiterten Eigenschaften der übertragenen Objekte sowie die abhängigen Objekte bei der Übertragung berücksichtigt werden. Beim Kopieren von Daten können Sie angeben, ob die bereits vorhandenen Daten ersetzt oder angefügt werden sollen.  
  
 Zur Laufzeit stellt der Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ eine Verbindung mit den Quell- und Zielservern her. Dazu werden zwei SMO-Verbindungs-Manager verwendet. Die SMO-Verbindungs-Manager werden getrennt vom Task " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen" konfiguriert. Darauf wird dann im Task " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen" verwiesen. Die SMO-Verbindungs-Manager geben den Server- und Authentifizierungsmodus an, der beim Zugriff auf den Server verwendet werden soll. Weitere Informationen finden Sie unter [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „SQL Server-Objekte übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)  
  
-   [Editor für den Task „SQL Server-Objekte übertragen“ &#40;Seite „Objekte“&#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-objects-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>Programmgesteuerte Konfiguration des Tasks 'SQL Server-Objekte übertragen'  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
