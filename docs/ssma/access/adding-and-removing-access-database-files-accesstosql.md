---
title: Hinzufügen und Entfernen von Access-Datenbankdateien (AccessToSQL) | Microsoft Docs
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
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc44607d172ebc1f8d7d09b68ba77d68002de2bb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Hinzufügen und Entfernen von Access-Datenbankdateien (AccessToSQL)
Migrieren von Access-Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, müssen Sie mindestens eine Access-Datenbanken die SSMA-Projekt hinzufügen. Diese Datenbanken müssen Access 97 oder höher sein. Wenn Sie Datenbanken aus einer früheren Version von Access verfügen, müssen Sie die Datenbanken auf eine neuere Version konvertieren. Dazu öffnen und speichern die Datenbanken in Access 97 oder höher, bevor Sie sie SSMA hinzufügen.  
  
## <a name="what-happens-when-you-add-access-database-files"></a>Was geschieht, wenn Sie die Access-Datenbankdateien hinzufügen?  
Wenn Sie eine Access-Datenbank zu einem SSMA-Projekt hinzufügen, SSMA Datenbankmetadaten liest, und klicken Sie dann die Projektdatei diese Metadaten hinzugefügt. Diese Metadaten werden der Datenbank und seine Objekte beschrieben. SSMA anhand der Metadaten aus, wenn Objekte konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax, und wenn sie Daten migriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können diese Metadaten in Access-Metadaten-Explorer durchsuchen und überprüfen Sie die Eigenschaften der einzelnen Datenbankobjekte.  
  
> [!NOTE]  
> Eine Access-Datenbank kann in mehrere Dateien aufgeteilt werden: ein Back-End-Datenbank, die Tabellen enthält, und die Front-End-Datenbanken, Abfragen, Formulare, Berichte, Makros, Module und Verknüpfungen enthalten. Wenn Sie eine Teilung Datenbank migrieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, die Front-End-Datenbank SSMA hinzuzufügen.  
  
## <a name="permissions-that-are-required-by-ssma"></a>Berechtigungen, die von SSMA erforderlich sind  
Zum Migrieren einer Access-Datenbank zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, die Benutzergruppe und die Admin-Benutzer müssen über Verwaltungsberechtigungen verfügen. Informationen zum Migrieren von Datenbanken mit Arbeitsgruppe Schutz finden Sie unter [Access-Datenbanken für die Migration vorbereiten](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
## <a name="selecting-databases-to-add"></a>Auswählen von Datenbanken hinzufügen  
Wenn Sie eine oder mehrere Datenbanken zu einem SSMA-Projekt hinzufügen möchten, und die Dateien befinden sich alle in einem bekannten Speicherort, können Sie die Dateien hinzufügen, indem Sie mithilfe des folgenden Verfahrens.  
  
**So fügen Sie einzelne Datenbankdateien hinzu**  
  
1.  Auf der **Datei** Menü klicken Sie auf **Datenbanken hinzufügen**.  
  
2.  In der **öffnen** Dialogfeld Feld, suchen Sie den Ordner, der die Datenbankdatei oder Dateien enthält.  
  
3.  Wählen Sie die Dateien, die Sie hinzufügen möchten, und klicken Sie dann auf **öffnen**.  
  
## <a name="finding-databases-to-add"></a>Suchen von Datenbanken hinzufügen  
Wenn Sie mehrere Access-Datenbanken in unterschiedlichen Ordnern zu einem SSMA-Projekt hinzufügen möchten, oder Sie verwenden möchten, fügen eine einzelne Datei, jedoch müssen Sie die Datei nicht finden, können Sie die folgenden Schritte durchführen, um eine weitere Dateien suchen, und fügen sie dem Projekt hinzu.  
  
**Suchen und Hinzufügen von Datenbanken**  
  
1.  Auf der **Datei** Menü klicken Sie auf **Datenbanken suchen**.  
  
2.  Geben Sie den Namen des Laufwerks, Dateipfad oder den UNC-Pfad, den Sie suchen möchten, klicken Sie im Assistenten zum Suchen von Datenbanken. Klicken Sie alternativ auf **Durchsuchen** auf dem Laufwerk oder Ordner zu suchen.  
  
3.  Klicken Sie auf **hinzufügen** auf den Speicherort der Liste hinzufügen.  
  
    Wiederholen Sie die vorherigen beiden Schritte, um weitere Suche Speicherorte hinzuzufügen.  
  
4.  Fügen Sie Suchkriterien, um die Liste der Datenbanken zu optimieren, die zurückgegeben werden.  
  
    > [!IMPORTANT]  
    > Die **alle oder einen Teil des Dateinamens** Textfeld unterstützt keine Platzhalterzeichen enthalten.  
  
5.  Klicken Sie auf **Scan**.  
  
    Die Seite "Überprüfung" wird angezeigt. Dies zeigt die Datenbanken, die gefunden wurden, und den Fortschritt der Suche. Um die Suche zu beenden, klicken Sie auf **beenden**.  
  
6.  Wählen Sie auf der Seite "Dateien auswählen" die Datenbanken, die Sie dem Projekt hinzufügen möchten.  
  
    Können Sie die **Alles markieren** und **alle löschen** Schaltflächen am oberen Rand der Liste aktivieren oder deaktivieren Sie alle Datenbanken. Sie können die STRG-Taste gedrückt, um mehrere Datenbanken auszuwählen oder gedrückter Umschalttaste auf Wählen Sie einen Bereich von Datenbanken.  
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Klicken Sie auf der Seite "Überprüfen" auf **Fertig stellen**.  
  
## <a name="browsing-access-metadata"></a>Durchsuchen von Metadaten zugreifen  
Nachdem Sie eine Access-Datenbank zu einem Projekt hinzugefügt haben, wird die Projektmetadaten im Access-Metadaten-Explorer angezeigt. Sie können die Hierarchie von Datenbanken und Datenbankobjekte im Explorer durchsuchen.  
  
**Durchsuchen von Metadaten**  
  
1.  Erweitern Sie im Metadaten-Explorer für den Zugriff, **Zugriff Metabasis**, und erweitern Sie dann **Datenbanken**.  
  
2.  Erweitern Sie die Datenbank, die Sie überprüfen möchten, und erweitern dann **Abfragen**.  
  
    Beachten Sie die Liste der Abfragen. Wenn Sie eine Abfrage Auswählen einer **SQL** Registerkarte und eine **Eigenschaften** Registerkarte im rechten Bereich angezeigt.  
  
3.  Erweitern Sie **Tabellen** und wählen Sie eine Tabelle.  
  
    Beachten Sie, dass vier Registerkarten angezeigt: **Tabelle**, **Type Mapping**, **Eigenschaften**, und **Daten**.  
  
4.  Erweitern Sie eine Tabelle und **Schlüssel**, und wählen Sie einen Schlüssel.  
  
    Die wichtigsten Eigenschaften werden im rechten Bereich angezeigt.  
  
5.  Erweitern Sie **Indizes**, und wählen Sie einen Index.  
  
    Die Indexeigenschaften werden im rechten Bereich angezeigt.  
  
## <a name="refreshing-databases"></a>Aktualisieren von Datenbanken  
Wenn Sie eine Access-Datenbank ändert, nachdem Sie die Datei hinzufügen, können Sie Metadaten aus der Access-Datenbank aktualisieren.  
  
**So aktualisieren Sie Metadaten für den Zugriff**  
  
-   In Access-Metadaten-Explorer mit der rechten Maustaste in der Datenbank, und wählen Sie dann **aus der Datenbank aktualisieren**.  
  
## <a name="removing-databases"></a>Entfernen von Datenbanken  
Sie können eine Access-Datenbank aus einem Projekt entfernen, indem Sie folgende Schritte.  
  
**So entfernen Sie eine Datenbank aus einem Projekt**  
  
1.  Erweitern Sie im Metadaten-Explorer für den Zugriff, **Zugriff Metabasis**, und erweitern Sie dann **Datenbanken**.  
  
2.  Mit der rechten Maustaste in der Datenbank, und wählen Sie dann **"Datenbank entfernen"**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [Herstellen einer Verbindung mit SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Erstellen und Verwalten von Projekten](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)  
  
