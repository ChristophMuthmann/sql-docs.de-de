---
title: "Verwenden des PowerShell-Anbieters für erweiterte Ereignisse | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9ab01ceaa7208e742d2833a2c368df334f7578fe
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="use-the-powershell-provider-for-extended-events"></a>Verwenden des PowerShell-Anbieters für erweiterte Ereignisse
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Erweiterte Ereignisse von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Sie mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -PowerShell-Anbieters verwalten. Der Unterordner XEvent ist auf dem SQLSERVER-Laufwerk verfügbar. Auf diesen Ordner können Sie mit einer der folgenden Methoden zugreifen:  
  
-   Geben Sie an einer Eingabeaufforderung **sqlps**ein, und drücken Sie anschließend die EINGABETASTE. Geben Sie **cd xevent**ein, und drücken Sie anschließend die EINGABETASTE. Von dort aus können Sie mit den Befehlen **cd** und **dir** (oder mit den Cmdlets **Set-Location** und **Get-Childitem** ) zum Servernamen und Instanznamen wechseln.  
  
-   Erweitern Sie im Objekt-Explorer den Instanznamen, erweitern Sie **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Erweiterte Ereignisse**, und klicken Sie anschließend auf **PowerShell starten**. Damit wird PowerShell unter dem folgenden Pfad gestartet:  
  
     PS SQLSERVER:\XEvent\\*Servername*\\*Instanzname*>  
  
    > [!NOTE]  
    >  PowerShell können Sie unter **Erweiterte Ereignisse**von jedem Knoten aus starten. Sie können z.B. mit der rechten Maustaste auf **Sitzungen**klicken und anschließend auf **PowerShell starten**klicken. Damit starten Sie PowerShell eine Ebene tiefer, mit dem Ordner Sitzungen.  
  
 Sie können die Struktur des Ordners "XEvent" nach vorhandenen Sitzungen für erweiterte Ereignisse und deren zugeordneten Ereignissen, Zielen und Prädikaten durchsuchen. Wenn Sie zum Beispiel unter dem Pfad PS SQLSERVER:\XEvent\\*Servername*\\*Instanzname*> den Befehl **cd sessions** eingeben, die EINGABETASTE drücken, **dir** eingeben und anschließend erneut die EINGABETASTE drücken, zeigen Sie die Liste der in dieser Instanz gespeicherten Sitzungen an. Sie können auch anzeigen, ob die Sitzung ausgeführt wird (und wenn dies der Fall ist, die bisherige Sitzungsdauer), sowie ob die Sitzung für den Start bei Instanzstart konfiguriert ist.  
  
 Wenn Sie die Ereignisse, deren Prädikate und die einer Sitzung zugeordneten Ziele anzeigen möchten, können Sie Verzeichnisse in den Sitzungsnamen ändern und dann den Ereignis- oder den Zielordner anzeigen. Um zum Beispiel die Ereignisse und deren Prädikate anzuzeigen, die der Standard-Systemintegritätssitzung zugeordnet sind, geben Sie unter dem Pfad PS SQLSERVER:\XEvent\\*Servername*\\*Instanzname*\Sessions> den Befehl **cd system_health\events,** ein, drücken Sie die EINGABETASTE, geben Sie **dir** ein, und drücken Sie anschließend erneut die EINGABETASTE.  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-PowerShell-Anbieter ist ein leistungsstarkes Tool, mit dem Sie Sitzungen für erweiterte Ereignisse erstellen, ändern und verwalten können. Der folgende Abschnitt enthält einige einfache Beispiele für die Verwendung von PowerShell-Skripts mit erweiterten Ereignissen.  
  
## <a name="examples"></a>Beispiele  
 Achten Sie in den folgenden Beispielen auf Folgendes:  
  
-   Die Skripts müssen an der Eingabeaufforderung von PS SQLSERVER:\\> ausgeführt werden (verfügbar, wenn Sie an einer Eingabeaufforderung **sqlps** eingeben).  
  
-   Die Skripts verwenden die Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Die Skripts müssen mit der Erweiterung .ps1 gespeichert werden.  
  
-   In der PowerShell-Ausführungsrichtlinie muss das auszuführende Skript zugelassen sein. Verwenden Sie das Cmdlet **Set-Executionpolicy** , um die Ausführungsrichtlinie festzulegen. (Weitere Informationen erhalten Sie, wenn Sie **get-help set-executionpolicy -detailed**eingeben und anschließend die EINGABETASTE drücken.)  
  
 Mit dem folgenden Skript erstellen Sie die neue Sitzung "TestSession".  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 Das folgende Skript fügt der im vorherigen Beispiel erstellten Sitzung das Ringpufferziel hinzu. (In diesem Beispiel wird die Verwendung der **Alter** -Methode veranschaulicht. Sie können das Ziel beim Erstellen der Sitzung hinzufügen.)  
  
```  
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir|where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 Mit dem folgenden Skript erstellen Sie eine neue Sitzung, in der ein Prädikatausdruck verwendet wird. In diesem Fall werden in der Sitzung Informationen gesammelt, die in die Datei „c:\temp.log“ geschrieben werden (über das Ereignis „sqlserver.file_written“).  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -argumentlist $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a>Sicherheit  
 Zum Erstellen, Ändern oder Löschen einer Sitzung für erweiterte Ereignisse müssen Sie über die ALTER ANY EVENT SESSION-Berechtigung verfügen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [Verwenden der system_health-Sitzung](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [Tools für erweiterte Ereignisse](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
