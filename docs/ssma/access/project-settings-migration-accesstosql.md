---
title: Projekteinstellungen (Migration) (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83f7ad0fbda7ead76a24e40f971e9589719fb788
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="project-settings-migration-accesstosql"></a>Projekteinstellungen (Migration) (AccessToSQL)
Die projekteinstellungen für die Migration können Sie konfigurieren, wie die Daten migriert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
Der Bereich für die Migration finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder.  
  
-   Verwenden der **Projekteinstellungen** (Dialogfeld), Konfigurationsoptionen für das aktuelle Projekt festzulegen. Die migrationseinstellungen auf den Zugriff auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Migration**.  
  
-   Verwenden der **Projekt Standardeinstellungen** (Dialogfeld), Konfigurationsoptionen für alle Projekte festzulegen. Die migrationseinstellungen auf den Zugriff auf die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie den Projekttyp in **Migration Zielversion** Kombinationsfeld, von denen Sie darauf zugreifen möchten die Einstellungen, klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Migration**.  
  
## <a name="options"></a>enthalten  
**Check-Einschränkungen**  
Gibt an, ob SSMA Einschränkungen überprüft werden sollen, wenn Daten zu Tabellen hinzugefügt.  
  
-   **Standardmodus**: "false"  
  
-   **Vollständige**: "true"  
  
-   **Vollständige Modus**: "false"  
  
**Trigger auslösen**  
Gibt an, ob SSMA einfügen Trigger ausgelöst werden soll, wenn sie Daten hinzufügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Tabellen.  
  
-   **Standardmodus**: "false"  
  
-   **Vollständige**: "true"  
  
-   **Vollständige Modus**: "false"  
  
**Identität beibehalten**  
Gibt an, ob SSMA Zugriff Identitätswerte beibehalten, wenn Daten hinzugefügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn dieser Wert "false" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Identitätswerte zuweist.  
  
-   **Standardmodus**: "true"  
  
-   **Vollständige**: "true"  
  
-   **Vollständige Modus**: "false"  
  
**NULL-Werte beibehalten**  
Gibt an, ob SSMA behält null-Werte in den Quelldaten aus, wenn Daten hinzugefügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], unabhängig von der Standardwerte, die im angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   **Standardmodus**: "true"  
  
-   **Vollständige**: "false"  
  
-   **Vollständige Modus**: "true"  
  
**Tabellensperren**  
Gibt an, ob SSMA Tabellen sperrt, wenn sie Daten während der Datenmigration für Tabellen hinzufügt. Wenn der Wert "false" ist, wird SSMA Zeilensperren verwendet.  
  
-   **Standardmodus**: "true"  
  
-   **Vollständige**: "true"  
  
-   **Vollständige Modus**: "true"  
  
**Ersetzen von nicht unterstützten Datumsangaben**  
Gibt an, ob SSMA Zugriffsdaten Beseitigung zuständig, die älter als die früheste sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "DateTime" Datum (01 Januar 1753).  
  
-   Um die Werte aktuell zu halten, wählen Sie **nichts**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datumsangaben vor 01 Januar 1753 wird in einer Datetime-Spalte nicht akzeptiert werden. Wenn Sie ältere Daten verwenden, müssen Sie die Datums-/ Uhrzeitwerten in Zeichenwerten konvertieren.  
  
-   Wählen Sie zum Konvertieren von Datumsangaben vor 01 Januar 1753 auf NULL **durch NULL Ersetzen**.  
  
-   Wählen Sie zum Ersetzen von Datumsangaben vor 01 Januar 1753 durch eine unterstützte Datum **am nächsten unterstützte Datum ersetzt**. Bei Auswahl dieser Wert standardmäßig nächste wird unterstützte Datum als 01 Januar 1753 ausgewählt werden.  
  
**Batchgröße**  
Während der Datenmigration verwendete Batchgröße. Eine Transaktion ist nach der einzelnen Batches protokolliert. Standardmäßig beträgt die Batchgröße für alle Schemas 10000.  
  
## <a name="see-also"></a>Siehe auch  
[Benutzer-Schnittstelle Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
