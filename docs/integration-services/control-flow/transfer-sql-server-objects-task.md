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
- sql13.dts.designer.transfersqlserverobjects.general.f1
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: fd7916034970aba3a64d66ee2b59a1661d8a9515
ms.contentlocale: de-de
ms.lasthandoff: 08/11/2017

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
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>Programmgesteuerte Konfiguration des Tasks 'SQL Server-Objekte übertragen'  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
## <a name="transfer-sql-server-objects-task-editor-general-page"></a>Editor für den Task SQL Server-Objekte übertragen (Seite Allgemein)
  Mithilfe der Seite **Allgemein** des Dialogfelds **Editor für den Task SQL Server-Objekte übertragen** können Sie den Task [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen benennen und beschreiben.  
  
> [!NOTE]  
>  Der Benutzer, der den Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ erstellt, benötigt die Berechtigung, die Quellserverobjekte zum Kopieren auszuwählen sowie die Berechtigung, auf die Datenbank des Zielservers zuzugreifen, auf den die Objekte übertragen werden.  
  
### <a name="options"></a>enthalten  
 **Name**  
 Geben Sie für den Task [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen einen eindeutigen Namen ein. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung des Tasks [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen ein.  
  
## <a name="transfer-sql-server-objects-task-editor-objects-page"></a>Editor für den Task 'SQL Server-Objekte übertragen' (Seite Objekte)
  Verwenden Sie die Seite **Objekte** des Dialogfelds **Editor für den Task 'SQL Server-Objekte übertragen'** , um die Eigenschaften für das Kopieren eines oder mehrerer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine andere anzugeben. Tabellen, Sichten, gespeicherte Prozeduren und benutzerdefinierte Funktionen sind beispielsweise [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte, die Sie kopieren können.  
  
> [!NOTE]  
>  Der Benutzer, der den Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ erstellt, benötigt die entsprechende Berechtigung, die Quellserverobjekte zum Kopieren auszuwählen, sowie die Berechtigung, auf die Datenbank des Zielservers zuzugreifen, auf den die Objekte übertragen werden.  
  
### <a name="static-options"></a>Statische Optionen  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager, oder klicken Sie auf  **\<neue Verbindung... >** um eine neue Verbindung mit dem Quellserver zu erstellen.  
  
 **SourceDatabase**  
 Wählen Sie eine Datenbank auf dem Quellserver aus, aus der die Objekte kopiert werden sollen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager, oder klicken Sie auf  **\<neue Verbindung... >** um eine neue Verbindung mit dem Zielserver zu erstellen.  
  
 **DestinationDatabase**  
 Wählen Sie eine Datenbank auf dem Zielserver aus, auf den die Objekte kopiert werden sollen.  
  
 **DropObjectsFirst**  
 Bestimmen Sie, ob die ausgewählten Objekte vor dem Kopieren zuerst auf dem Zielserver gelöscht werden sollen.  
  
 **IncludeExtendedProperties**  
 Bestimmen Sie, ob erweiterte Eigenschaften beim Kopieren von Objekten vom Quellserver auf den Zielserver beibehalten werden sollen.  
  
 **CopyData**  
 Bestimmen Sie, ob beim Kopieren von Objekten vom Quellserver auf den Zielserver Daten beinhaltet werden sollen.  
  
 **ExistingData**  
 Bestimmen Sie, wie die Daten auf den Zielserver kopiert werden sollen. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Ersetzen**|Daten auf dem Zielserver werden überschrieben.|  
|**Anfügen**|Die vom Quellserver kopierten Daten werden an die vorhandenen Daten auf dem Zielserver angehängt.|  
  
> [!NOTE]  
>  Die Option **ExistingData** ist nur verfügbar, wenn **CopyData** auf **True**festgelegt ist.  
  
 **CopySchema**  
 Bestimmen Sie, ob mit dem Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ auch das Schema kopiert werden soll.  
  
> [!NOTE]  
>  **CopySchema** ist nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar.  
  
 **UseCollation**  
 Bestimmen Sie, ob die Übertragung von Objekten die auf dem Quellserver angegebene Sortierung beinhalten soll.  
  
 **IncludeDependentObjects**  
 Bestimmen Sie, ob beim Kopieren auch die kaskadierenden Objekte, die von den für das Kopieren ausgewählten Objekten abhängig sind, kopiert werden sollen.  
  
 **CopyAllObjects**  
 Bestimmen Sie, ob der Task alle Objekte der angegebenen Quelldatenbank oder nur die ausgewählten Objekte kopieren soll.  Wenn Sie diese Option auf False festlegen, haben Sie die Möglichkeit, die zu übertragenden Objekte auszuwählen. Dazu werden dann die dynamischen Optionen des Bereichs **CopyAllObjects**angezeigt.  
  
 **ObjectsToCopy**  
 Erweitern Sie **ObjectsToCopy** , um anzugeben, welche Objekte von der Quelldatenbank in die Zieldatenbank kopiert werden sollen.  
  
> [!NOTE]  
>  **ObjectsToCopy** ist nur verfügbar, wenn **CopyAllObjects** auf **False**festgelegt ist.  
  
 Die Optionen zum Kopieren der folgenden Objekttypen werden nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt:  
  
 Assemblys  
  
 Partitionsfunktionen  
  
 Partitionsschemas  
  
 Schemas  
  
 Benutzerdefinierte Aggregate  
  
 Benutzerdefinierte Typen  
  
 XML-Schemaauflistungen  
  
 **CopyDatabaseUsers**  
 Geben Sie an, ob die Übertragung Datenbankbenutzer beinhalten soll.  
  
 **CopyDatabaseRoles**  
 Geben Sie an, ob die Übertragung Datenbankrollen beinhalten soll.  
  
 **CopySqlServerLogins**  
 Geben Sie an, ob die Übertragung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen beinhalten soll.  
  
 **CopyObjectLevelPermissions**  
 Geben Sie an, ob die Übertragung Berechtigungen auf Objektebene beinhalten soll.  
  
 **CopyIndexes**  
 Geben Sie an, ob die Übertragung Indizes beinhalten soll.  
  
 **CopyTriggers**  
 Geben Sie an, ob die Übertragung Trigger beinhalten soll.  
  
 **CopyFullTextIndexes**  
 Geben Sie an, ob die Übertragung Volltextindizes beinhalten soll.  
  
 **CopyPrimaryKeys**  
 Geben Sie an, ob die Übertragung Primärschlüssel beinhalten soll.  
  
 **CopyForeignKeys**  
 Geben Sie an, ob die Übertragung Fremdschlüssel beinhalten soll.  
  
 **GenerateScriptsInUnicode**  
 Geben Sie an, ob die generierten Übertragungsskripts das Unicode-Format aufweisen sollen.  
  
### <a name="dynamic-options"></a>Dynamische Optionen  
  
#### <a name="copyallobjects--false"></a>CopyAllObjects = False  
 **CopyAllTables**  
 Bestimmen Sie, ob der Task alle Tabellen der angegebenen Quelldatenbank oder nur die ausgewählten Tabellen kopieren soll.  
  
 **TablesList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Tabellen auswählen** zu öffnen.  
  
 **CopyAllViews**  
 Bestimmen Sie, ob der Task alle Sichten der angegebenen Quelldatenbank oder nur die ausgewählten Sichten kopieren soll.  
  
 **ViewsList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Sichten auswählen** zu öffnen.  
  
 **CopyAllStoredProcedures**  
 Bestimmen Sie, ob der Task alle benutzerdefinierten gespeicherten Prozeduren der angegebenen Quelldatenbank oder nur die ausgewählten Prozeduren kopieren soll.  
  
 **StoredProceduresList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Gespeicherte Prozeduren auswählen** zu öffnen.  
  
 **CopyAllUserDefinedFunctions**  
 Bestimmen Sie, ob der Task alle benutzerdefinierten Funktionen der angegebenen Quelldatenbank oder nur die ausgewählten benutzerdefinierten Prozeduren kopieren soll.  
  
 **UserDefinedFunctionsList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Benutzerdefinierte Funktionen auswählen** zu öffnen.  
  
 **CopyAllDefaults**  
 Bestimmen Sie, ob der Task alle Standardwerte der angegebenen Quelldatenbank oder nur die ausgewählten Standardwerte kopieren soll.  
  
 **DefaultsList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Standardwerte auswählen** zu öffnen.  
  
 **CopyAllUserDefinedDataTypes**  
 Bestimmen Sie, ob der Task alle benutzerdefinierten Datentypen der angegebenen Quelldatenbank oder nur die ausgewählten benutzerdefinierten Datentypen kopieren soll.  
  
 **UserDefinedDataTypesList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Benutzerdefinierte Datentypen auswählen** zu öffnen.  
  
 **CopyAllPartitionFunctions**  
 Bestimmen Sie, ob der Task alle benutzerdefinierten Partitionsfunktionen der angegebenen Quelldatenbank oder nur die ausgewählten Partitionsfunktionen kopieren soll. Dies wird nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt.  
  
 **PartitionFunctionsList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Partitionsfunktionen auswählen** zu öffnen.  
  
 **CopyAllPartitionSchemes**  
 Bestimmen Sie, ob der Task alle Partitionsschemas der angegebenen Quelldatenbank oder nur die ausgewählten Partitionsschemas kopieren soll. Dies wird nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt.  
  
 **PartitionSchemesList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Partitionsschemas auswählen** zu öffnen.  
  
 **CopyAllSchemas**  
 Bestimmen Sie, ob der Task alle Schemas der angegebenen Quelldatenbank oder nur die ausgewählten Schemas kopieren soll. Dies wird nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt.  
  
 **SchemasList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Schemas auswählen** zu öffnen.  
  
 **CopyAllSqlAssemblies**  
 Bestimmen Sie, ob der Task alle SQL-Assemblys der angegebenen Quelldatenbank oder nur die ausgewählten SQL-Assemblys kopieren soll. Dies wird nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt.  
  
 **SqlAssembliesList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Assemblys auswählen** zu öffnen.  
  
 **CopyAllUserDefinedAggregates**  
 Bestimmen Sie, ob der Task alle benutzerdefinierten Aggregate der angegebenen Quelldatenbank oder nur die ausgewählten benutzerdefinierten Aggregate kopieren soll. Dies wird nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt.  
  
 **UserDefinedAggregatesList**  
 Klicken Sie auf diese Option, um das Dialogfeld **Benutzerdefinierte Aggregate** auswählen zu öffnen.  
  
 **CopyAllUserDefinedTypes**  
 Bestimmen Sie, ob der Task alle benutzerdefinierten Typen der angegebenen Quelldatenbank oder nur die ausgewählten benutzerdefinierten Datentypen kopieren soll. Dies wird nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt.  
  
 **UserDefinedTypes**  
 Klicken Sie auf diese Option, um das Dialogfeld **Benutzerdefinierte Typen** auswählen zu öffnen.  
  
 **CopyAllXmlSchemaCollections**  
 Bestimmen Sie, ob der Task alle XML-Schemaauflistungen der angegebenen Quelldatenbank oder nur die ausgewählten XML-Schemaauflistungen kopieren soll. Dies wird nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützt.  
  
 **XmlSchemaCollectionsList**  
 Klicken Sie auf diese Option, um das Dialogfeld **XML-Schemaauflistungen** auswählen zu öffnen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Übertragen Sie die Task-Editor für SQL Server-Objekte &#40; Seite "Allgemein" &#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [Datenformate für Massenimport oder Massenexport &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [Überlegungen zur Sicherheit bei SQL Server-Installationen](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  

