---
title: Projekteinstellungen (Konvertierung) (AccessToSQL) | Microsoft Docs
ms.prod: sql
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
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd8aa23b438b5acf14ec0748b464ffe228415721
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="project-settings-conversion-accesstosql"></a>Projekteinstellungen (Konvertierung) (AccessToSQL)
Die Konvertierung projekteinstellungen können Sie konfigurieren, wie Objekte aus den Zugriff auf Datenbankobjekte zu umgewandelt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte.  
  
Bereich Konvertierung finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder.  
  
-   Verwenden der **Projekteinstellungen** (Dialogfeld), Konfigurationsoptionen für das aktuelle Projekt festzulegen. Die Konvertierungseinstellungen für den Zugriff auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie auf **allgemeine** am unteren Rand des linken Bereich, und klicken Sie dann wählen **Konvertierung**.  
  
-   Verwenden der **Projekt Standardeinstellungen** (Dialogfeld), Konfigurationsoptionen für alle Projekte festzulegen. Zum Zugriff auf den Konvertierungseinstellungen für die in den **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, Migrationstyp-Projekt für die Einstellungen erforderlich sind, angezeigt oder geändert werden, wählen **Migration Zielversion** Dropdown-Liste, klicken Sie auf **allgemeine** am unteren Rand des linken Bereich, und klicken Sie dann wählen **Konvertierung**.  
  
## <a name="options"></a>enthalten  
**Primärschlüssel hinzufügen**  
Erstellt einen neuen primären Schlüssel in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabelle, wenn eine Access-Tabelle ohne Primärschlüssel oder eindeutigen Index verfügt.  
  
-   **Standardmodus**: "false"  
  
-   **Vollständige**: "false"  
  
-   **Vollständige Modus**: "true"  
  
Wenn in SQL Azure verbunden ist, ist es standardmäßig "Wahr". **Timestamp-Spalten hinzufügen**  
Gibt an, ob es sich bei SSMA einen Zeitstempelwert erstellen soll, wenn es erforderlich ist.  
  
-   **Standardmodus**: entscheiden Sie SSMA ermöglichen  
  
-   **Vollständige**: nie  
  
-   **Vollständige Modus**: entscheiden Sie SSMA ermöglichen  
  
**Enthalten Sie eine Bewertung Datenbericht mit Konvertierung Bewertungsberichte**  
Enthält eine Bewertung von Daten in den Bewertungsbericht an.  
  
-   **Standardmodus**: "true"  
  
-   **Vollständige**: "false"  
  
-   **Vollständige Modus**: "true"  
  
**Nachrichtentyp, wenn ein Primärschlüssel, Spalten NULL-Werte zulässt enthält**  
Gibt den Typ der Nachricht (Warnung, Fehler oder nichts), in der SSMA im Ausgabebereich angezeigt, wenn Primärschlüssel mit Spalten NULL-Werte zulässt gefundenen.  
  
-   **Standardmodus**: Warnung  
  
-   **Vollständige**: keine Nachricht  
  
-   **Vollständige Modus**: Fehler  
  
**Nachrichtentyp, wenn die Fremdschlüsselspalten unterschiedlich lang sind**  
Gibt den Typ der Nachricht (Warnung, Fehler oder nichts), in der SSMA im Ausgabebereich angezeigt, wenn ein Fremdschlüssel mit falscher TEXT gefunden wird.  
  
-   **Standardmodus**: Warnung  
  
-   **Vollständige**: keine Nachricht  
  
-   **Vollständige Modus**: Fehler  
  
**Nachrichtentyp beim Memospalten indiziert werden**  
Gibt den Typ der Nachricht (Warnung, Fehler oder nichts), in der SSMA im Ausgabebereich angezeigt, wenn einen Index gefunden wird, der enthält einem **Memo** Spalte.  
  
-   **Standardmodus**: Warnung  
  
-   **Vollständige**: keine Nachricht  
  
-   **Vollständige Modus**: Fehler  
  
**Warnhinweis anzeigen, wenn eine komplexe Abfrage einen Platzhalter verwendet (\&#42;)**  
Wenn ein Spaltenname in einer SELECT-Anweisung ein Platzhalterzeichen (*) ist, wird eine Warnung in den Bereich Ausgabe und Fehlerliste angezeigt.  
  
-   **Standardmodus**: "true"  
  
-   **Vollständige**: "false"  
  
-   **Vollständige Modus**: "true"  
  
**Warnhinweis anzeigen Sie, wenn Bezeichnername geändert wird**  
Zeigt eine Meldung in den Bewertungsbericht, und klicken Sie im Bereich "Ausgabe" ein, wenn ein Objektname für die Bezeichner von SSMA geändert wird.  
  
-   **Standardmodus**: "true"  
  
-   **Vollständige**: "false"  
  
-   **Vollständige Modus**: "true"  
  
**Warnhinweis anzeigen Sie, wenn Bezeichner in Anführungszeichen eingeschlossen**  
Zeigt eine Meldung in den Bewertungsbericht, und klicken Sie im Bereich "Ausgabe" ein, wenn ein Bezeichner von SSMA zitiert wird. Bezeichner ist erforderlich, wenn der Name ein Schlüsselwort ist oder Sonderzeichen enthält.  
  
-   **Standardmodus**: "true"  
  
-   **Vollständige**: "false"  
  
-   **Vollständige Modus**: "true"  
  
## <a name="see-also"></a>Siehe auch  
[Benutzer-Schnittstelle Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
