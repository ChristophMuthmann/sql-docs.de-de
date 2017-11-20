---
title: "Konstanten in Eigenschaftsausdrücken | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], expressions
- dynamic properties
- updating package properties
- enumerated constants [Integration Services]
- property expressions [Integration Services]
ms.assetid: a4418315-38e2-4ad3-8784-576163b25d6f
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8483c36dca5a24485e865b1115e766aa579635b9
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="enumerated-constants-in-property-expressions"></a>Aufgezählte Konstanten in Eigenschaftsausdrücken
  Wenn Eigenschaftsausdrücke Werte aus einer Liste von Enumeratorelementen enthalten, müssen die Ausdrücke den numerischen Wert des Enumeratorelements anstelle des Anzeigenamens des Elements verwenden. Wenn z. B. ein Ausdruck die **LoggingMode** -Eigenschaft festlegt, müssen Sie den numerischen Wert 2 anstelle des Anzeigenamens Disabled verwenden.  
  
 In diesem Thema werden nur die entsprechenden numerischen Werte für Anzeigenamen von Enumeratoren aufgelistet, deren Elemente häufig in Eigenschaftsausdrücken verwendet werden. Das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell enthält viele zusätzliche Enumeratoren, die Sie beim Programmieren des Objektmodells verwenden können, um Pakete programmgesteuert zu erstellen oder um benutzerdefinierte Paketelemente, wie z. B. Tasks und Datenflusskomponenten, zu programmieren.  
  
 Neben den benutzerdefinierten Eigenschaften für Pakete und Paketobjekte enthält das Eigenschaftenfenster in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] eine Reihe von Eigenschaften, die für Pakete, Tasks, für die Foreach- und For-Schleife sowie für Sequenzcontainer zur Verfügung stehen. Die allgemeinen Eigenschaften, die mithilfe von Werten aus Enumeratoren festgelegt werden - hierzu zählen die**ForceExecutionResult**-, **LoggingMode**-, **IsolationLevel**- und **Transaction Option**-Enumeratoren -, werden im Abschnitt Allgemeine Eigenschaften aufgelistet.  
  
 In den folgenden Abschnitten werden Informationen zu den folgenden aufgelisteten Konstanten bereitgestellt:  
  
 [Paket](#Package)  
  
 [Foreach-Schleifenenumeratoren](#Foreach)  
  
 [Aufgaben](#Tasks)  
  
 [Wartungsplantasks](#MaintenancePlanTasks)  
  
 [Allgemeine Eigenschaften](#CommonProperties)  
  
##  <a name="Package"></a> Paket  
 In den folgenden Tabellen finden Sie eine Auflistung der Anzeigenamen und der entsprechenden numerischen Werte für Eigenschaften von Paketen, die Sie mithilfe von Werten eines Enumerators festlegen.  
  
 **PackageType** -Eigenschaft – Festlegung mithilfe von Werten der **DTSPackageType** -Enumeration.  
  
|Anzeigename in DTSPackageType|Numerischer Wert|  
|-------------------------------------|-------------------|  
|Standardwert|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 **CheckpointUsage** -Eigenschaft – Festlegung mithilfe von Werten der **DTSCheckpointUsage** -Enumeration.  
  
|Anzeigename in DTSCheckpointUsage|Numerischer Wert|  
|-----------------------------------------|-------------------|  
|Never|0|  
|IfExists|1|  
|Always|2|  
  
 **PackagePriorityClass** -Eigenschaft – Festlegung mithilfe von Werten der **DTSPriorityClass** -Enumeration.  
  
|Anzeigename in DTSPriorityClass|Numerischer Wert|  
|---------------------------------------|-------------------|  
|Standardwert|0|  
|AboveNormal|1|  
|Normal|2|  
|BelowNormal|3|  
|Idle|4|  
  
 **ProtectionLevel** -Eigenschaft – Festlegung mithilfe von Werten der **DTSProtectionLevel** -Enumeration.  
  
|Anzeigename in DTSProtectionLevel|Numerischer Wert|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="PrecedenceConstraints"></a> Rangfolgeneinschränkungen  
 **EvalOp** -Eigenschaft – Festlegung mithilfe von Werten der **DTSPrecedenceEvalOp** -Enumeration.  
  
|Anzeigename in DTSPrecedenceEvalOp|Numerischer Wert|  
|------------------------------------------|-------------------|  
|expression|1|  
|Einschränkung|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 **Value** -Eigenschaft – Festlegung mithilfe von Werten der **DTSExecResult** -Enumeration.  
  
|Anzeigename|Numerischer Wert|  
|-------------------|-------------------|  
|Success|0|  
|Failure|1|  
|Completion|2|  
|Canceled|3|  
  
##  <a name="Foreach"></a> Foreach-Schleifenenumeratoren  
 Die Foreach-Schleife enthält eine Reihe von Enumeratoren mit Eigenschaften, die mithilfe von Eigenschaftsausdrücken festgelegt werden können.  
  
### <a name="foreach-ado-enumerator"></a>Foreach-ADO-Enumerator  
 **Type** -Eigenschaft – Festlegung mithilfe von Werten der **ADOEnumerationType** -Enumeration.  
  
|Anzeigename in ADOEnumerationType|Numerischer Wert|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Foreach-NodeList-Enumerator  
 **SourceDocumentType**-, **InnerXPathStringSourceType**- und **OuterXPathStringSourceType** -Eigenschaften – Festlegung mithilfe von Werten der **SourceType** -Enumeration.  
  
|Anzeigename in SourceType|Numerischer Wert|  
|---------------------------------|-------------------|  
|FileConnection|0|  
|Variable|1|  
|DirectInput|2|  
  
 **EnumerationType** -Eigenschaft – Festlegung mithilfe von Werten der **EnumerationType** -Enumeration.  
  
|Anzeigename in EnumerationType|Numerischer Wert|  
|--------------------------------------|-------------------|  
|Navigator|0|  
|Node|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 **InnerElementType** -Eigenschaft – Festlegung mithilfe von Werten der **InnerElementType** -Enumeration.  
  
|Anzeigename in InnerElementType|Numerischer Wert|  
|---------------------------------------|-------------------|  
|Navigator|0|  
|Node|1|  
|NodeText|2|  
  
##  <a name="Tasks"></a> Aufgaben  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält eine Reihe von Tasks mit Eigenschaften, die mithilfe von Eigenschaftsausdrücken festgelegt werden können.  
  
### <a name="analysis-services-execute-ddl-task"></a>DDL ausführen (Analysis Services-Task)  
 **SourceType** -Eigenschaft – Festlegung mithilfe von Werten der **DDLSourceType** -Enumeration.  
  
|Anzeigename in DDLSourceType|Numerischer Wert|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variable|2|  
  
### <a name="bulk-insert-task"></a>Masseneinfügungstask  
 **DataFileType** -Eigenschaft – Festlegung mithilfe von Werten der **DTSBulkInsert_DataFileType** -Enumeration.  
  
|Anzeigename in DTSBulkInsert_DataFileType|Numerischer Wert|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>SQL ausführen (Task)  
 **ResultSetType** -Eigenschaft – Festlegung mithilfe von Werten der **ResultSetType** -Enumeration.  
  
|Anzeigename in ResultSetType|Numerischer Wert|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 **SqlStatementSourceType** -Eigenschaft – Festlegung mithilfe von Werten der **SqlStatementSourceType** -Enumeration.  
  
|Anzeigename in SqlStatementSourceType|Numerischer Wert|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|FileConnection|2|  
|Variable|3|  
  
### <a name="file-system-task"></a>Task Dateisystem  
 **Operation** -Eigenschaft – Festlegung mithilfe von Werten der **DTSFileSystemOperation** -Enumeration.  
  
|Anzeigename in DTSFileSystemOperation|Numerischer Wert|  
|---------------------------------------------|-------------------|  
|CopyFile|0|  
|MoveFile|1|  
|DeleteFile|2|  
|RenameFile|3|  
|SetAttributes|4|  
|CreateDirectory|5|  
|CopyDirectory|6|  
|MoveDirectory|7|  
|DeleteDirectory|8|  
|DeleteDirectoryContent|9|  
  
 **Attributes** -Eigenschaft – Festlegung mithilfe von Werten der **DTSFileSystemAttributes** -Enumeration.  
  
|Anzeigename in DTSFileSystemAttributes|Numerischer Wert|  
|----------------------------------------------|-------------------|  
|Normal|0|  
|Archive|1|  
|Hidden|2|  
|ReadOnly|4|  
|System|8|  
  
### <a name="ftp-task"></a>FTP-Task  
 **Operation** -Eigenschaft – Festlegung mithilfe von Werten der **DTSFTPOp** -Enumeration.  
  
|Anzeigename in DTSFTPOp|Numerischer Wert|  
|-------------------------------|-------------------|  
|Send|0|  
|Receive|1|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Nachrichtenwarteschlange (Task)  
 **MessageType** -Eigenschaft – Festlegung mithilfe von Werten der **MQMessageType** -Enumeration.  
  
|Anzeigename in MQMessageType|Numerischer Wert|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 **StringCompareType** -Eigenschaft – Festlegung mithilfe von Werten der **MQStringMessageCompare** -Enumeration.  
  
|Anzeigename in MQStringMessageCompare|Numerischer Wert|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 **TaskType** -Eigenschaft – Festlegung mithilfe von Werten der **MQType** -Enumeration.  
  
|Anzeigename in MQType|Numerischer Wert|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>Mail senden (Task)  
 **MessageSourceType** -Eigenschaft – Festlegung mithilfe von Werten der **SendMailMessageSourceType** -Enumeration.  
  
|Anzeigename in SendMailMessageSourceType|Numerischer Wert|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|Variable|2|  
  
 **Priority** -Eigenschaft – Festlegung mithilfe von Werten der **MailPriority** -Enumeration.  
  
|Anzeigename in MailPriority|Numerischer Wert|  
|-----------------------------------|-------------------|  
|High|1|  
|Normal|3|  
|Low|5|  
  
### <a name="transfer-database-task"></a>Datenbanken übertragen (Task)  
 **Action** -Eigenschaft – Festlegung mithilfe von Werten der **TransferAction** -Enumeration.  
  
|Anzeigename in TransferAction|Numerischer Wert|  
|-------------------------------------|-------------------|  
|Kopieren|0|  
|Verschieben|1|  
  
 **Method** -Eigenschaft – Festlegung mithilfe von Werten der **TransferMethod** -Enumeration.  
  
|Anzeigename in TransferMethod|Numerischer Wert|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>Fehlermeldungen übertragen (Task)  
 **IfObjectExists** -Eigenschaft – Festlegung mithilfe von Werten der **IfObjectExists** -Enumeration.  
  
|Anzeigename in IfObjectExists|Numerischer Wert|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>Aufträge übertragen (Task)  
 **IfObjectExists** -Eigenschaft – Festlegung mithilfe von Werten der **IfObjectExists** -Enumeration.  
  
|Anzeigename in IfObjectExists|Numerischer Wert|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>Task "Anmeldungen übertragen"  
 **IfObjectExists** -Eigenschaft – Festlegung mithilfe von Werten der **IfObjectExists** -Enumeration.  
  
|Anzeigename in IfObjectExists|Numerischer Wert|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
 **LoginsToTransfer** -Eigenschaft – Festlegung mithilfe von Werten der **LoginsToTransfer** -Enumeration.  
  
|Anzeigename in LoginsToTransfer|Numerischer Wert|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>In master gespeicherte Prozeduren übertragen (Task)  
 **IfObjectExists** -Eigenschaft – Festlegung mithilfe von Werten der **IfObjectExists** -Enumeration.  
  
|Anzeigename in IfObjectExists|Numerischer Wert|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>SQL Server-Objekte kopieren (Task)  
 **ExistingData** -Eigenschaft – Festlegung mithilfe von Werten der **ExistingData** -Enumeration.  
  
|Anzeigename in ExistingData|Numerischer Wert|  
|-----------------------------------|-------------------|  
|Ersetzen|0|  
|Anfügen|1|  
  
### <a name="web-service-task"></a>Webdienst (Task)  
 **OutputType** -Eigenschaft – Festlegung mithilfe von Werten der **DTSOutputType** -Enumeration.  
  
|Anzeigename in DTSOutputType|Numerischer Wert|  
|------------------------------------|-------------------|  
|File|0|  
|Variable|1|  
  
### <a name="wmi-data-reader-task"></a>WMI-Datenleser (Task)  
 **OverwriteDestination** -Eigenschaft – Festlegung mithilfe von Werten der **OverwriteDestination** -Enumeration.  
  
|Anzeigename in OverwriteDestination|Numerischer Wert|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 **OutputType** -Eigenschaft – Festlegung mithilfe von Werten der **OutputType** -Enumeration.  
  
|Anzeigename in OutputType|Numerischer Wert|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 **DestinationType** -Eigenschaft – Festlegung mithilfe von Werten der **DestinationType** -Enumeration.  
  
|Anzeigename in DestinationType|Numerischer Wert|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|Variable|1|  
  
 **WqlQuerySourceType** -Eigenschaft – Festlegung mithilfe von Werten der **QuerySourceType** -Enumeration.  
  
|Anzeigename in QuerySourceType|Numerischer Wert|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variable|2|  
  
 **ActionAtEvent** -Eigenschaft der WMI-Ereignisüberwachung – Festlegung mithilfe von Werten der **ActionAtEvent** -Enumeration.  
  
|Anzeigename in ActionAtEvent|Numerischer Wert|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 **ActionAtTimeout** -Eigenschaft – Festlegung mithilfe von Werten der **ActionAtTimeout** -Enumeration.  
  
|Anzeigename in ActionAtTimeout|Numerischer Wert|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 **AfterEvent** -Eigenschaft – Festlegung mithilfe von Werten der **AfterEvent** -Enumeration.  
  
|Anzeigename in AfterEvent|Numerischer Wert|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 **AfterTimeout** -Eigenschaft – Festlegung mithilfe von Werten der **AfterTimeout** -Enumeration.  
  
|Anzeigename in AfterTimeout|Numerischer Wert|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 **WqlQuerySourceType** -Eigenschaft – Festlegung mithilfe von Werten der **QuerySourceType** -Enumeration.  
  
|Anzeigename in QuerySourceType|Numerischer Wert|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|Variable|2|  
  
### <a name="xml-task"></a>XML-Task  
 **OperationType** -Eigenschaft – Festlegung mithilfe von Werten der **DTSXMLOperation** -Enumeration.  
  
|Anzeigename in DTSXMLOperation|Numerischer Wert|  
|--------------------------------------|-------------------|  
|Überprüfen|0|  
|XSLT|1|  
|XPATH|2|  
|Merge|3|  
|Diff|4|  
|Patch|5|  
  
 Eigenschaften**SourceType**, **SecondOperandType**und **XPathSourceType** – Festlegung mithilfe von Werten der **DTSXMLSourceType** -Enumeration.  
  
|Anzeigename in DTSXMLSourceType|Numerischer Wert|  
|---------------------------------------|-------------------|  
|FileConnection|0|  
|Variable|1|  
|DirectInput|2|  
  
 **DestinationType** -Eigenschaft und **DiffGramDestinationType** -Eigenschaft – Festlegung mithilfe von Werten der **DTSXMLSaveResultTo** -Enumeration.  
  
|Anzeigename in DTSXMLSaveResultTo|Numerischer Wert|  
|-----------------------------------------|-------------------|  
|FileConnection|0|  
|Variable|1|  
  
 **ValidationType** -Eigenschaft – Festlegung mithilfe von Werten der **DTSXMLValidationType** -Enumeration.  
  
|Anzeigename in DTSXMLValidationType|Numerischer Wert|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 **XPathOperation** -Eigenschaft – Festlegung mithilfe von Werten der **DTSXMLXPathOperation** -Enumeration.  
  
|Anzeigename in DTSXMLXPathOperation|Numerischer Wert|  
|-------------------------------------------|-------------------|  
|Evaluation|0|  
|Werte|1|  
|NodeList|2|  
  
 **DiffOptions** -Eigenschaft – Festlegung mithilfe von Werten der **DTSXMLDiffOptions** -Enumeration. Die Optionen in diesem Enumerator schließen sich nicht gegenseitig aus. Stellen Sie eine durch Trennzeichen getrennte Liste der anzuwendenden Optionen bereit, um mehrere Optionen zu verwenden.  
  
|Anzeigename in DTSXMLDiffOptions|Numerischer Wert|  
|----------------------------------------|-------------------|  
|InclusionThresholdSetting|0|  
|IgnoreChildOrder|1|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNamespaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 **DiffAlgorithm** -Eigenschaft – Festlegung mithilfe von Werten der **DTSXMLDiffAlgorithm** -Enumeration.  
  
|Anzeigename in DTSXMLDiffAlgorithm|Numerischer Wert|  
|------------------------------------------|-------------------|  
|Automatisch|0|  
|Fast|1|  
|Precise|2|  
  
##  <a name="MaintenancePlanTasks"></a> Wartungsplantasks  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält eine Reihe von Tasks, mit denen SQL Server-Tasks für die Verwendung in Wartungsplänen und [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen ausgeführt werden.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt nicht die programmgesteuerte Verwendung dieser Tasks, und die Programmierungsreferenzdokumentation enthält keine API-Dokumentation dieser Tasks und ihrer zugehörigen Enumeratoren.  
  
### <a name="all-maintenance-tasks"></a>Alle Wartungstasks  
 Die folgenden Enumerationen werden in allen Wartungstasks verwendet, um die angegebenen Eigenschaften festzulegen.  
  
 **DatabaseSelectionType** -Eigenschaft – Festlegung mithilfe von Werten der **DatabaseSelection** -Enumeration.  
  
|Anzeigename in DatabaseSelection|Numerischer Wert|  
|----------------------------------------|-------------------|  
|InclusionThresholdSetting|0|  
|Alle|1|  
|System|2|  
|Benutzer|3|  
|Specific|4|  
  
 **TableSelectionType** -Eigenschaft – Festlegung mithilfe von Werten der **TableSelection** -Enumeration.  
  
|Anzeigename in TableSelection|Numerischer Wert|  
|-------------------------------------|-------------------|  
|InclusionThresholdSetting|0|  
|Alle|1|  
|Specific|2|  
  
 **ObjectTypeSelection** -Eigenschaft – Festlegung mithilfe von Werten der **ObjectType** -Enumeration.  
  
|Anzeigename in ObjectType|Numerischer Wert|  
|---------------------------------|-------------------|  
|Tabelle|0|  
|Sicht|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>Datenbank sichern (Task)  
 **DestinationCreationType** -Eigenschaft – Festlegung mithilfe von Werten der **DestinationType** -Enumeration.  
  
|Anzeigename in DestinationType|Numerischer Wert|  
|--------------------------------------|-------------------|  
|Automatisch|0|  
|Manuell|1|  
  
 **ExistingBackupsAction** -Eigenschaft – Festlegung mithilfe von Werten der **ActionForExistingBackups** -Enumeration.  
  
|Anzeigename in ActionForExistingBackups|Numerischer Wert|  
|-----------------------------------------------|-------------------|  
|Anfügen|0|  
|Overwrite|1|  
  
 **BackupAction** -Eigenschaft – Festlegung mithilfe von Werten der **BackupTaskType** -Enumeration. Diese Eigenschaft arbeitet mit der **BackupIsIncremental** -Eigenschaft zusammen, um den Typ der vom Task durchgeführten Sicherung zu definieren.  
  
|Anzeigename in BackupTaskType|Numerischer Wert|  
|-------------------------------------|-------------------|  
|Datenbank|0|  
|Dateien|1|  
|Log|2|  
  
 **BackupDevice-Eigenschaft** – Festlegung mithilfe von Werten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DeviceType **-Enumeration von SMO (** Management Objects).  
  
|Anzeigename in DeviceType|Numerischer Wert|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|Band|1|  
|File|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>Wartungscleanup (Task)  
 **FileTypeSelected** -Eigenschaft – Festlegung mithilfe von Werten der **FileType** -Enumeration.  
  
|Anzeigename in FileType|Numerischer Wert|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 **OlderThanTimeUnitType** -Eigenschaft – Festlegung mithilfe von Werten der **TimeUnitType** -Enumeration.  
  
|Anzeigename in TimeUnitType|Numerischer Wert|  
|-----------------------------------|-------------------|  
|Day|0|  
|Week|1|  
|Month|2|  
|Year|3|  
  
### <a name="update-statistics-task"></a>Statistiken aktualisieren (Task)  
 **UpdateType** -Eigenschaft – Festlegung mithilfe von Werten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] StatisticsTarget **-Enumeration von SMO (** Management Objects).  
  
|Anzeigename in StatisticsTarget|Numerischer Wert|  
|---------------------------------------|-------------------|  
|Column|1|  
|Index|2|  
|Alle|3|  
  
##  <a name="CommonProperties"></a> Allgemeine Eigenschaften  
 Pakete, Tasks, die Foreach-Schleife, die For-Schleife und Sequenzcontainer können die folgenden Enumerationen verwenden, um die angegebenen Eigenschaften festzulegen.  
  
 **ForceExecutionResult** -Eigenschaft – Festlegung mithilfe von Werten der **DTSForcedExecResult** -Enumeration.  
  
|Anzeigename in DTSForcedExecResult|Numerischer Wert|  
|------------------------------------------|-------------------|  
|InclusionThresholdSetting|-1|  
|Success|0|  
|Failure|1|  
|Completion|2|  
  
 **IsolationLevel** -Eigenschaft – Festlegung mithilfe der **IsolationLevel** -Enumeration von .NET Framework. Weitere Informationen finden Sie in der .NET Framework-Klassenbibliothek unter der [MSDN Library](http://go.microsoft.com/fwlink?LinkId=17313).  
  
 **LoggingMode** -Eigenschaft – Festlegung mithilfe von Werten der **DTSLoggingMode** -Enumeration.  
  
|Anzeigename in DTSLoggingMode|Numerischer Wert|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|Aktiviert|1|  
|Disabled|2|  
  
 **TransactionOption** -Eigenschaft – Festlegung mithilfe von Werten der **DTSTransactionOption** -Enumeration.  
  
|Anzeigename in DTSTransactionOption|Numerischer Wert|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|Supported|1|  
|Required|2|  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Hinzufügen oder Ändern eines Eigenschaftsausdrucks](../../integration-services/expressions/add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Integrationsservices &#40; SSIS &#41; Pakete](../../integration-services/integration-services-ssis-packages.md)   
 [Integration Services-Container](../../integration-services/control-flow/integration-services-containers.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Rangfolgeneinschränkungen](../../integration-services/control-flow/precedence-constraints.md)  
  
  

