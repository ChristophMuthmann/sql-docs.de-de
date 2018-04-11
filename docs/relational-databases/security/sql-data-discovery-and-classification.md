---
title: SQL-Datenermittlung und -klassifizierung | Microsoft-Dokumentation
description: SQL-Datenermittlung und -klassifizierung
services: sql-server
documentationcenter: ''
author: giladm
manager: shaik
ms.reviewer: carlrab
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-server
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 02/13/2018
ms.author: giladm
ms.openlocfilehash: eee9d5b920f422d000fa4e9cb8b78924cb55b466
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2018
---
# <a name="sql-data-discovery-and-classification"></a>SQL-Datenermittlung und -klassifizierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Die Datenermittlung und -klassifizierung führt ein neues Tool in SSMS (SQL Server Management Studio) für das **Ermitteln**, **Klassifizieren**, **Bezeichnen** & **Melden** von sensiblen Daten in Ihren Datenbanken ein.
Die Ermittlung und Klassifizierung Ihrer sensibelsten Daten (geschäftliche, finanzielle, gesundheitliche, personenbezogene Daten, usw.) kann in dem Informationsschutzformat Ihres Unternehmens eine entscheidende Rolle spielen. Sie kann für Folgendes als Infrastruktur gelten:
* Zur Unterstützung, um Datenschutzstandards und gesetzlich geregelten Konformitätsanforderungen, wie z.B. GDPR, zu entsprechen.
* Steuern des Zugriffs auf und Verstärken der Sicherheit von Datenbanken oder Spalten, die hochsensible Daten enthalten.


> [!NOTE]
> Die Datenermittlung und -klassifizierung werden **in SQL Server 2008 und höher unterstützt**. Weitere Informationen zur Datenermittlung und -klassifizierung in Azure SQL-Datenbanken finden Sie unter [Azure SQL-Datenbank – Datenermittlung und -klassifizierung](https://go.microsoft.com/fwlink/?linkid=866265).

## <a id="subheading-1"></a>Übersicht
Die Datenermittlung und -klassifizierung führen eine Reihe von erweiterten Diensten ein, und sie bilden ein neues SQL Information Protection-Paradigma für den Schutz von Daten, nicht nur von der Datenbank:
* **Ermittlung und Empfehlungen**: Die Klassifizierungsengine überprüft Ihre Datenbank und identifiziert Spalten, die möglicherweise sensible Daten enthalten. Dann besteht die einfache Möglichkeit zum Überprüfen und Anwenden der geeigneten Empfehlungen zur Klassifizierung und zum manuellen Klassifizieren von Spalten.
* **Bezeichnung**: Sensible Daten können dauerhaft mit Klassifizierungsbezeichnungen gekennzeichnet werden.
* **Sichtbarkeit**: Der Klassifizierungsstatus der Datenbank kann in einem detaillierten Bericht im Portal angezeigt werden, der zwecks Konformität und Überwachung sowie anderer Gründe ausgedruckt oder exportiert werden kann.

## <a id="subheading-2"></a>Ermitteln, Klassifizieren und Bezeichnen von sensiblen Spalten
Im folgenden Abschnitt werden die Schritte zum Ermitteln, Klassifizieren und Bezeichnen von Spalten mit sensiblen Daten in Ihrer Datenbank sowie das Anzeigen des aktuellen Klassifizierungsstatus Ihrer Datenbank und das Exportieren von Berichten beschrieben.

Die Klassifizierung umfasst zwei Metadatenattribute:
* Bezeichnungen: Die wichtigsten Klassifizierungsattribute zum Definieren der Vertraulichkeitsstufe der in der Spalte gespeicherten Daten.  
* Informationstypen: Sie bieten zusätzliche Granularität für den Typ der in der Spalte gespeicherten Daten.

<br>
**Klassifizieren Ihrer SQL Server-Datenbank:**

1. Stellen Sie in SSMS (SQL Server Management Studio) eine Verbindung zu SQL Server her.

2. Führen Sie im Objekt-Explorer von SSMS einen Rechtsklick auf die Datenbank aus, die Sie klassifizieren möchten, und wählen Sie dann **Tasks** > **Classify Data...** (Aufgaben > Daten klassifizieren...) aus.

    ![Navigationsbereich][1]

3. Die Klassifizierungsengine prüft Ihre Datenbank auf Spalten, die potenziell sensible Daten enthalten, und erstellt eine Liste der **empfohlenen Spaltenklassifizierungen**:

    * Klicken Sie auf das Benachrichtigungsfeld für die Empfehlungen im oberen Rand des Fensters, oder klicken Sie auf den Bereich für Empfehlungen im unteren Rand des Fensters, um eine Liste der empfohlenen Spaltenklassifizierungen anzuzeigen:

        ![Navigationsbereich][2]

        ![Navigationsbereich][3]

    * Überprüfen Sie die Liste der Empfehlungen:
        * Zum Akzeptieren einer Empfehlung für eine bestimmte Spalte aktivieren Sie das Kontrollkästchen in der linken Spalte der entsprechenden Zeile. Sie können auch *alle Empfehlungen* als akzeptiert markieren, indem Sie das Kontrollkästchen im Tabellenkopf der Empfehlungen aktivieren.

        * Sie können auch den empfohlenen Informationstyp und die Vertraulichkeitsbezeichnung mithilfe der Dropdownfelder ändern.        

        ![Navigationsbereich][4]

    * Klicken Sie zum Anwenden Ihrer ausgewählten Empfehlungen auf die blaue Schaltfläche **Accept selected recommendations** (Ausgewählte Änderungen akzeptieren).

        ![Navigationsbereich][5]

4. Alternativ oder zusätzlich zur empfehlungsbasierten Klassifizierung können Sie Spalten auch **manuell klassifizieren**:

    * Klicken Sie im oberen Menü des Fensters auf **Klassifizierung hinzufügen**.

        ![Navigationsbereich][6]

    * Wählen Sie im daraufhin geöffneten Kontextfenster das Schema, die Tabelle und dann die Spalte, die Sie klassifizieren möchten, sowie den Informationstyp und die Vertraulichkeitsbezeichnung aus. Klicken Sie dann auf die Schaltfläche **Klassifizierung hinzufügen** am unteren Rand des Kontextfensters.

        ![Navigationsbereich][7]

5. Klicken Sie im oberen Menü des Fensters auf **Speichern**, um Ihre Klassifizierung zu vervollständigen und die Datenbankspalten dauerhaft mit den neuen Klassifizierungsmetadaten zu bezeichnen (Tag).

    ![Navigationsbereich][8]


6. Klicken Sie im oberen Menü des Fensters auf **Bericht anzeigen**, um einen Bericht mit einer vollständigen Zusammenfassung des Klassifizierungsstatus der Datenbank zu generieren.

    ![Navigationsbereich][9]

    ![Navigationsbereich][10]


## <a id="subheading-3"></a>Nächste Schritte

Weitere Informationen zur Datenermittlung und -klassifizierung in Azure SQL-Datenbanken finden Sie unter [Azure SQL-Datenbank – Datenermittlung und -klassifizierung](https://go.microsoft.com/fwlink/?linkid=866265).

Ziehen Sie in Betracht, Ihre sensiblen Spalten durch Anwenden von Sicherheitsmechanismen auf der Spaltenebene zu schützen:

* [Dynamische Datenmaskierung](https://docs.microsoft.com/en-us/sql/relational-databases/security/dynamic-data-masking) zum Verbergen der verwendeten sensiblen Spalten.
* [Immer verschlüsselt](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine) zum Verschlüsseln der sensiblen Spalten im Ruhezustand.

<!--Anchors-->
[SQL Data Discovery & Classification overview]: #subheading-1
[Discovering, classifying & labeling sensitive columns]: #subheading-2
[Next Steps]: #subheading-3

<!--Image references-->
[1]: ./media/sql-data-discovery-and-classification/1_data_classification_explorer_menu.png
[2]: ./media/sql-data-discovery-and-classification/2_recommendations_notification_box.png
[3]: ./media/sql-data-discovery-and-classification/3_recommendations_panel.png
[4]: ./media/sql-data-discovery-and-classification/4_recommendations.png
[5]: ./media/sql-data-discovery-and-classification/5_accept_recommendations_button.png
[6]: ./media/sql-data-discovery-and-classification/6_add_classification_button.png
[7]: ./media/sql-data-discovery-and-classification/7_manual_classification.png
[8]: ./media/sql-data-discovery-and-classification/8_save.png
[9]: ./media/sql-data-discovery-and-classification/9_view_report.png
[10]: ./media/sql-data-discovery-and-classification/10_report.png
