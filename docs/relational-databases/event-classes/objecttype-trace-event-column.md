---
title: "ObjectType (Spalte für Ablaufverfolgungsereignisse) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server event classes, Object Type column values
- events [SQL Server], Object Type column values
- event classes [SQL Server], Object Type column values
- Object Type column values [SQL Server]
ms.assetid: 42f85c50-34c9-49ca-955f-af9595e2707f
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f4870fdd355f03c7f1e5c4fee15cf410f5794411
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="objecttype-trace-event-column"></a>ObjectType (Spalte für Ablaufverfolgungsereignisse)
  Die ObjectType-Spalte wird für eine Vielzahl von Ablaufverfolgungsereignissen verwendet. In diesem Thema werden die möglichen Werte dieser Spalte und eine Definition des jeweiligen Wertes aufgeführt.  
  
## <a name="object-type-column-values"></a>Werte der ObjectType-Spalte  
  
|Wert|Definition|  
|-----------|----------------|  
|8259|CHECK-Einschränkung|  
|8260|Standard (Einschränkung oder eigenständig)|  
|8262|FOREIGN KEY-Einschränkung|  
|8272|Gespeicherte Prozedur|  
|8274|Rule|  
|8275|Systemtabelle|  
|8276|Trigger für Server|  
|8277|Tabelle (benutzerdefiniert)|  
|8278|Sicht|  
|8280|Erweiterte gespeicherte Prozeduren|  
|16724|CLR-Trigger|  
|16964|Datenbank|  
|16975|Objekt|  
|17222|Volltextkatalog|  
|17232|CLR-gespeicherte Prozedur|  
|17235|Schema|  
|17475|Anmeldeinformationen|  
|17491|DDL-Ereignis|  
|17741|Verwaltungsereignis|  
|17747|Sicherheitsereignis|  
|17749|Benutzerereignis|  
|17985|CLR-Aggregatfunktion|  
|17993|Inline-Tabellenwertfunktion von SQL|  
|18000|Partitionsfunktion|  
|18002|Replikationsfilterprozedur|  
|18004|SQL-Tabellenwertfunktionen|  
|18259|Serverrolle|  
|18263|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Gruppe|  
|19265|Asymmetrischer Schlüssel|  
|19277|Hauptschlüssel|  
|19280|Primärschlüssel|  
|19283|ObfusKey|  
|19521|Anmeldung mit asymmetrischem Schlüssel|  
|19523|Anmeldung mit Zertifikat|  
|19538|Rolle|  
|19539|SQL-Anmeldung|  
|19543|Windows-Anmeldung|  
|20034|Remotedienstbindung|  
|20036|DB-Ereignisbenachrichtigung|  
|20037|Ereignisbenachrichtigung|  
|20038|SQL-Skalarfunktionen|  
|20047|Objektereignisbenachrichtigung|  
|20051|Synonym|  
|20307|Sequenz|  
|20549|Endpunkt|  
|20801|Gegebenenfalls zwischengespeicherte Ad-hoc-Abfragen|  
|20816|Gegebenenfalls zwischengespeicherte vorbereitete Abfragen|  
|20819|Service Broker-Dienstwarteschlange|  
|20821|UNIQUE-Einschränkung|  
|21057|Anwendungsrolle|  
|21059|Zertifikat|  
|21075|Server|  
|21076|Transact-SQL-Trigger|  
|21313|Assembly|  
|21318|CLR-Skalarfunktion|  
|21321|SQL-Inlineskalarfunktion|  
|21328|Partitionsschema|  
|21333|Benutzer|  
|21571|Service Broker-Dienstvertrag|  
|21572|Trigger für Datenbank|  
|21574|CLR-Tabellenwertfunktionen|  
|21577|Interne Tabelle (z. B. XML-Knotentabelle, Warteschlangentabelle)|  
|21581|Service Broker-Nachrichtentyp|  
|21586|Service Broker-Route|  
|21587|Statistik|  
|21825<br /><br /> 21827<br /><br /> 21831<br /><br /> 21843<br /><br /> 21847|Benutzer|  
|22099|Service Broker-Dienst|  
|22601|Index|  
|22604|Anmeldung mit Zertifikat|  
|22611|XML-Schema|  
|22868|Typ|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  

