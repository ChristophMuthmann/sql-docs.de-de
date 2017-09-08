---
title: "Festlegen von Optionen für Projekt (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f325a606-97ac-48bc-b344-b55f5e086a48
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1f5b71db23d56150fbc6a2f7990ba9960d83d2d1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="setting-project-options-db2tosql"></a>Einstellungsoptionen für Projekt (DB2ToSQL)
Für jedes SSMA-Projekt können Sie Optionen für Projekt festlegen. Diese Optionen geben Objekt Konvertierung, Objekt laden, Benutzeroberflächen- und Migration benutzereinstellungen. Bevor Sie Objekte konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Migrieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], stellen Sie sicher, dass die Konfigurationsoptionen für das Projekt geeignet sind.  
  
SSMA können Sie die Standardoptionen für alle Projekte zu konfigurieren. Diese Optionen werden auf jedem neuen Projekt angewendet, die Sie erstellen. Sie können dann die Optionen für jedes Projekt anpassen.  
  
## <a name="configuration-options-and-modes"></a>Modi "und"-Konfigurationsoptionen  
SSMA verfügt über fünf Mengen von projekteinstellungen:  
  
-   Projektinformationen  
  
-   Allgemein (Konvertierung, Migration, Laden von Objekten)  
  
-   Synchronization  
  
-   GUI  
  
-   Typzuordnung  
  
Es sind auch vier Modi für diese Einstellungen konfigurieren:  
  
-   Standardwert  
  
-   Optimistisch  
  
-   Vollständig  
  
-   Benutzerdefiniert  
  
Der Standardmodus ist für die meisten Benutzer empfohlen. Der optimistische hält mehrere der Syntax für die aktuelle DB2 und einfacher zu lesen. Jedoch behalten die aktuelle Syntax genau möglicherweise nicht. Wenn die DB2-Syntax muss, in entsprechende konvertiert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, die der Vollmodus die beste Konvertierung durchgeführt, aber möglicherweise ist des resultierenden Codes schwieriger zu lesen. In den benutzerdefinierten Modus legen Sie die Optionen an.  
  
Weitere Informationen zu den Einstellungen und wie die Einstellungen in jedem Modus angewendet werden finden Sie unter den folgenden Themen:  
  
-   [Projekteinstellungen &#40; Konvertierung &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)  
  
-   [Projekteinstellungen &#40; Migration &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-migration-db2tosql.md)  
  
-   [Projekteinstellungen &#40; Synchronisierung &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)  
  
-   [Projekteinstellungen &#40; GUI &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-gui-db2tosql.md)  
  
-   [Projekteinstellungen &#40; Typzuordnung &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)  
  
## <a name="setting-project-options"></a>Einstellung Projektoptionen  
In SSMA können Sie die Standardeinstellungen für alle Projekte konfigurieren. Diese Einstellungen sind der SSMA-Konfigurationsdatei gespeichert und angewendet wird, zu einem neuen Projekt, das Sie erstellen.  
  
**Zum Festlegen von standardmäßigen Projektoptionen**  
  
1.  Auf der **Tools** Menü klicken Sie auf **Projekt Standardeinstellungen**.  
  
2.  In der **Projekt Standardeinstellungen** (Dialogfeld), verwenden Sie eine der folgenden Verfahren:  
  
    -   Wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden **Migration Zielversion** Dropdown-Liste auf **allgemeine** am unteren Rand der Links, und wählen Sie dann Konvertierung oder Migration.  
  
    -   Wählen Sie einen vordefinierten Modus in den **Modus** wählen Sie im Dropdown- **Standard**, **Optimistic**, oder **vollständige**.  
  
    -   Um benutzerdefinierte Einstellungen festzulegen, wählen Sie aus, oder geben Sie den neuen Einstellungen oder Werten.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
Sie können auch die Einstellungen für das aktuelle Projekt anpassen. Diese Einstellungen werden in der aktuellen Projektdatei gespeichert.  
  
**Einstellungen für das aktuelle Projekt anpassen**  
  
1.  Auf der **Tools** Menü klicken Sie auf **Projekteinstellungen**.  
  
2.  In der **Projekteinstellungen** (Dialogfeld), verwenden Sie eine der folgenden Verfahren:  
  
    -   Wählen Sie einen vordefinierten Modus in den **Modus** wählen Sie im Dropdown- **Standard**, **Optimistic**, oder **vollständige**.  
  
    -   Angeben einen benutzerdefinierten Modus, in der **Modus** wählen Sie im **benutzerdefinierte**, und wählen Sie dann die richtigen projekteinstellungen.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
## <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnung DB2 und SQL Server-Datentypen &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   Konvertieren Sie Sie andernfalls die DB2-Datenbank-Objektdefinitionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Objektdefinitionen. Weitere Informationen finden Sie unter [DB2-Schemas konvertieren &#40; DB2ToSQL &#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Zuordnen von DB2 und SQL Server-Datentypen &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)  
  

