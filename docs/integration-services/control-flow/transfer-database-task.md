---
title: "Übertragen Sie die Task \"Datenbank\" | Microsoft Docs"
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
- sql13.dts.designer.transferdatabasetask.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 86e2b602632d1492d3889981af041c5ee38cfb6b
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

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
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „Datenbanken übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)  
  
-   [Editor für den Task „Datenbanken übertragen“ &#40;Seite „Datenbanken“&#41;](../../integration-services/control-flow/transfer-database-task-editor-databases-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>Programmgesteuerte Konfiguration des Tasks "Datenbank übertragen"  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
  
