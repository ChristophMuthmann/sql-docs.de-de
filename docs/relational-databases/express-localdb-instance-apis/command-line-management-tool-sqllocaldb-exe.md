---
title: 'Verwaltungstool für Befehlszeilen: SqlLocalDB.exe | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apilocation:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
caps.latest.revision: 9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c27b227883bd41af5a00422061c319d43af82864
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>Verwaltungstool für Befehlszeilen: SqlLocalDB.exe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SqlLocalDB.exe ist ein einfaches Tool, das dem Benutzer die einfache Verwaltung der LocalDB-Instanzen in der Befehlszeile ermöglicht. Es wird als einfacher Wrapper um die LocalDB Instanz-API implementiert. Wie in vielen ähnlichen SQL Server-Tools (zum Beispiel SQLCMD) werden Parameter als Befehlszeilenargumente an SqlLocalDB übergeben, und die Ausgabe wird an die Konsole gesendet.  
  
 SqlLocalDB ermöglicht Entwicklern die Verwendung von LocalDB, ohne Code zum Aufrufen der API schreiben zu müssen und ohne von anderen Tools abhängig zu sein, die dies erledigen müssten.  
  
## <a name="sqllocaldb-options"></a>SqlLocalDB-Optionen  
 SqlLocalDB unterstützt die folgenden Optionen.  
  
|Option|Aktion|  
|------------|------------------|  
|`-?`|Druckt Hilfetext.|  
|`create\|c "instance name" [version-number] [-s]`|Erstellt eine neue LocalDB-Instanz mit einem angegebenen Namen und einer Version.<br /><br /> Wenn der [Versionsnummer]-Parameter weggelassen wird, wird standardmäßig die SqlLocalDB-Buildversion verwendet.<br /><br /> -s startet die neue LocalDB-Instanz nach dem Erstellen.|  
|`delete\|d "instance name"`|Löscht die LocalDB-Instanz mit dem angegebenen Namen.|  
|`start\|s "instance name"`|Startet die LocalDB-Instanz mit dem angegebenen Namen.|  
|`stop\|p "instance name" [-i\|-k]`|Beendet die LocalDB-Instanz mit dem angegebenen Namen, nachdem die Ausführung aktueller Abfragen beendet wird.<br /><br /> -i fordert das Herunterfahren der LocalDB-Instanz mit der NOWAIT-Option an.<br /><br /> -k bricht den LocalDB-Instanzprozess ohne Kontaktieren ab.|  
|`share\|h ["owner SID or account"] "private name" "shared name"`|Gibt die angegebene private Instanz mithilfe des angegebenen freigegebenen Namens frei. Wenn die Benutzer-SID oder der Kontoname weggelassen wird, wird standardmäßig der aktuelle Benutzer verwendet.|  
|`unshare\|u "shared name"`|Hebt die Freigabe der angegebenen freigegebenen LocalDB-Instanz auf.|  
|`info\|i`|Listet alle vorhandenen LocalDB-Instanzen im Besitz des aktuellen Benutzers und aller freigegebenen LocalDB-Instanzen auf.|  
|`info\|i "instance name"`|Druckt die Informationen zur angegebenen LocalDB-Instanz.|  
|`versions\|v`|Listet alle auf dem Computer installierten LocalDB-Versionen auf.|  
|||  
|`trace\|t on\|off`|Aktiviert und deaktiviert die Ablaufverfolgung.|  
  
 SqlLocalDB behandelt Leerzeichen als Trennzeichen. Sie müssen die Instanznamen mit Anführungszeichen umschließen, die Leerzeichen und Sonderzeichen enthalten. Zum Beispiel:  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
