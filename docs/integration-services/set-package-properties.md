---
title: "Festlegen von Paketeigenschaften | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services-Pakete, Eigenschaften"
  - "Eigenschaften [Integration Services]"
  - "Prüfpunkte [Integration Services]"
  - "Ausführungseigenschaften [Integration Services]"
  - "Pakete [Integration Services], Eigenschaften"
  - "Identifizierungseigenschaften [Integration Services]"
  - "Kennwörter [Integration Services]"
  - "SSIS-Pakete, Eigenschaften"
  - "Transaktionseigenschaften [Integration Services]"
  - "Aktualisieren von Paketeigenschaften"
  - "Eigenschaften erzwungener Ausführungswerte [Integration Services]"
  - "Sicherheitseigenschaften [Integration Services]"
  - "Versionseigenschaften [Integration Services]"
  - "SQL Server Integration Services-Pakete, Eigenschaften"
ms.assetid: 13f81c3e-2b18-4f83-b445-a2f4a2c560aa
caps.latest.revision: 40
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Festlegen von Paketeigenschaften
  Wenn Sie ein Paket in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] mithilfe der grafischen Benutzeroberfläche von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] erstellen, legen Sie die Eigenschaften des Paketobjekts im Eigenschaftenfenster fest.  
  
 Das Fenster **Eigenschaften** stellt eine kategorisierte und alphabetische Liste der Eigenschaften bereit. Klicken Sie auf das Nach Kategorien-Symbol, um das Fenster **Eigenschaften** nach der Kategorie anzuordnen.  
  
 Bei der Anordnung nach der Kategorie werden die Eigenschaften im Fenster **Eigenschaften** in den folgenden Kategorien gruppiert:  
  
-   [Prüfpunkte](#Checkpoints)  
  
-   [Ausführung](#Execution)  
  
-   [Erzwungener Ausführungswert](#ForcedExecutionValue)  
  
-   [Identifikation](#Identification)  
  
-   [Sonstiges](#Misc)  
  
-   [Security](#Security)  
  
-   [Transaktionen](#Transactions)  
  
-   [Version](#Version)  
  
 Informationen zu zusätzlichen Paketeigenschaften, die Sie im Fenster **Eigenschaften** nicht festlegen können, finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.Package>.  
  
### So legen Sie Paketeigenschaften im Eigenschaftenfenster fest.  
  
-   [Festlegen der Eigenschaften eines Pakets](../Topic/Set%20the%20Properties%20of%20a%20Package.md)  
  
## Eigenschaften nach Kategorie  
 In den folgenden Tabellen sind die Paketeigenschaften nach Kategorie aufgelistet.  
  
###  <a name="Checkpoints"></a> Prüfpunkte  
 Mit den Eigenschaften in dieser Kategorie können Sie das Paket von dem Punkt an, an dem der Fehler in der Paketablaufsteuerung auftrat, neu starten, anstatt das Paket vom Beginn der Ablaufsteuerung erneut auszuführen. Weitere Informationen finden Sie unter [Restart Packages by Using Checkpoints](../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**CheckpointFileName**|Der Name der Datei, die die Prüfpunktinformationen aufzeichnet, mit der ein Paket neu gestartet werden kann. Wenn das Paket erfolgreich ausgeführt wurde, wird diese Datei gelöscht.|  
|**CheckpointUsage**|Gibt an, wann ein Paket neu gestartet werden kann. Mögliche Werte sind **Never**, **IfExists**und **Always**. Der Standardwert dieser Eigenschaft ist **Never**, mit dem das Paket nicht neu gestartet werden kann. Weitere Informationen finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>.|  
|**SaveCheckpoints**|Gibt an, ob die Prüfpunkte in die Prüfpunktdatei geschrieben werden, wenn das Paket ausgeführt wird. Der Standardwert dieser Eigenschaft ist **False**.|  
  
> [!NOTE]  
>  Das Festlegen der Prüfpunktausführungsoption **/CheckPointing** von dtexec auf „on“ entspricht der **SaveCheckpoints**-Eigenschaft des Pakets „True“ oder der **CheckpointUsage**-Eigenschaft „Immer“. Weitere Informationen finden Sie unter [dtexec Utility](../integration-services/packages/dtexec-utility.md).  
  
###  <a name="Execution"></a> Ausführung  
 Mit den Eigenschaften in dieser Kategorie wird das Laufzeitverhalten des Paketobjekts konfiguriert.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**DelayValidation**|Zeigt an, ob die Paketüberprüfung bis zur Ausführung des Pakets verschoben wird. Der Standardwert dieser Eigenschaft ist **False**.|  
|**Deaktivieren**|Zeigt an, ob das Paket deaktiviert ist. Der Standardwert dieser Eigenschaft ist **False**.|  
|**DisableEventHandlers**|Gibt an, ob die Paketereignishandler ausgeführt werden. Der Standardwert dieser Eigenschaft ist **False**.|  
|**FailPackageOnFailure**|Gibt an, ob das Paket bei einem Fehler in einer Paketkomponente fehlschlägt. Der einzige gültige Wert dieser Eigenschaft ist **False**.|  
|**FailParentOnError**|Gibt an, ob der übergeordnete Container bei einem Fehler in einem untergeordneten Container fehlschlägt. Der Standardwert dieser Eigenschaft ist **False**.|  
|**MaxConcurrentExecutables**|Die Anzahl von ausführbaren Dateien, die das Paket gleichzeitig ausführen kann. Der Standardwert dieser Eigenschaft ist **-1**, mit dem es kein Limit gibt.|  
|**MaximumErrorCount**|Die maximale zulässige Anzahl von Fehlern, nach der die Ausführung eines Pakets beendet wird. Der Standardwert dieser Eigenschaft ist **1**.|  
|**PackagePriorityClass**|Die Win32-Threadprioritätsklasse des Paketthreads. Mögliche Werte sind **Default**, **AboveNormal**, **Normal**, **BelowNormal**und **Idle**. Der Standardwert dieser Eigenschaft ist **Default**. Weitere Informationen finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>.|  
  
###  <a name="ForcedExecutionValue"></a> Erzwungener Ausführungswert  
 Mit den Eigenschaften in dieser Kategorie wird ein optionaler Ausführungswert für das Paket konfiguriert.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**ForcedExecutionValue**|Ein Wert, der den vom Paket zurückgegebenen optionalen Ausführungswert angibt, falls ForceExecutionValue auf **TRUE** festgelegt ist. Der Standardwert dieser Eigenschaft ist **0**.|  
|**ForcedExecutionValueType**|Der Datentyp von ForcedExecutionValue. Der Standardwert dieser Eigenschaft ist **Int32**.|  
|**ForceExecutionValue**|Ein boolescher Wert, der angibt, ob ein bestimmter optionaler Ausführungswert des Containers erzwungen werden soll. Der Standardwert dieser Eigenschaft ist **False**.|  
  
###  <a name="Identification"></a> Identifikation  
 Mit den Eigenschaften in dieser Kategorie werden Informationen bereitgestellt, wie z. B. der eindeutige Bezeichner und der Name des Pakets.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**CreationDate**|Das Datum, an dem das Paket erstellt wurde.|  
|**CreatorComputerName**|Der Name des Computers, auf dem das Paket erstellt wurde.|  
|**CreatorName**|Der Name der Person, die das Paket erstellt hat.|  
|**Description**|Eine Beschreibung der Paketfunktionalität.|  
|**ID**|Der Paket-GUID, der dem Paket beim Erstellen zugewiesen wird. Diese Eigenschaft ist schreibgeschützt. Um einen neuen Zufallswert für die **ID**-Eigenschaft zu generieren, wählen Sie **\<Neue ID generieren>** in der Dropdownliste aus.|  
|**Name**|Der Name des Pakets.|  
|**PackageType**|Der Pakettyp. Mögliche Werte sind **Default**, **DTSDesigner**, **DTSDesigner100**, **DTSWizard**, **SQLDBMaint**und **SQLReplication**. Der Standardwert dieser Eigenschaft ist **Default**. Weitere Informationen finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>.|  
  
###  <a name="Misc"></a> Sonstiges  
 Mit den Eigenschaften in dieser Kategorie wird auf Konfigurationen und Ausdrücke zugegriffen, die von einem Paket verwendet werden. Außerdem werden Informationen zum Gebietsschema und zum Protokollierungsmodus des Pakets bereitgestellt. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../integration-services/expressions/use-property-expressions-in-packages.md).  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Konfigurationen**|Die Auflistung mit Konfigurationen, die vom Paket verwendet werden. Klicken Sie auf die Schaltfläche zum Durchsuchen **(…)**, um Paketkonfigurationen anzuzeigen und zu konfigurieren.|  
|**Ausdrücke**|Klicken Sie auf die Schaltfläche zum Durchsuchen **(…)**, um Ausdrücke für Paketeigenschaften zu erstellen.<br /><br /> Beachten Sie, dass Sie Eigenschaftsausdrücke für alle Paketeigenschaften dieses Objektmodells erstellen können, nicht nur für die im Eigenschaftenfenster aufgeführten Eigenschaften.<br /><br /> Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../integration-services/expressions/use-property-expressions-in-packages.md).<br /><br /> Erweitern Sie **Expressions**, um vorhandene Eigenschaftsausdrücke anzuzeigen. Klicken Sie in einem Ausdruckstextfeld auf die Schaltfläche zum Durchsuchen **(…)**, um einen Ausdruck zu ändern und auszuwerten.|  
|**ForceExecutionResult**|Das Ausführungsergebnis des Pakets. Mögliche Werte sind **None**, **Success**, **Failure**und **Completion**. Der Standardwert dieser Eigenschaft ist **None**. Weitere Informationen finden Sie unter T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult.|  
|**LocaleId**|Ein Microsoft Win32-Gebietsschema. Der Standardwert dieser Eigenschaft ist das Gebietsschema des Betriebssystems auf dem lokalen Computer.|  
|**LoggingMode**|Ein Wert, der das Protokollierungsverhalten des Pakets angibt. Mögliche Werte sind **Disabled**, **Enabled**und **UseParentSetting**. Der Standardwert dieser Eigenschaft ist **UseParentSetting**. Weitere Informationen finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|**OfflineMode**|Gibt an, ob sich das Paket im Offlinemodus befindet. Diese Eigenschaft ist schreibgeschützt. Die Eigenschaft wird auf Projektebene festgelegt. Normalerweise versucht der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer eine Verbindung mit jeder Datenquellen herzustellen, die von dem Paket verwendet wird, um die den Quellen und Zielen zugeordneten Metadaten zu überprüfen. Wenn die Datenquellen nicht verfügbar sind, können Sie diese Verbindungsversuche und die resultierenden Überprüfungsfehler verhindern, indem Sie vor dem Öffnen eines Pakets im Menü **SSIS** die Option **Offline arbeiten** aktivieren. Sie können die Option **Offline arbeiten** auch aktivieren, um die Vorgänge im Designer zu beschleunigen, und sie lediglich zum Überprüfen des Pakets deaktivieren.|  
|**SuppressConfigurationWarnings**|Zeigt an, ob die von Konfigurationen generierten Warnungen unterdrückt werden. Der Standardwert dieser Eigenschaft ist **False**.|  
|**UpdateObjects**|Zeigt an, ob das Paket aktualisiert wird, um neuere Versionen der vorhandenen Objekte zu verwenden, falls neuere Versionen verfügbar sind. Beispielsweise wird ein Paket mit einem Masseneinfügungstask aktualisiert, wenn diese Eigenschaft auf **TRUE** festgelegt ist, damit die neuere Version des Masseneinfügungstasks von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] verwendet wird. Der Standardwert dieser Eigenschaft ist **False**.|  
  
###  <a name="Security"></a> Security  
 Mit den Eigenschaften in dieser Kategorie wird die Schutzebene des Pakets konfiguriert. Weitere Informationen finden Sie unter [Access Control for Sensitive Data in Packages](../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**PackagePassword**|Das Kennwort für Paketschutzebenen (**EncryptSensitiveWithPassword** und **EncryptAllWithPassword**), die Kennwörter erfordern.|  
|**ProtectionLevel**|Die Schutzebene des Pakets. Mögliche Werte sind **DontSaveSensitive**, **EncryptSensitiveWithUserKey**, **EncryptSensitiveWithPassword**, **EncryptAllWithPassword**und **ServerStorage**. Der Standardwert dieser Eigenschaft ist **EncryptSensitiveWithUserKey**. Weitere Informationen finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>.|  
  
###  <a name="Transactions"></a> Transaktionen  
 Mit den Eigenschaften in dieser Kategorie werden die Isolationsstufe und die Transaktionsoption des Pakets konfiguriert. Weitere Informationen finden Sie unter [Integration Services-Transaktionen](../integration-services/integration-services-transactions.md).  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**IsolationLevel**|Die Isolationsstufe der Pakettransaktionen. Mögliche Werte sind **Unspecified**, **Chaos**, **ReadUncommitted**, **ReadCommitted**, **RepeatableRead** **Serializable**und **Snapshot**. Der Standardwert dieser Eigenschaft ist **Serializable**.<br /><br /> Hinweis: Der Wert **Momentaufnahme** der Eigenschaft **IsolationLevel** ist mit Pakettransaktionen nicht kompatibel. Daher können Sie die **IsolationLevel** -Eigenschaft nicht verwenden, um die Isolationsstufe von Pakettransaktionen auf **Shapshot**festzulegen. Verwenden Sie stattdessen eine SQL-Abfrage, um Pakettransaktionen auf **Snapshot**festzulegen. Weitere Informationen finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md).<br /><br /> Das System wendet die **IsolationLevel** -Eigenschaft nur dann auf Pakettransaktionen an, wenn der Wert der **TransactionOption** -Eigenschaft auf **Required**festgelegt ist.<br /><br /> Der Wert der von einem untergeordneten Container angeforderten **IsolationLevel** -Eigenschaft wird ignoriert, wenn die folgenden Bedingungen erfüllt sind:<br />Der Wert der **TransactionOption** -Eigenschaft des untergeordneten Containers ist **Supported**.<br />Der untergeordnete Container nimmt an der Transaktion eines übergeordneten Containers teil.<br /><br /> Der Wert der vom Container angeforderten **IsolationLevel** -Eigenschaft wird nur berücksichtigt, wenn der Container eine neue Transaktion initiiert. Ein Container initiiert eine neue Transaktion, wenn die folgenden Bedingungen erfüllt sind:<br />Der Wert der **TransactionOption** -Eigenschaft des Containers ist **Required**.<br />Der übergeordnete Container hat nicht bereits eine Transaktion gestartet.<br /><br /> <br /><br /> Weitere Informationen finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|**TransactionOption-**|Die Transaktionsteilnahme des Pakets. Mögliche Werte sind **NotSupported**, **Supported**und **Required**. Der Standardwert dieser Eigenschaft ist **Supported**. Weitere Informationen finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
###  <a name="Version"></a> Version  
 Mit den Eigenschaften in dieser Kategorie werden Informationen zur Version des Paketobjekts bereitgestellt.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**VersionBuild**|Die Versionsnummer des Paketbuilds.|  
|**VersionComments**|Kommentare zur Paketversion.|  
|**VersionGUID**|Der GUID der Paketversion. Diese Eigenschaft ist schreibgeschützt.|  
|**VersionMajor**|Die aktuelle Hauptversion des Pakets.|  
|**VersionMinor**|Die aktuelle Nebenversion des Pakets.|  
  
  