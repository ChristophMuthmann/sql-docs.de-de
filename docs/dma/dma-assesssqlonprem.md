---
title: "Führen Sie eine Bewertung der SQL Server-Migration (Data Migration Assistant) | Microsoft Docs"
ms.custom: 
ms.date: 10/04/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: dma
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Assess
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac241b75f8501df03eb7938ab5ab952dd49ddb52
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="perform-a-sql-server-migration-assessment"></a>Führen Sie eine SQL Server-Migrations-Bewertung
Die folgenden schrittweisen Anweisungen unterstützen Sie Ihre erste Bewertung für die Migration zu einer lokalen SQL Server, SQL Server auf einem virtuellen Azure-Computer oder die Azure SQL-Datenbank ausgeführt wird, mithilfe des Migrations-Assistenten Daten ausführen.

## <a name="create-an-assessment"></a>Erstellen Sie eine Bewertung

1.  Wählen Sie die **neu** (+) Symbol ", und wählen Sie dann die **Assessment** Projekttyp.

2.  Legen Sie den Quell- und Ziel-Server-Typ.

    Wenn Sie Ihre lokalen SQL Server-Instanz eine moderne lokalen SQL Server-Instanz oder SQL Server auf einem virtuellen Azure-Computer gehostet aktualisieren, auf den Quell- und Ziel-Servertyp festgelegt **SQL Server**. Wenn Sie zu Azure SQL-Datenbank migrieren, legen Sie stattdessen der Typ des Zielservers auf **Azure SQL-Datenbank**.

3.  Klicken Sie auf **Erstellen**.

    ![Erstellen Sie eine Bewertung](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>Wählen Sie Optionen für die Bewertung

1. Wählen Sie die SQL Server-Zielversion, der Sie für die Migration zu planen.

2. Wählen Sie den Bericht.

   Wenn Sie Ihre SQL Server-Quellinstanz für die Migration einer lokalen SQL Server oder SQL Server auf Azure-VM-Ziele gehostet bewerten, können Sie eine oder beide der folgenden Berichtstypen Bewertung auswählen:

    -   **Kompatibilitätsprobleme**

    -   **Neue Funktionen Empfehlung**

    ![Wählen Sie einen Berichtstyp Assessment für SQL Server-Ziel](../dma/media/AssessmentTypes.png)

   Wenn Sie Ihre SQL Server-Quellinstanz für die Migration zu Azure SQL-Datenbank bewerten, können Sie eine oder beide der folgenden Berichtstypen Bewertung auswählen:

    -   **Überprüfen Sie die Datenbank-Kompatibilitätsgrad**

    -   **Funktionsparität überprüfen**

    ![Wählen Sie die Bewertung Berichtstyp für Ziel-SQL-Datenbank](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>Hinzufügen von Datenbanken zu bewerten

1.  Wählen Sie **Quellen hinzufügen** Verbindung Dropdown-Menü zu öffnen.

2.  Geben Sie die SQL Server-Instanzname, wählen Sie den Authentifizierungstyp, legen Sie die Eigenschaften für die richtige Verbindung und wählen Sie dann **verbinden**.

3.  Wählen Sie die Datenbanken zu bewerten, und wählen Sie dann **hinzufügen**.

    > [!NOTE] 
    > Sie können mehrere Datenbanken entfernen, dazu, während die UMSCHALTTASTE oder STRG-Taste gedrückt halten und dann auf **Quellen entfernen**. Sie können auch Datenbanken von mehreren SQL Server-Instanzen hinzufügen, mit der **Quellen hinzufügen** Schaltfläche.

4.  Klicken Sie auf **Weiter** um die Analyse zu starten.

    ![Hinzufügen von Datenquellen und Starten von assessment](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>Anzeigen der Ergebnisse

Die Dauer der Bewertung der hängt davon ab, die Anzahl der Datenbanken hinzugefügt und das Schemagröße jeder Datenbank. Ergebnisse werden für jede Datenbank angezeigt, sobald sie verfügbar sind.

1.  Wählen Sie die Datenbank, die die Analyse abgeschlossen wurde, und wechseln Sie zwischen **Kompatibilitätsprobleme** und **Feature Empfehlungen** mithilfe der Switcher.

2.  Überprüfen Sie die Kompatibilitätsprobleme über alle von der SQL Server-Zielversion unterstützt Kompatibilitätsgrade, die Sie ausgewählt haben, auf die **Optionen** Seite.

Sie können Kompatibilitätsprobleme überprüfen, durch die Analyse der betroffenen Objekt und seine Details für jedes Problem unter identifiziert **Breaking Changes**, **verhaltensänderungen**, und **als veraltet markierte Funktionen** .

![Anzeigen der Ergebnisse zu assessment](../dma/media/ReviewResults.png)

Auf ähnliche Weise können Sie überprüfen, Feature Empfehlung über **Leistung**, **Speicher**, und **Sicherheit** Bereiche.

Funktion Empfehlungen behandelt eine Reihe von Features wie z. B. In-Memory OLTP und Columnstore, Stretch-Datenbank immer verschlüsselt, Dynamic Data Masking und Transparent Data Encryption.

![Die Funktion Empfehlungen anzeigen](../dma/media/FeatureRecommendations.png)

Geben Sie für Azure SQL-Datenbank die Bewertungen, blockierende Probleme bei der Paketmigration und paritätsprobleme Funktion. Überprüfen Sie die Ergebnisse für beide Anwendungskategorien durch Auswahl bestimmter Optionen.

- Die **SQL Server-Funktionsparität** Kategorie bietet einen umfassenden Satz von Empfehlungen, alternative Ansätze, die in Azure und Schritten verfügbar. Sie hilft bei diesen Aufwand in Ihren Migrationsprojekten zu planen.

  ![Anzeigen von Informationen für SQL Server-Funktionsparität](../dma/media/SQLFeatureParity.png)

- Die **Kompatibilitätsprobleme** Kategorie umfasst teilweise unterstützte oder nicht unterstützte Funktionen, die Migration von einer lokalen SQL Server-Datenbanken zu Azure SQL-Datenbanken zu blockieren. Es stellt Empfehlungen lassen sich diese Probleme beheben bereit.

  ![Kompatibilitätsprobleme anzeigen](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>Exportieren von Ergebnissen

Nachdem alle Datenbanken die Bewertung abgeschlossen haben, wählen Sie **Exportbericht** die Ergebnisse in einer JSON-Datei oder eine CSV-Datei exportieren. Sie können die Daten dann nach Belieben analysieren.

Sie können mehrere Bewertungen gleichzeitig ausgeführt werden und Anzeigen des Status der Bewertungen durch Öffnen der **alle Bewertungen** Seite.
