---
title: Vorbereiten von Befehlen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-commands
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- prepared statements [SQL Server Native Client]
- commands [OLE DB]
- command preparation [SQL Server Native Client]
ms.assetid: 09ec0c6c-0a44-4766-b9b7-5092f676ee54
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6d30ccd88e58b99febeffe60da9199434dffc63
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="preparing-commands"></a>Vorbereiten von Befehlen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der OLE-DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client unterstützt die Befehlsvorbereitung für die optimierte mehrfache Ausführung eines einzelnen Befehls. Allerdings ist die Befehlsvorbereitung mit zusätzlichem Aufwand verbunden, und Consumer müssen Befehle nicht vorbereiten, um sie mehrfach auszuführen. Im Allgemeinen sollte ein Befehl vorbereitet werden, wenn er mehr als drei Mal ausgeführt wird.  
  
 Aus Leistungsgründen wird die Befehlsvorbereitung verzögert, bis der Befehl ausgeführt wird. Dies ist das Standardverhalten. Fehler in dem vorbereiteten Befehl werden erst dann erkannt, wenn der Befehl ausgeführt wird oder ein Metaeigenschaftsvorgang durchgeführt wird. Durch die Festlegung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Eigenschaft SSPROP_DEFERPREPARE auf FALSE kann dieses Standardverhalten deaktiviert werden.  
  
 Wenn ein Befehl in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] direkt ausgeführt wird (ohne dass er zuerst vorbereitet wurde), wird ein Ausführungsplan erstellt und zwischengespeichert. Wenn die SQL-Anweisung erneut ausgeführt wird, setzt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen effizienten Algorithmus ein, um die neue Anweisung dem vorhandenen Ausführungsplan im Cache zuzuordnen, und verwendet den Ausführungsplan dann erneut.  
  
 Für vorbereitete Befehle stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] systemeigene Unterstützung für das Vorbereiten und Ausführen von Befehlsanweisungen bereit. Wenn Sie eine Anweisung vorbereiten, erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Ausführungsplan, speichert ihn zwischen und übergibt dem Anbieter einen Handle für diesen Ausführungsplan. Der Anbieter verwendet dieses Handle, um die Anweisung wiederholt auszuführen. Es werden keine gespeicherten Prozeduren erstellt. Da das Handle den Ausführungsplan für eine SQL-Anweisung direkt identifiziert, statt die Anweisung dem Ausführungsplan im Cache zuzuordnen (wie bei der direkten Ausführung), ist es effizienter, eine Anweisung vorzubereiten (statt sie direkt auszuführen), wenn Sie wissen, dass eine Anweisung häufiger ausgeführt werden wird.  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] können vorbereitete Anweisungen nicht zur Erstellung temporärer Objekte verwendet werden, und vorbereitete Anweisungen können nicht auf gespeicherte Systemprozeduren verweisen, die temporäre Objekte erstellen, z. B. temporäre Tabellen. Diese Prozeduren müssen direkt ausgeführt werden.  
  
 Einige Befehle sollten nie vorbereitet werden. Beispielsweise sollten Befehle, mit denen die Ausführung gespeicherter Prozeduren angegeben wird oder die ungültigen Text für die Erstellung gespeicherter Prozeduren in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthalten, nicht vorbereitet werden.  
  
 Wenn eine temporäre gespeicherte Prozedur erstellt wird, dann führt der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client die temporäre gespeicherte Prozedur aus, wobei die Ergebnisse so ausgegeben werden, als sei die Anweisung selbst ausgeführt worden.  
  
 Die Erstellung temporär gespeicherter Prozeduren wird durch die Initialisierungseigenschaft SSPROP_INIT_USEPROCFORPREP gesteuert, die dem OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client eigen ist. Wenn der Eigenschaftswert SSPROPVAL_USEPROCFORPREP_ON oder SSPROPVAL_USEPROCFORPREP_ON_DROP lautet, versucht der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client eine gespeicherte Prozedur zu erstellen, wenn ein Befehl vorbereitet wird. Die Erstellung der gespeicherten Prozedur ist erfolgreich, wenn der Anwendungsbenutzer über ausreichende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Berechtigungen verfügt.  
  
 Für Consumer, die selten die Verbindung trennen, kann die Erstellung temporär gespeicherter Prozeduren bedeutende Menge von Ressourcen erfordern **Tempdb**die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Systemdatenbank, in denen temporäre Objekte erstellt werden. Wenn SSPROP_INIT_USEPROCFORPREP den Wert SSPROPVAL_USEPROCFORPREP_ON hat, werden die vom OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client erstellten temporären gespeicherten Prozeduren nur dann gelöscht, wenn die Verbindung zwischen der Sitzung, in der der Befehl erstellt wurde, und der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] getrennt wird. Falls es sich bei dieser Verbindung um die Standardverbindung handelt, die bei der Initialisierung der Datenquelle erstellt wurde, dann wird die temporär gespeicherte Prozedur nur dann gelöscht, wenn die Initialisierung der Datenquelle aufgehoben wird.  
  
 Wenn SSPROP_INIT_USEPROCFORPREP den Wert SSPROPVAL_USEPROCFORPREP_ON_DROP hat, werden die vom OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client erstellten temporär gespeicherten Prozeduren gelöscht, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Der Consumer verwendet **ICommandText:: SetCommandText** um einen neuen Befehl anzugeben.  
  
-   Der Consumer verwendet **ICommandPrepare:: Unprepare** , um anzugeben, dass sie den Befehlstext nicht mehr erforderlich ist.  
  
-   Der Consumer gibt alle Verweise auf das Befehlsobjekt, das die temporäre gespeicherte Prozedur verwendet, frei.  
  
 Ein Befehlsobjekt verfügt höchstens eine temporäre gespeicherte Prozedur **Tempdb**. Jede vorhandene temporär gespeicherte Prozedur stellt den aktuellen Befehlstext eines bestimmten Befehlsobjekts dar.  
  
## <a name="see-also"></a>Siehe auch  
 [Befehle](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
