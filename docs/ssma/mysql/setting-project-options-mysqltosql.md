---
title: "Festlegen von Optionen für Projekt (MySQLToSQL) | Microsoft Docs"
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
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 005889e4a4fc813819f6133d7a5a7b2a5223b861
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="setting-project-options-mysqltosql"></a>Einstellungsoptionen für Projekt (MySQLToSQL)
Für jedes Projekt SSMA können Sie das Projekt auf Dokumentebene Optionen festlegen. Diese Optionen angeben, wie Objekte umgewandelt werden, wie die Daten migriert werden und wie Quelldatentypen Ziel-Datentypen zugeordnet.  Bevor Sie Objekte in SQL Server oder SQL Azure konvertieren oder Migrieren von Daten in SQL Server oder SQL Azure, stellen Sie sicher, dass die Konfigurationsoptionen für das Projekt geeignet sind.  
  
SSMA können Sie die Standardoptionen für alle Projekte zu konfigurieren. Diese Optionen werden auf jedem neuen Projekt angewendet, die Sie erstellen. Sie können dann die Optionen für jedes Projekt anpassen.  
  
## <a name="configuration-options-and-modes"></a>Modi "und"-Konfigurationsoptionen  
SSMA verfügt über fünf Mengen von projekteinstellungen:  
  
-   Projektinformationen  
  
-   Allgemein (Konvertierung, Migration und SQL Azure)  
  
-   Synchronization  
  
-   GUI  
  
-   Typzuordnung  
  
Die Einstellungen für Projektdateien können auf vier Arten konfiguriert werden:  
  
-   Standardwert  
  
-   Optimistisch  
  
-   Vollständig  
  
-   Benutzerdefiniert  
  
Der Standardmodus ist für die meisten Benutzer empfohlen. Der optimistische hält mehrere der Syntax für die aktuelle MySQL und einfacher zu lesen. Jedoch behalten die aktuelle Syntax genau möglicherweise nicht. Wenn die MySQL-Syntax in entsprechende SQL Server- bzw. SQL Azure-Syntax konvertiert werden muss, durch die Vollmodus die möglichst lückenlos Konvertierung durchgeführt. Der resultierende Code möglicherweise jedoch schwieriger zu lesen. In den benutzerdefinierten Modus können Sie die Optionen festlegen.  
  
Weitere Informationen zu den Einstellungen und wie die Einstellungen in jedem Modus angewendet werden finden Sie unter den folgenden Themen:  
  
-   [Projekteinstellungen &#40; Konvertierung &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [Projekteinstellungen &#40; Migration &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [Projekteinstellungen (GUI) (SSMA Common)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Projekteinstellungen &#40; Typzuordnung &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [Projekteinstellungen &#40; Synchronisierung &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [Projekteinstellungen &#40; Azure SQL-Datenbank &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>Einstellung Projektoptionen  
In SSMA können Sie die Standardeinstellungen für alle Projekte konfigurieren. Diese Einstellungen sind der SSMA-Konfigurationsdatei gespeichert und angewendet wird, zu einem neuen Projekt, das Sie erstellen.  
  
**Zum Festlegen von standardmäßigen Projektoptionen**  
  
1.  Auf der **Tools** Menü klicken Sie auf **Projekt Standardeinstellungen**.  
  
2.  In der **Projekt Standardeinstellungen** (Dialogfeld), verwenden Sie eine der folgenden Verfahren:  
  
    1.  Wählen Sie die Migration-Projekttyp, die für die Einstellungen angezeigt oder geändert werden, erforderlich sind **Migration Zielversion** Dropdown-Liste, klicken Sie auf **allgemeine** am unteren Rand des linken Bereich, und klicken Sie dann wählen **Konvertierung oder Migration oder SQL Azure** Option.  
  
    2.  Wählen Sie zum Auswählen eines vordefinierten Modus **Standard**, **Optimistic**, oder **vollständige** aus der **Modus** Dropdown-Menü.  
  
    3.  Um benutzerdefinierte Einstellungen festzulegen, wählen Sie aus, oder geben Sie den neuen Einstellungen oder Werten.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
Sie können auch die Einstellungen für das aktuelle Projekt anpassen. Der aktuellen Projektdatei abrufen gespeichert.  
  
**Einstellungen für das aktuelle Projekt anpassen**  
  
1.  Auf der **Tools** Menü klicken Sie auf **ProjectSettings**.  
  
2.  In der **ProjectSettings** (Dialogfeld), verwenden Sie eine der folgenden Verfahren:  
  
    1.  Wählen Sie zum Auswählen eines vordefinierten Modus **Standard**, **Optimistic**, oder **vollständige** aus der **Modus** Dropdown-Menü.  
  
    2.  Wählen Sie zum Angeben eines benutzerdefinierten Modus **benutzerdefinierte** aus der **Modus** Dropdown-Menü. Und wählen Sie dann die richtigen projekteinstellungen.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnung MySQL und SQL Server-Datentypen &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Andernfalls können Sie die Objektdefinitionen für MySQL-Datenbank in SQL Server- oder SQL Azure-Objektdefinitionen konvertieren. Weitere Informationen finden Sie unter [MySQL-Datenbanken konvertieren &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Zuordnen von MySQL und SQL Server-Datentypen &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  

