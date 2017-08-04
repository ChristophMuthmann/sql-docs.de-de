---
title: "Editor für SQL Server Objects Task (Seite Objekte) übertragen | Microsoft Docs"
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
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects Task Editor
ms.assetid: 8cc09118-70ac-4013-8308-d87f8411ca0c
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 67557562dd3f2efbe3c40673a835dd557f617604
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-sql-server-objects-task-editor-objects-page"></a>Editor für den Task 'SQL Server-Objekte übertragen' (Seite Objekte)
  Verwenden Sie die Seite **Objekte** des Dialogfelds **Editor für den Task 'SQL Server-Objekte übertragen'** , um die Eigenschaften für das Kopieren eines oder mehrerer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine andere anzugeben. Tabellen, Sichten, gespeicherte Prozeduren und benutzerdefinierte Funktionen sind beispielsweise [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte, die Sie kopieren können. Weitere Informationen zu diesem Task finden Sie unter [Transfer SQL Server Objects Task](../../integration-services/control-flow/transfer-sql-server-objects-task.md).  
  
> [!NOTE]  
>  Der Benutzer, der den Task „ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte übertragen“ erstellt, benötigt die entsprechende Berechtigung, die Quellserverobjekte zum Kopieren auszuwählen, sowie die Berechtigung, auf die Datenbank des Zielservers zuzugreifen, auf den die Objekte übertragen werden.  
  
## <a name="static-options"></a>Statische Optionen  
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
  
## <a name="dynamic-options"></a>Dynamische Optionen  
  
### <a name="copyallobjects--false"></a>CopyAllObjects = False  
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
  
  
