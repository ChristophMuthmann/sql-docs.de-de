---
title: Herstellen einer Verbindung mit Azure SQL-Datenbank (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
caps.latest.revision: "21"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2573e0aa114381dc90e21ab2a871453793ddc13d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>Herstellen einer Verbindung mit Azure SQL-Datenbank (AccessToSQL)
Um Access-Datenbanken zu SQL Azure zu migrieren, müssen Sie mit der Zielinstanz von SQL Azure verbinden. Wenn Sie eine Verbindung herstellen, wird SSMA Ruft Metadaten zu allen Datenbanken in der Instanz von SQL Azure ab und Datenbank-Metadaten in der SQL Azure-Metadaten-Explorer zeigt. SSMA speichert Informationen über die Instanz von SQL Azure verbunden sind, jedoch werden Kennwörter nicht gespeichert.  
  
Die Verbindung mit SQL Azure bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie in SQL Azure erneut, wenn Sie möchten, dass eine aktive Verbindung mit dem Server verbinden. Sie können offline arbeiten, bis Sie Datenbankobjekte in SQL Azure laden und Migrieren von Daten.  
  
Metadaten zur Instanz von SQL Azure werden nicht automatisch synchronisiert. Um die Metadaten in SQL Azure-Metadaten-Explorer zu aktualisieren, müssen Sie stattdessen manuell die SQL Azure-Metadaten aktualisieren. Weitere Informationen finden Sie im Abschnitt "Synchronisieren von SQL Azure-Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-sql-azure-permissions"></a>Erforderliche SQL Azure-Berechtigungen  
Das Konto, das verwendet wird, für die Verbindung zu SQL Azure erfordert unterschiedliche Berechtigungen abhängig von den Aktionen, die das Konto ausführt:  
  
-   Zugreifen auf Objekte zu konvertieren [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, um Metadaten von SQL Azure zu aktualisieren oder konvertierte Syntax zum Speichern von Skripts, das Konto muss über die Berechtigung zum Anmelden bei der Instanz von SQL Azure.  
  
-   Zum Laden von Datenbankobjekten in SQL Azure ist die Mindestberechtigung Anforderung die Mitgliedschaft in der **Db_owner** Datenbankrolle in der Zieldatenbank.  
  
## <a name="establishing-a-sql-azure-connection"></a>Einrichten einer SQL Azure-Verbindung  
Bevor Sie den Zugriff auf Datenbankobjekte in Azure SQL-Syntax konvertieren, müssen Sie eine Verbindung mit der Instanz von SQL Azure einrichten, wo Sie die Access-Datenbank oder Datenbanken migrieren möchten.  
  
Wenn Sie die Verbindungseigenschaften definieren, geben Sie auch die Datenbank, in denen Objekte und Daten migriert werden sollen. Sie können diese Zuordnung auf der Ebene des Zugriffs nach dem Herstellen einer Verbindung mit SQL Azure anpassen. Weitere Informationen finden Sie unter [Zuordnen von Microsoft Access-Datenbanken in SQL Server-Schemas](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung zu SQL Azure herstellen, stellen Sie sicher, dass die Instanz von SQL Azure ausgeführt wird und Verbindungen akzeptieren kann.  
  
**Verbindung mit SQL Azure**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit SQL Azure** (diese Option ist nach der Erstellung eines Projekts).  
  
    Wenn Sie zuvor in SQL Azure verbunden, wird der Befehlsname sein **eine erneute Verbindung mit SQL Azure**.  
  
2.  Klicken Sie im Dialogfeld Verbindung geben Sie ein, oder wählen Sie den Namen des SQL Azure.  
  
3.  Geben Sie ein, wählen oder **Durchsuchen** den Datenbanknamen.  
  
4.  Geben Sie ein oder wählen Sie **Benutzername**.  
  
5.  Geben Sie die **Kennwort**.  
  
6.  SSMA empfiehlt verschlüsselte Verbindung zu SQL Azure.  
  
7.  Klicken Sie auf **Verbinden**.  
  
> [!IMPORTANT]  
> SSMA für Access unterstützt keine Verbindung mit **master** Datenbank in SQL Azure.  
  
Wenn keine Datenbanken im SQL Azure-Konto vorhanden sind, können Sie erstellen, die erste Datenbank mit **Azure-Datenbank erstellen** Optionen, die auf einem Klick auf angezeigt **Durchsuchen** Schaltfläche.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Synchronisieren von SQL Azure-Metadaten  
Metadaten zu SQL Azure-Datenbanken wird nicht automatisch aktualisiert. Die Metadaten im Metadaten-Explorer von SQL Azure ist eine Momentaufnahme der Metadaten, wenn Sie zunächst mit SQL Azure verbunden, oder der letzten Ausführung, die Sie manuell die Metadaten aktualisiert. Sie können die Metadaten für alle Datenbanken oder für jede einzelne Datenbank oder ein Datenbankobjekt manuell aktualisieren.  
  
**Zum Synchronisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit SQL Azure verbunden sind.  
  
2.  Wählen Sie in SQL Azure-Metadaten-Explorer das Kontrollkästchen neben der Datenbank oder das Datenbankschema, die Sie aktualisieren möchten.  
  
    Angenommen, um die Metadaten für alle Datenbanken zu aktualisieren, wählen Sie das Kontrollkästchen neben den Datenbanken an.  
  
3.  Mit der rechten Maustaste Datenbanken, oder die einzelne Datenbank oder das Datenbankschema, und wählen Sie dann **mit Datenbank synchronisieren**.  
  
## <a name="refreshing-sql-azure-metadata"></a>Aktualisieren von SQL Azure-Metadaten  
Wenn SQL Azure-Schemas ändern, nachdem Sie eine Verbindung herstellen, können Sie Metadaten vom Server aktualisieren.  
  
**Aktualisieren von SQL Azure-Metadaten**  
  
-   Klicken Sie in SQL Azure-Metadaten-Explorer mit der rechten Maustaste auf **Datenbanken**, und wählen Sie dann **aus der Datenbank aktualisieren**.  
  
## <a name="reconnecting-to-sql-azure"></a>Erneutes Herstellen einer Verbindung mit SQL Azure  
Die Verbindung mit SQL Azure bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie in SQL Azure erneut, wenn Sie möchten, dass eine aktive Verbindung mit dem Server verbinden. Sie können offline arbeiten, bis Sie Datenbankobjekte in SQL Azure laden und Migrieren von Daten.  
  
Das Verfahren zum Wiederherstellen der Verbindung mit SQL Azure ist das Verfahren zum Herstellen einer Verbindung identisch.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Wenn Sie die Zuordnung zwischen Schemas Access und SQL Azure-Datenbanken und Schemas anpassen zu können, finden Sie unter [Zuordnung Access-Datenbanken in SQL Server-Schemas](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4).  
  
-   Konfigurationsoptionen für die Projekte anpassen können, finden Sie unter [Einstellung Projektoptionen](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167).  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnungsquelle und Ziel-Datentypen](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
-   Wenn Sie nicht verfügen, um diese Aufgaben auszuführen, können Sie die Objektdefinitionen für Access-Datenbank in SQL Azure-Objektdefinitionen konvertieren. Weitere Informationen finden Sie unter [Konvertieren von Access-Datenbanken](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
