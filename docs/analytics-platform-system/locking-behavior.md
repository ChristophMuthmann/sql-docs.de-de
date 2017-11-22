---
title: Sperrverhalten (SQLServer PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c55c636e-b767-4a0c-8184-be991a10801f
caps.latest.revision: "27"
ms.openlocfilehash: 6f4b213942db85b9e7171d11d6b88512d3ad7779
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="locking-behavior"></a>Sperrverhalten
SQL Server PDW verwendet sperren, um die Integrität von Transaktionen sicherzustellen und um die Konsistenz der Datenbanken beizubehalten, wenn mehrere Benutzer gleichzeitig auf Daten zugreifen.  
  
## <a name="Basics"></a>Grundlagen der Sperren  
**Modi**  
  
SQL Server PDW unterstützt vier Sperren Modi:  
  
Exclusive  
Die exklusive Sperre verhindert zu schreiben oder Lesen von gesperrten Objekts, bis die Transaktion, die gedrückt halten, dass die exklusive Sperre abgeschlossen ist. Keine andere Sperren von einem beliebigen-Modus sind zulässig, während die exklusive Sperre aktiviert ist. Beispielsweise verwenden Sie DROP TABLE und CREATE DATABASE eine exklusive Sperre.  
  
Shared  
Die gemeinsame Sperre verhindert die Initiierung von eine exklusive Sperre für das betroffene Objekt, aber Sie können von allen anderen Sperrmodi. Z. B. die SELECT-Anweisung initiiert eine gemeinsame Sperre und aus diesem Grund kann mehrere Abfragen gleichzeitig auf die ausgewählten Daten zugreifen, verhindert aber Updates in die Datensätze gelesen, bis die SELECT-Anweisung abgeschlossen ist.  
  
ExclusiveUpdate  
Die ExclusiveUpdate Sperre verhindert das Schreiben in die gesperrten Objekts, lässt jedoch über die gemeinsame Sperre lesen. Keine andere Sperren sind zulässig, während die ExclusiveUpdate Sperre aktiviert ist. Beispielsweise verwenden Sie BACKUP DATABASE und RESTORE DATABASE eine exklusive updatesperre.  
  
SharedUpdate  
SharedUpdate-Sperre verhindert die exklusive und ExclusiveUpdate Sperrmodi und ermöglicht es Modi für freigegeben und SharedUpdate-Sperre für das Objekt. SharedUpdate ein Objekts ändert, jedoch nicht den Lesezugriff, während der Datenänderung. Beispielsweise INSERT und UPDATE verwendet eine SharedUpdate-Sperre.  
  
**Ressourcenklassen**  
  
Werden Sperren für die folgenden Objektklassen: Datenbank, SCHEMA, Objekt (Tabelle, Sicht oder Prozedur), Anwendung (wird intern verwendet), EXTERNALDATASOURCE, EXTERNALFILEFORMAT und SCHEMARESOLUTION (Datenbankebene Sperren aufgezeichnet wurde beim Erstellen, ändern, oder für welche Schemaobjekte löschen oder Datenbankbenutzer). Diesen Objektklassen können angezeigt werden, in der Spalte Object_type [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="Remarks"></a>Allgemeine Hinweise  
Sperren können für Datenbanken, Tabellen oder Sichten angewendet werden.  
  
Alle konfigurierbaren Isolationsstufen von SQL Server PDW nicht implementiert. Gemäß dem ANSI-standard unterstützt READ_UNCOMMITTED-Isolationsstufe. Allerdings seit Lesevorgänge unter READ_UNCOMMITTED-Vorgänge ausgeführt werden, nur sehr wenige blockierende Vorgänge tatsächlich auftreten oder dazu führen, dass Konflikte im System.  
  
SQL Server PDW basiert auf dem zugrunde liegenden SQL Server-Datenbankmodul zum Sperren und Parallelität Steuerelement zu implementieren. Wenn Vorgänge eines zugrunde liegenden SQL Server-Deadlocks innerhalb des gleichen Knotens sind, wird SQL Server PDW nutzt die SQL Server-Deadlock-Erkennung-Funktion und die blockierenden Anweisungen beendet.  
  
> [!NOTE]  
> SQL Server lässt sich nicht auf Anweisungen aus, die durch neuere sperranforderungen blockiert werden Sperren warten. SQL Server PDW ist dabei nicht vollständig implementiert. In SQL Server-PDW können fortlaufende-Anforderungen für neue freigegebene Sperren manchmal eine vorherige (aber wartende)-Anforderung für eine exklusive Sperre blockiert. Z. B. ein **UPDATE** (und erfordert eine exklusive Sperre)-Anweisung kann blockiert werden, durch gemeinsame Sperren, die für die Reihe von erteilten **wählen** Anweisungen. Einen blockierten Prozess auflösen (identifiziert durch Überprüfen der [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) Matrixneukonfiguration) beenden neue Anforderungen zu senden, bis die exklusive Sperre erfüllt wurde.  
  
## <a name="lock-definition-table"></a>Lock-Definition (Tabelle)  
SQL Server unterstützt die folgenden Typen von Sperren. Nicht alle Typen von Sperren auf den Knoten "Zugriffssteuerung" verfügbar sind, jedoch können auftreten, auf den Serverknoten.  
  
-   Sch-S (Schemastabilität). Stellt sicher, dass ein Schemaelement, wie z. B. eine Tabelle oder ein Index, nicht gelöscht wird, während eine Sitzung eine Schemastabilitätssperre für das Schemaelement aufrechterhält.  
  
-   SCH-M (Schema Modification). Muss von jeder Sitzung aufrechterhalten werden, die das Schema der angegebenen Ressource ändern möchte. Stellt sicher, dass keine anderen Sitzungen auf das angegebene Objekt verweisen.  
  
-   S (Shared). Der haltenden Sitzung wird der gemeinsame Zugriff auf die Ressource erteilt.  
  
-   U (Update). Zeigt eine Updatesperre an, die für Ressourcen ausgegeben wurde, die möglicherweise aktualisiert werden. Sie wird dazu verwendet, eine häufige Form von Deadlock zu verhindern, die auftritt, wenn mehrere Sitzungen Ressourcen sperren, um diese möglicherweise zu einem späteren Zeitpunkt zu aktualisieren.  
  
-   X (Exclusive). Der haltenden Sitzung wird exklusiver Zugriff auf die Ressource erteilt.  
  
-   (Ist Intent Shared). Gibt die Absicht an, S-Sperren für eine untergeordnete Ressource in der Sperrhierarchie zu platzieren.  
  
-   IU (Intent Update). Gibt die Absicht an, U-Sperren für eine untergeordnete Ressource in der Sperrhierarchie zu platzieren.  
  
-   IX (Intent Exclusive). Gibt die Absicht an, X-Sperren für eine untergeordnete Ressource in der Sperrhierarchie zu platzieren.  
  
-   SIU (freigegebene beabsichtigte Update). Zeigt den gemeinsamen Zugriff auf eine Ressource mit der Absicht an, Updatesperren für untergeordnete Ressourcen in der Sperrhierarchie zu erhalten.  
  
-   SECHS (Shared Intent Exclusive). Zeigt den gemeinsamen Zugriff auf eine Ressource mit der Absicht an, exklusive Sperren für untergeordnete Ressourcen in der Sperrhierarchie zu erhalten.  
  
-   UIX (Update Intent Exclusive). Zeigt eine aufrechterhaltene Updatesperre für eine Ressource mit der Absicht an, exklusive Sperren für untergeordnete Ressourcen in der Sperrhierarchie zu erhalten.  
  
-   BU. Wird von Massenvorgängen verwendet.  
  
-   RangeS_S (freigegebener Schlüsselbereich und freigegebene Ressourcensperre). Zeigt serialisierbaren Bereichsscan an.  
  
-   RangeS_U (freigegebener Schlüsselbereich und Update-Ressourcensperre). Zeigt serialisierbaren Updatescan an.  
  
-   RangeI_N (Schlüsselbereich einfügen und keine Ressourcensperre). Wird zum Testen von Bereichen verwendet, bevor ein neuer Schlüssel in einen Index eingefügt wird.  
  
-   RangeI_S. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und S-Sperren erzeugt wurde.  
  
-   RangeI_U. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und U-Sperren erzeugt wurde.  
  
-   RangeI_X. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und X-Sperren erzeugt wurde.  
  
-   RangeX_S. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und RangeS_S.-Sperren erzeugt wurde.  
  
-   RangeX_U. Konvertierungssperre für Schlüsselbereich, die durch eine Überschneidung von RangeI_N- und RangeS_U-Sperren erzeugt wurde.  
  
-   RangeX_X (exklusiver Schlüsselbereich und exklusive Ressourcensperre). Dies ist eine Konvertierungssperre, die für das Update eines Schlüssels in einem Bereich verwendet wird.  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
