---
title: "Übertragen Sie die Task \"Datenbank\" | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferdatabasetask.f1
- sql13.dts.designer.transferdatabasetask.general.f1
- sql13.dts.designer.transferdatabasetask.database.f1
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
- sql13.dts.designer.transferdatabasetask.destdbfiles.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 29f66d1eeed7e2af0df962b62020169fb2095f6e
ms.contentlocale: de-de
ms.lasthandoff: 08/11/2017

---
# <a name="transfer-database-task"></a>Datenbanken übertragen (Task)
  Der Task "Datenbanken übertragen" verschiebt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank zwischen zwei Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Im Gegensatz zu den anderen Tasks, die lediglich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte durch Kopieren verschieben, kann der Task "Datenbanken übertragen" eine Datenbank entweder kopieren oder verschieben. Dieser Task kann auch verwendet werden, um eine Datenbank innerhalb desselben Servers zu kopieren.  
  
## <a name="offline-and-online-modes"></a>Offline- und Onlinemodi  
 Die Datenbank kann im Online- oder im Offlinemodus übertragen werden. Wenn Sie den Onlinemodus verwenden, bleibt die Datenbank verbunden und wird mithilfe des SMO-Objekts (SQL Management Object) zum Kopieren der Datenbankobjekte übertragen. Wenn Sie im Offlinemodus arbeiten, wird die Datenbankverbindung getrennt, die Datenbankdateien werden kopiert oder verschoben, und die Datenbank wird am Ziel verbunden, nachdem die Übertragung erfolgreich abgeschlossen wurde. Wenn die Datenbank kopiert wird, wird sie automatisch an der Quelle neu verbunden, falls der Kopiervorgang erfolgreich ist. Im Offlinemodus wird die Datenbank schneller kopiert, sie steht jedoch den Benutzern während der Übertragung nicht zur Verfügung.  
  
 Im Offlinemodus müssen Sie die Netzwerkdateifreigaben auf den Quell- und Zielservern angeben, auf denen sich die Datenbankdateien befinden. Ist der Ordner freigegeben und kann vom Benutzer darauf zugegriffen werden, können Sie auf die Netzwerkfreigabe mithilfe der Syntax \\\Computername\Programme\meinOrdner\\verweisen. Andernfalls müssen Sie die Syntax \\\Computername\c$\Programme\meinOrdner\\verwenden. Um diese Syntax zu verwenden, muss der Benutzer Schreibzugriff auf die Quell- und Zielnetzwerkfreigaben haben.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>Übertragung von Datenbanken zwischen verschiedenen Versionen von SQL Server  
 Der Task "Datenbank übertragen" kann eine Datenbank zwischen Instanzen verschiedener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Versionen übertragen.  
  
## <a name="events"></a>Ereignisse  
 Der Task "Datenbanken übertragen" meldet keinen schrittweisen Fortschritt der Fehlermeldungsübertragung; er meldet nur 0 % und 100 % der Ausführung.  
  
## <a name="execution-value"></a>Ausführungswert  
 Der in der **ExecutionValue** -Eigenschaft des Tasks definierte Ausführungswert gibt den Wert 1 zurück, da der Task "Datenbank übertragen" im Gegensatz zu anderen Übertragungstasks nur eine Datenbank übertragen kann.  
  
 Indem der **ExecValueVariable**-Eigenschaft des Tasks „Datenbanken übertragen“ eine benutzerdefinierte Variable zugewiesen wird, können Informationen über die Fehlermeldungsübertragung anderen Objekten im Paket zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Protokolleinträge  
 Der Task "Datenbanken übertragen" enthält die folgenden benutzerdefinierten Protokolleinträge:  
  
-   SourceSQLServer    Dieser Protokolleintrag gibt den Namen des Quellservers an.  
  
-   DestSQLServer    Dieser Protokolleintrag gibt den Namen des Zielservers an.  
  
-   SourceDB    Dieser Protokolleintrag gibt den Namen der übertragenen Datenbank an.  
  
 Außerdem wird beim Überschreiben der Zieldatenbank ein Protokolleintrag für das **OnInformation** -Ereignis geschrieben.  
  
## <a name="security-and-permissions"></a>Sicherheit und Berechtigungen  
 Wenn Sie eine Datenbank im Offlinemodus übertragen, muss der Benutzer, der das Paket ausführt, Mitglied der sysadmin-Serverrolle sein.  
  
 Um eine Datenbank im Onlinemodus zu übertragen, muss der Benutzer, der das Paket ausführt, Mitglied der sysadmin-Serverrolle oder Datenbankbesitzer (dbo) der ausgewählten Datenbank sein.  
  
## <a name="configuration-of-the-transfer-database-task"></a>Konfiguration des Tasks "Datenbank übertragen"  
 Sie können angeben, ob der Task versucht, eine erneute Verbindung mit der Quelldatenbank herzustellen, falls die Datenbankübertragung fehlschlägt.  
  
 Der Task "Datenbank übertragen" kann auch so konfiguriert werden, dass das Überschreiben einer Zieldatenbank mit demselben Namen nicht zulässig ist und die Zieldatenbank ersetzt wird.  
  
 Die Quelldatenbank kann als Teil des Übertragungsprozesses ebenfalls umbenannt werden. Wenn Sie eine Datenbank in eine Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] übertragen möchten, die bereits eine Datenbank mit demselben Namen enthält, kann die Datenbank durch Umbenennen der Quelldatenbank übertragen werden. Die Dateinamen der Datenbank müssen jedoch auch verschieden sein. Wenn bereits Datenbankdateien mit denselben Namen am Ziel vorhanden sind, schlägt der Task fehl.  
  
 Wenn Sie eine Datenbank kopieren, kann die Datenbank nicht kleiner als die **model** -Datenbank auf dem Zielserver sein. Sie können entweder die zu kopierende Datenbank vergrößern, oder die Größe der **model**-Datenbank reduzieren.  
  
 Zur Laufzeit stellt der Task "Datenbank übertragen" eine Verbindung mit den Quell- und Zielservern her. Dazu werden ein oder zwei SMO-Verbindungs-Manager verwendet. Wenn Sie eine Datenbankkopie auf demselben Server erstellen, wird nur ein SMO-Verbindungs-Manager benötigt. Die SMO-Verbindungs-Manager werden getrennt vom Task "Datenbanken übertragen" konfiguriert. Es wird darauf dann im Task "Datenbank übertragen" verwiesen. Die SMO-Verbindungs-Manager geben den Server- und Authentifizierungsmodus an, der beim Zugriff auf den Server verwendet werden soll. Weitere Informationen finden Sie unter [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>Programmgesteuerte Konfiguration des Tasks "Datenbank übertragen"  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
## <a name="transfer-database-task-editor-general-page"></a>Editor für den Task Datenbanken übertragen (Seite Allgemein)
  Mithilfe der Seite **Allgemein** des Dialogfelds **Editor für den Task 'Datenbanken übertragen'** können Sie den Task Datenbanken übertragen benennen und beschreiben. Der Task Datenbanken übertragen kopiert oder verschiebt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank zwischen zwei Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dieser Task kann auch verwendet werden, um eine Datenbank innerhalb desselben Servers zu kopieren.   
  
### <a name="options"></a>enthalten  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Task Datenbanken übertragen ein. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung für den Task Datenbanken übertragen ein.  
  
## <a name="transfer-database-task-editor-databases-page"></a>Editor für den Task Datenbanken übertragen (Seite Datenbanken)
  Verwenden Sie die Seite **Datenbanken** des Dialogfelds **Editor für den Task Datenbanken übertragen** , um die Eigenschaften für die im Task Datenbanken übertragen verwendeten Quell- und Zieldatenbanken anzugeben. Der Task Datenbanken übertragen kopiert oder verschiebt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank zwischen zwei Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dieser Task kann auch verwendet werden, um eine Datenbank innerhalb desselben Servers zu kopieren.  
  
### <a name="options"></a>enthalten  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager, oder klicken Sie auf  **\<neue Verbindung... >** um eine neue Verbindung mit dem Quellserver zu erstellen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager, oder klicken Sie auf  **\<neue Verbindung... >** um eine neue Verbindung mit dem Zielserver zu erstellen.  
  
 **DestinationDatabaseName**  
 Geben Sie den Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank auf dem Zielserver an.  
  
 Um dieses Feld automatisch mit dem Namen der Quelldatenbank aufzufüllen, geben Sie zuerst die **SourceConnection** (Quellverbindung) und den **SourceDatabaseName** (Quelldatenbanknamen) an.  
  
 Um die Datenbank auf dem Zielserver umzubenennen, geben Sie in diesem Feld den neuen Namen an.  
  
 **DestinationDatabaseFiles**  
 Gibt die Namen und Speicherorte der Datenbankdateien auf dem Zielserver an.  
  
 Um dieses Feld automatisch mit den Namen und Speicherorten der Quelldatenbankdateien aufzufüllen, geben Sie zuerst die **SourceConnection**(Quellverbindung), den **SourceDatabaseName**(Quelldatenbanknamen) und die **SourceDatabaseFiles** (Quelldatenbankdateien) an.  
  
 Um die Datenbankdateien umzubenennen oder neue Speicherorte auf dem Zielserver anzugeben, tragen Sie in diesem Feld die Quelldatenbankinformationen ein und klicken dann auf die Schaltfläche zum Durchsuchen. Bearbeiten Sie im Dialogfeld **Zieldatenbankdateien** die Einträge für **Zieldatei**, **Zielordner**oder **Netzwerkdateifreigabe**.  
  
> [!NOTE]  
>  Wenn Sie die Datenbankdateien über die Schaltfläche zum Durchsuchen auswählen, wird der Dateispeicherort in der Notation des lokalen Laufwerks angegeben, z.B. C:\\. Diese müssen Sie durch die Notation der Netzwerkfreigabe ersetzen, einschließlich des Computernamens und des Freigabenamens. Wenn die standardmäßige Administrationsfreigabe verwendet wird, müssen Sie die $-Notation verwenden und über Administratorzugriff auf die Freigabe verfügen.  
  
 **DestinationOverwrite**  
 Geben Sie an, ob die Datenbank auf dem Zielserver überschrieben werden kann.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Zielserverdatenbank überschreiben.|  
|**False**|Zielserverdatenbank nicht überschreiben.|  
  
> [!CAUTION]  
>  Die Daten in der Zielserverdatenbank werden überschrieben, wenn Sie für **DestinationOverwrite** **True**angeben. Dies kann zu Datenverlusten führen. Um dies zu vermeiden, sollten Sie die Zielserverdatenbank an einem anderen Speicherort sichern, bevor Sie den Task Datenbanken übertragen ausführen.  
  
 **Aktion**  
 Gibt an, ob der Task die Datenbank auf den Zielserver kopiert ( **Kopieren** ) oder verschiebt ( **Verschieben** ).  
  
 **Methode**  
 Gibt an, ob der Task ausgeführt wird, während sich die Datenbank auf dem Quellserver im Online- oder Offlinemodus befindet.  
  
 Um eine Datenbank im Offlinemodus zu übertragen, muss der Benutzer, der das Paket ausführt, ein Mitglied der festen Serverrolle **sysadmin** sein.  
  
 Um eine Datenbank im Onlinemodus zu übertragen, muss der Benutzer, der das Paket ausführt, ein Mitglied der festen Serverrolle **sysadmin** oder der Besitzer (**dbo**) der ausgewählten Datenbank sein.  
  
 **SourceDatabaseName**  
 Wählen Sie den Namen der zu kopierenden oder zu verschiebenden Datenbank aus.  
  
 **SourceDatabaseFiles**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen, um die Datenbankdateien auszuwählen.  
  
 **ReattachSourceDatabase**  
 Geben Sie an, ob der Task versuchen soll, die Quelldatenbank wieder anzufügen, falls ein Fehler auftritt.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Quelldatenbank wieder anfügen.|  
|**False**|Quelldatenbank nicht wieder anfügen.|  

## <a name="source-database-files"></a>Quelldatenbankdateien
  Verwenden Sie das Dialogfeld **Quelldatenbankdateien** , um die Namen und Speicherorte der Datenbankdateien auf dem Quellserver anzuzeigen, oder um für den Task "Datenbanken übertragen" eine Dateifreigabe auf dem Netzwerk anzugeben.   
  
 Um dieses Dialogfeld mit den Datenbankdateinamen und -speicherorten des Quellservers aufzufüllen, geben Sie zuerst auf der Seite **Datenbanken** des Dialogfelds **Editor für den Task 'Datenbanken übertragen'** die Parameter **SourceConnection** und **SourceDatabaseName** an.  
  
### <a name="options"></a>enthalten  
 **Quelldatei**  
 Die Namen der zu übertragenden Datenbankdateien auf dem Quellserver. **Quelldatei** ist schreibgeschützt.  
  
 **Quellordner**  
 Der Ordner auf dem Quellserver, in dem sich die zu übertragenden Datenbankdateien befinden. **Quellordner** ist schreibgeschützt.  
  
 **Netzwerkdateifreigabe**  
 Der auf dem Netzwerk freigegebene Ordner auf dem Quellserver, aus dem die Datenbankdateien übertragen werden sollen. Verwenden Sie **Netzwerkdateifreigabe** , wenn Sie eine Datenbank im Offlinemodus übertragen, indem Sie auf der Seite **Datenbanken** des Dialogfelds **Editor für den Task 'Datenbanken übertragen'** als **Methode** **DatabaseOffline** angeben.  
  
 Geben Sie den Speicherort der Netzwerkdateifreigabe ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , um zu dieser Netzwerkdateifreigabe zu navigieren.  
  
 Beim Übertragen einer Datenbank im Offlinemodus werden die Datenbankdateien zunächst in den als **Netzwerkdateifreigabe** angegebenen Speicherort auf dem Quellserver kopiert, bevor sie auf den Zielserver übertragen werden.  

## <a name="destination-database-files"></a>Zieldatenbankdateien
  Verwenden Sie das Dialogfeld **Zieldatenbankdateien** , um die Namen und Speicherorte der Datenbankdateien auf dem Zielserver anzuzeigen oder um für den Task "Datenbanken übertragen" eine Dateifreigabe auf dem Netzwerk anzugeben.  
  
 Um dieses Dialogfeld automatisch mit den Datenbankdateinamen und -speicherorten des Quellservers aufzufüllen, geben Sie zuerst auf der Seite **Datenbanken**des Dialogfelds **Editor für den Task 'Datenbanken übertragen'**die Parameter **SourceConnection** , **SourceDatabaseName** und **SourceDatabaseFiles** an.  
  
### <a name="options"></a>enthalten  
 **Zieldatei**  
 Namen der übertragenen Datenbankdateien auf dem Zielserver.  
  
 Geben Sie den Dateinamen ein, oder klicken Sie darauf, um ihn zu bearbeiten.  
  
 **Zielordner**  
 Der Ordner auf dem Zielserver, in den die Datenbankdateien übertragen werden sollen.  
  
 Geben Sie den Ordnerpfad auf dem Zielserver ein, klicken Sie darauf, um ihn zu bearbeiten, oder klicken Sie auf die Schaltfläche zum Durchsuchen, um zu dem Ordner zu navigieren, in den Sie die Datenbankdateien übertragen wollen.  
  
 **Netzwerkdateifreigabe**  
 Die Netzwerkdateifreigabe auf dem Zielserver, in die die Datenbankdateien übertragen werden sollen. Verwenden Sie **Netzwerkdateifreigabe** , wenn Sie eine Datenbank im Offlinemodus übertragen, indem Sie auf der Seite **Datenbanken** des Dialogfelds **Editor für den Task 'Datenbanken übertragen'** als **Methode** **DatabaseOffline** angeben.  
  
 Geben Sie den Speicherort der Netzwerkdateifreigabe ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen, um zu dieser Netzwerkdateifreigabe zu navigieren.  
  
 Beim Übertragen einer Datenbank im Offlinemodus werden die Datenbankdateien zunächst in den als **Netzwerkdateifreigabe** angegebenen Speicherort kopiert, bevor sie in den als **Zielordner** gekennzeichneten Speicherort übertragen werden.  

