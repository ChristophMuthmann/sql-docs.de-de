---
title: MSSQLSERVER_8992 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: a60080ff9db09713061a43810be4c641c68ea343
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver8992"></a>MSSQLSERVER_8992
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|8992|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC3_CHECK_CATALOG|  
|Meldungstext|Meldung ERROR zum Prüfen des Katalogs, Ebene LEVEL, Status STATE: MESSAGE.|  
  
## <a name="explanation"></a>Erklärung  
DBCC CHECKCATALOG oder DBCC CHECKDB hat in den Systemmetadatentabellen eine Inkonsistenz für das angegebene Objekt festgestellt. Es handelt sich um eine Inkonsistenz zwischen der aufgezeichneten Objekt-ID und dem in der Fehlermeldung angegebenen Objekt.  
  
Dieser Fehler kann auftreten, wenn eine oder mehrere Systemtabellen manuell auf eine Weise aktualisiert wurden, die in den Systemmetadaten eine Inkonsistenz verursacht. Zum Beispiel hat ein Benutzer möglicherweise manuell ein Objekt aus der Tabelle **sysobjects** gelöscht, ohne die zugeordneten Zeilen in anderen Tabellen, z.B. **sysindexes** und **syscolumns**, zu entfernen.  
  
Dieser Fehler kann beim Ausführen von DBCC CHECKDB für eine Datenbank auftreten, die von SQL Server 2000 auf SQL Server 2005 oder höher aktualisiert wurde. In SQL Server 2000 enthält DBCC CHECKDB die DBCC CHECKCATALOG-Funktion nicht. Deshalb wird der Fehler nicht vor dem Upgrade abgefangen, es sei denn, DBCC CHECKCATALOG wurde ausdrücklich für die Datenbank in SQL Server 2000 ausgeführt.  
  
In Verbindung mit Fehler 8992 werden möglicherweise folgende Fehler angezeigt:  
  
Meldung 3851 – Eine ungültige Zeile (%ls) wurde in der sys.%ls%ls-Systemtabelle gefunden.  
  
Meldung 3852 – Für die Zeile (%ls) in sys.%ls%ls ist keine entsprechende Zeile (%ls) in sys.%ls%ls vorhanden.  
  
3853 – Für das Attribut (%ls) der Zeile (%ls) in sys.%ls%ls ist keine entsprechende Zeile (%ls) in sys.%ls%ls vorhanden.  
  
3854 – Für das Attribut (%ls) der Zeile (%ls) in sys.%ls%ls ist eine entsprechende Zeile (%ls) in sys.%ls%ls vorhanden, sie ist jedoch ungültig.  
  
3855 – Das Attribut (%ls) ist ohne eine Zeile (%ls) in sys.%ls%ls vorhanden.  
  
3856 – Das Attribut (%ls) ist fälschlicherweise für die Zeile (%ls) in sys.%ls%ls vorhanden.  
  
3857 – Das Attribut (%ls) ist für die Zeile (%ls) in sys.%ls%ls erforderlich, fehlt jedoch.  
  
3858 – Das Attribut (%ls) der Zeile (%ls) in sys.%ls%ls weist einen ungültigen Wert auf.  
  
## <a name="user-action"></a>Benutzeraktion  
  
### <a name="drop-and-re-create-the-specified-object"></a>Löschen und Neuerstellen des angegebenen Objekts  
Wenn möglich, löschen Sie das angegebene Objekt, und erstellen Sie es erneut. Wenn das Objekt z. B. eine gespeicherte Prozedur oder ein benutzerdefinierter Typ ist, behebt die Neuerstellung des Objekts möglicherweise das Problem.  
  
### <a name="restore-from-backup"></a>Sicherungswiederherstellung  
Stellen Sie die Datenbank aus der Sicherung wieder her, wenn das Problem nicht hardwarebezogen ist und eine bekannte intakte Sicherungskopie vorhanden ist. Diese Aktion ist nur anwendbar, wenn die Sicherung den Metadatenfehler nicht enthält.  
  
### <a name="export-the-data-to-a-new-database"></a>Exportieren der Daten in eine neue Datenbank  
Wenn die Metadateninkonsistenz auch in der Sicherung enthalten ist, müssen Sie eine neue Datenbank erstellen und den Inhalt der vorhandenen Datenbank in die neue Datenbank exportieren.  
  
### <a name="dbcc-checkdb-cannot-repair-this-error"></a>Dieser Fehler kann durch DBCC CHECKDB nicht repariert werden  
Dieser Fehler kann nicht repariert werden.  Wenn Sie die Datenbank nicht mithilfe einer Sicherung wiederherstellen können, wenden Sie sich an den Kundenservice und -support von [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
### <a name="do-not-manually-update-system-tables"></a>Systemtabellen dürfen nicht manuell aktualisiert werden  
Nehmen Sie keine manuellen Updates an den Systemtabellen vor. SQL Server unterstützt keine manuellen Änderungen an den Systemdatenbanken. Wenn Sie eine Systemtabelle in einer SQL Server-Datenbank aktualisieren, werden zwei Ereignisse (Ereignis-ID 17659 und Ereignis-ID 3859) protokolliert. Weitere Informationen finden Sie im KB-Artikel 2688307 "Beim Aktualisieren von Systemtabellen in einer SQL Server-Datenbank werden Ereignis-ID 17659 und Ereignis-ID 3859 protokolliert".  
  
## <a name="see-also"></a>Siehe auch  
[Beim Aktualisieren von Systemtabellen in einer SQL Server-Datenbank werden Ereignis-ID 17659 und Ereignis-ID 3859 protokolliert](http://support.microsoft.com/kb/2688307/EN-US)  
  
