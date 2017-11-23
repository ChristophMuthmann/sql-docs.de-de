---
title: "Verwaltungstool für Befehlszeilen: SqlLocalDB.exe | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apilocation: sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8f2bac1f105f5d299fa97d11fa579226026134aa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Verwaltungstool für Befehlszeilen: SqlLocalDB.exe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]SqlLocalDB.exe ist ein einfaches Tool, das dem Benutzer ermöglicht, die einfache Verwaltung der LocalDB-Instanzen in der Befehlszeile. Es wird als einfacher Wrapper um die LocalDB Instanz-API implementiert. Wie in vielen ähnlichen SQL Server-Tools (zum Beispiel SQLCMD) werden Parameter als Befehlszeilenargumente an SqlLocalDB übergeben, und die Ausgabe wird an die Konsole gesendet.  
  
 SqlLocalDB ermöglicht Entwicklern die Verwendung von LocalDB, ohne Code zum Aufrufen der API schreiben zu müssen und ohne von anderen Tools abhängig zu sein, die dies erledigen müssten.  
  
## <a name="sqllocaldb-options"></a>SqlLocalDB-Optionen  
 SqlLocalDB unterstützt die folgenden Optionen.  
  
|Option|Aktion|  
|------------|------------------|  
|`-?`|Druckt Hilfetext.|  
|"Create\|c "der Instanzname" [Versionsnummer] [-s] "|Erstellt eine neue LocalDB-Instanz mit einem angegebenen Namen und einer Version.<br /><br /> Wenn der [Versionsnummer]-Parameter weggelassen wird, wird standardmäßig die SqlLocalDB-Buildversion verwendet.<br /><br /> -s startet die neue LocalDB-Instanz nach dem Erstellen.|  
|"Delete\|"der Instanzname"-d "|Löscht die LocalDB-Instanz mit dem angegebenen Namen.|  
|"Start|"der Instanzname"-s "|Startet die LocalDB-Instanz mit dem angegebenen Namen.|  
|"Stop|p "der Instanzname" [-I\|-k] "|Beendet die LocalDB-Instanz mit dem angegebenen Namen, nachdem die Ausführung aktueller Abfragen beendet wird.<br /><br /> -i fordert das Herunterfahren der LocalDB-Instanz mit der NOWAIT-Option an.<br /><br /> -k bricht den LocalDB-Instanzprozess ohne Kontaktieren ab.|  
|"Share\|h ["Besitzer-SID oder Konto"] "private Name" "Freigabenamen" "|Gibt die angegebene private Instanz mithilfe des angegebenen freigegebenen Namens frei. Wenn die Benutzer-SID oder der Kontoname weggelassen wird, wird standardmäßig der aktuelle Benutzer verwendet.|  
|"Unshare\|"freigegebene Name" u "|Hebt die Freigabe der angegebenen freigegebenen LocalDB-Instanz auf.|  
|"Info\|ich "|Listet alle vorhandenen LocalDB-Instanzen im Besitz des aktuellen Benutzers und aller freigegebenen LocalDB-Instanzen auf.|  
|"Info\|i "der Instanzname" "|Druckt die Informationen zur angegebenen LocalDB-Instanz.|  
|"Versionen aktualisieren\|V "|Listet alle auf dem Computer installierten LocalDB-Versionen auf.|  
|||  
|"Trace\|t-on\|deaktiviert "|Aktiviert und deaktiviert die Ablaufverfolgung.|  
  
 SqlLocalDB behandelt Leerzeichen als Trennzeichen. Sie müssen die Instanznamen mit Anführungszeichen umschließen, die Leerzeichen und Sonderzeichen enthalten. Zum Beispiel:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
