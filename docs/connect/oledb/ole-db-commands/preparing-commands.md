---
title: Vorbereiten von Befehlen | Microsoft Docs
description: Vorbereiten von Befehlen, die mithilfe von OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- prepared statements [OLE DB Driver for SQL Server]
- commands [OLE DB]
- command preparation [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: cdef5e3ebb01ec678f0916ec9324d39c939b5e6d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="preparing-commands"></a>Vorbereiten von Befehlen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server unterstützt die befehlsvorbereitung für mehrfache Ausführung eines einzelnen Befehls optimiert; Allerdings befehlsvorbereitung Mehraufwand, und ein Consumer muss nicht vorbereiten ein Befehls mehrmals auszuführen. Im Allgemeinen sollte ein Befehl vorbereitet werden, wenn er mehr als drei Mal ausgeführt wird.  
  
 Aus Leistungsgründen wird die Befehlsvorbereitung verzögert, bis der Befehl ausgeführt wird. Dies ist das Standardverhalten. Fehler in dem vorbereiteten Befehl werden erst dann erkannt, wenn der Befehl ausgeführt wird oder ein Metaeigenschaftsvorgang durchgeführt wird. Durch die Festlegung der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Eigenschaft SSPROP_DEFERPREPARE auf FALSE kann dieses Standardverhalten deaktiviert werden.  
  
 Wenn ein Befehl in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] direkt ausgeführt wird (ohne dass er zuerst vorbereitet wurde), wird ein Ausführungsplan erstellt und zwischengespeichert. Wenn die SQL-Anweisung erneut ausgeführt wird, setzt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] einen effizienten Algorithmus ein, um die neue Anweisung dem vorhandenen Ausführungsplan im Cache zuzuordnen, und verwendet den Ausführungsplan dann erneut.  
  
 Für vorbereitete Befehle stellt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] systemeigene Unterstützung für das Vorbereiten und Ausführen von Befehlsanweisungen bereit. Wenn Sie eine Anweisung vorbereiten, erstellt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] einen Ausführungsplan, speichert ihn zwischen und übergibt dem Anbieter einen Handle für diesen Ausführungsplan. Der Anbieter verwendet dieses Handle, um die Anweisung wiederholt auszuführen. Es werden keine gespeicherten Prozeduren erstellt. Da das Handle den Ausführungsplan für eine SQL-Anweisung direkt identifiziert, statt die Anweisung dem Ausführungsplan im Cache zuzuordnen (wie bei der direkten Ausführung), ist es effizienter, eine Anweisung vorzubereiten (statt sie direkt auszuführen), wenn Sie wissen, dass eine Anweisung häufiger ausgeführt werden wird.  
  
 In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] können vorbereitete Anweisungen nicht zur Erstellung temporärer Objekte verwendet werden, und vorbereitete Anweisungen können nicht auf gespeicherte Systemprozeduren verweisen, die temporäre Objekte erstellen, z. B. temporäre Tabellen. Diese Prozeduren müssen direkt ausgeführt werden.  
  
 Einige Befehle sollten nie vorbereitet werden. Beispielsweise sollten Befehle, mit denen die Ausführung gespeicherter Prozeduren angegeben wird oder die ungültigen Text für die Erstellung gespeicherter Prozeduren in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enthalten, nicht vorbereitet werden.  
  
 Wenn eine temporäre gespeicherte Prozedur erstellt wird, führt der OLE DB-Treiber für SQL Server die temporäre gespeicherte Prozedur zurückgeben von Ergebnissen, als wäre die Anweisung selbst ausgeführt wurde.  
  
 Erstellung temporär gespeicherter Prozeduren wird gesteuert, von der OLE DB-Treiber für SQL Server-spezifische Initialisierungseigenschaft SSPROP_INIT_USEPROCFORPREP. Wenn der Eigenschaftswert SSPROPVAL_USEPROCFORPREP_ON oder SSPROPVAL_USEPROCFORPREP_ON_DROP ist, versucht der OLE DB-Treiber für SQL Server zum Erstellen einer gespeicherten Prozedur, wenn ein Befehl vorbereitet wird. Die Erstellung der gespeicherten Prozedur ist erfolgreich, wenn der Anwendungsbenutzer über ausreichende [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Berechtigungen verfügt.  
  
 Für Consumer, die selten die Verbindung trennen, kann die Erstellung temporär gespeicherter Prozeduren bedeutende Menge von Ressourcen erfordern **Tempdb**die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Systemdatenbank, in denen temporäre Objekte erstellt werden. Bei der Wert sspropval_useprocforprep_on zwischen ist, werden temporäre gespeicherte Prozeduren, die von der OLE DB-Treiber für SQL Server erstellt wurden gelöscht, nur, wenn die Sitzung, die der Befehl erstellt eine Verbindung mit der Instanz von verliert[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Falls es sich bei dieser Verbindung um die Standardverbindung handelt, die bei der Initialisierung der Datenquelle erstellt wurde, dann wird die temporär gespeicherte Prozedur nur dann gelöscht, wenn die Initialisierung der Datenquelle aufgehoben wird.  
  
 Wenn SSPROP_INIT_USEPROCFORPREP den Wert SSPROPVAL_USEPROCFORPREP_ON_DROP ist, werden die OLE DB-Treiber für SQL Server temporäre gespeicherte Prozeduren gelöscht, wenn eines der folgenden Ereignisse eintritt:  
  
-   Der Consumer verwendet **ICommandText:: SetCommandText** um einen neuen Befehl anzugeben.  
  
-   Der Consumer verwendet **ICommandPrepare:: Unprepare** , um anzugeben, dass sie den Befehlstext nicht mehr erforderlich ist.  
  
-   Der Consumer gibt alle Verweise auf das Befehlsobjekt, das die temporäre gespeicherte Prozedur verwendet, frei.  
  
 Ein Befehlsobjekt verfügt höchstens eine temporäre gespeicherte Prozedur **Tempdb**. Jede vorhandene temporär gespeicherte Prozedur stellt den aktuellen Befehlstext eines bestimmten Befehlsobjekts dar.  
  
## <a name="see-also"></a>Siehe auch  
 [Befehle](../../oledb/ole-db-commands/commands.md)  
  
  
