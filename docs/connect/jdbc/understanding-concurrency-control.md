---
title: "Grundlegendes zur Parallelitätssteuerung | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 52c954cb3acc87753f9ede5a0fc786bd9ed9b755
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-concurrency-control"></a>Grundlegendes zur Parallelitätssteuerung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Als Parallelitätssteuerung werden unterschiedliche Verfahren beschrieben, mit denen die Integrität der Datenbank erhalten wird, wenn mehrere Benutzer gleichzeitig Zeilen aktualisieren. Falsche Parallelität kann zu Problemen führen, beispielsweise Dirty Reads, Phantomlesezugriffe und nicht wiederholbare Lesevorgänge. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] stellt Schnittstellen für alle von verwendeten parallelitätsverfahren bereit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] zum Lösen dieser Probleme.  
  
> [!NOTE]  
>  Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Parallelität, finden Sie unter "Verwalten von parallelen Datenzugriffs" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="remarks"></a>Hinweise  
 Der JDBC-Treiber unterstützt die folgenden Parallelitätstypen:  
  
|Parallelitätstyp|Merkmale|Sperren auf Zeilenebene|Description|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|Read Only|Nein|Updates über den Cursor sind nicht zulässig; es werden keine Sperren für die Zeilen aufrechterhalten, aus denen das Resultset besteht.|  
|CONCUR_UPDATABLE|Optimistic Read Write|Nein|Die Datenbank geht davon aus, dass Zeilenkonflikte unwahrscheinlich, aber möglich sind. Zeilenintegrität wird mit einem Timestampvergleich geprüft.|  
|CONCUR_SS_SCROLL_LOCKS|Pessimistic Read Write|ja|Die Datenbank geht davon aus, dass Zeilenkonflikte wahrscheinlich sind. Zeilenintegrität wird mit Zeilensperren sichergestellt.|  
|CONCUR_SS_OPTIMISTIC_CC|Optimistic Read Write|Nein|Die Datenbank geht davon aus, dass Zeilenkonflikte unwahrscheinlich, aber möglich sind. Zeilenintegrität wird mit einem Timestampvergleich überprüft.<br /><br /> Für [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] und höher, der Server ändert sich dies in CONCUR_SS_OPTIMISTIC_CCVAL, wenn die Tabelle keine Timestamp-Spalte enthält.<br /><br /> Für [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], wenn die zugrunde liegende Tabelle eine Timestamp-Spalte verfügt, wird OPTIMISTIC WITH ROW VERSIONING verwendet, auch wenn OPTIMISTIC WITH VALUES angegeben ist. Wenn OPTIMISTIC WITH ROW VERSIONING angegeben wurde und die Tabelle keine Timestamps aufweist, wird OPTIMISTIC WITH VALUES verwendet.|  
|CONCUR_SS_OPTIMISTIC_CCVAL|Optimistic Read Write|Nein|Die Datenbank geht davon aus, dass Zeilenkonflikte unwahrscheinlich, aber möglich sind. Zeilenintegrität wird mit einem Zeilendatenvergleich geprüft.|  
  
## <a name="result-sets-that-are-not-updateable"></a>Nicht aktualisierbare Resultsets  
 Ein aktualisierbares Resultset ist ein Resultset, in dem Zeilen eingefügt, aktualisiert und gelöscht werden können. In den folgenden Fällen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] keinen aktualisierbaren Cursor kann nicht erstellt werden. Die generierte Ausnahme lautet "Das Resultset kann nicht aktualisiert werden".  
  
|Ursache|Description|Remedy|  
|-----------|-----------------|------------|  
|Anweisung wurde nicht mit JDBC 2.0-Syntax (oder neuer) erstellt|In JDBC 2.0 wurden neue Methoden eingeführt, um Anweisungen zu erstellen. Bei der Verwendung von JDBC 1.0-Syntax ist das Resultset standardmäßig schreibgeschützt.|Geben Sie den Resultsettyp und die Parallelität beim Erstellen der Anweisung an.|  
|Anweisung wurde mit TYPE_SCROLL_INSENSITIVE erstellt|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]erstellt einen statischen momentaufnahmencursor. Dieser ist von den zugrunde liegenden Tabellenzeilen getrennt, um den Cursor vor Zeilenudpates durch andere Benutzer zu schützen.|Verwenden Sie TYPE_SCROLL_SENSITIVE, TYPE_SS_SCROLL_KEYSET, TYPE_SS_SCROLL_DYNAMIC oder TYPE_FORWARD_ONLY mit CONCUR_UPDATABLE, um das Erstellen eines statischen Cursors zu vermeiden.|  
|Tabellenentwurf schließt einen KEYSET-Cursor oder einen DYNAMIC-Cursor aus|Die zugrunde liegende Tabelle keinen eindeutigen Schlüssel aktivieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] zur eindeutigen Identifizierung eine Zeile.|Fügen Sie der Tabelle eindeutige Schlüssel hinzu, um eine eindeutige Identifikation jeder Zeile bereitzustellen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Resultsets mit dem JDBC-Treiber legt diese fest](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
