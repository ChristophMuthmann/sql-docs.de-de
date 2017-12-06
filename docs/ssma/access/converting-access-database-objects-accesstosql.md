---
title: Konvertieren den Zugriff auf Datenbankobjekte (AccessToSQL) | Microsoft Docs
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
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
caps.latest.revision: "22"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 273aa5bf31ffddc9665531297cbca9b8dbfbbd5a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="converting-access-database-objects-accesstosql"></a>Konvertieren den Zugriff auf Datenbankobjekte (AccessToSQL)
Nachdem Sie den Zugriff auf Datenbanken hinzugefügt und verbunden haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, SSMA zeigt die Metadaten für den Zugriff und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte. Sie können nun den Zugriff auf Datenbankobjekte auswählen und dann die Umstellung der Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schemas.  
  
## <a name="the-conversion-process"></a>Konvertierungsprozess  
Konvertieren von Datenbankobjekten nimmt die Objektdefinitionen aus den Metadaten für den Zugriff, konvertiert sie in entsprechende [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, und klicken Sie dann diese Informationen in das Projekt geladen. Sie können dann Anzeigen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte und ihre Eigenschaften mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer.  
  
> [!IMPORTANT]  
> Konvertieren von Objekten erstellt keine Objekte im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Es werden nur die Definitionen von Systemobjekten konvertiert und speichert die Informationen in das SSMA-Projekt.  
  
Bei der Konvertierung druckt SSMA Status an den Ausgabebereich, und Fehler-, Warn- und informationsmeldungen in den Bereich Fehlerliste. Verwenden Sie diese Informationen, um festzustellen, ob Sie zum Ändern der Access-Datenbanken oder die Konvertierung in die gewünschte Konvertierungsergebnisse zu erhalten müssen. Sie können auch die Informationen in den [Access-Datenbanken für die Migration vorbereiten](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114) Thema, um zu bestimmen, was wird und nicht konvertiert werden.  
  
## <a name="setting-conversion-options"></a>Festlegen von Optionen  
Lesen Sie vor dem Konvertieren von Objekten, das Projekt Konvertierungsoptionen in der **Projekteinstellungen** (Dialogfeld). Mithilfe dieses Dialogfelds können Sie festlegen, wie SSMA indizierte Memospalten, Primärschlüssel, foreign Key-Einschränkungen, Zeitstempel und Tabellen ohne Indizes konvertiert. Weitere Informationen finden Sie unter [Projekteinstellungen (Konvertierung)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>Konvertierungsergebnisse  
Die folgende Tabelle zeigt, welche Zugriff Objekte konvertiert werden, und die resultierende [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte:  
  
|Access-Objekt|Resultierende SQL Server-Objekt|  
|-----------------|-------------------------------|  
|table|table|  
|column|column|  
|Index|Index|  
|Fremdschlüssel|Fremdschlüssel|  
|Abfrage|Ansicht<br /><br />Die meisten SELECT-Abfragen werden in Ansichten konvertiert. Andere Abfragen, z. B. UPDATE-Abfragen werden nicht migriert.<br /><br />SELECT-Abfragen, die Parameter werden nicht konvertiert, was auch Kreuztabellenberichten Abfragen.|  
|Bericht|nicht konvertiert.|  
|Formular|nicht konvertiert.|  
|Makro|nicht konvertiert.|  
|Modul|nicht konvertiert.|  
|Standardwert|Standardwert|  
|Zulassen von NULL Length-Eigenschaft für Spalte|CHECK-Einschränkung|  
|Validierungsregel für die Spalte|CHECK-Einschränkung|  
|Validierungsregel für die Tabelle|CHECK-Einschränkung|  
|Primärschlüssel|Primärschlüssel|  
  
## <a name="converting-access-objects"></a>Konvertieren von Access-Objekte  
Um den Zugriff auf Datenbankobjekte zu konvertieren, müssen Sie zuerst die Objekte auswählen, die Sie konvertieren, und lassen dann die Konvertierung SSMA möchten. Anzeige von Ausgabenachrichten bei der Konvertierung auf der **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Wählen Sie aus, und den Zugriff auf Datenbankobjekte in SQL Server- bzw. SQL Azure-Syntax konvertieren**  
  
1.  Erweitern Sie im Metadaten-Explorer für den Zugriff, **Zugriff Metabasis**, und erweitern Sie dann **Datenbanken**.  
  
2.  Führen Sie eine oder mehrere der folgenden:  
  
    -   Um alle Datenbanken zu konvertieren, aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
    -   Zum konvertieren, oder lassen Sie einzelne Datenbanken, wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Zum konvertieren, oder lassen Sie Abfragen, erweitern Sie die Datenbank, und aktivieren bzw. Deaktivieren der **Abfragen** Kontrollkästchen.  
  
    -   Zum konvertieren, oder lassen Sie einzelne Tabellen, erweitern Sie die Datenbank und **Tabellen**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben der Tabelle.  
  
3.  Führen Sie eines der folgenden Verfahren aus:  
  
    -   Zum Konvertieren von Schemas Maustaste **Datenbanken** , und wählen Sie **Schema konvertieren**.  
  
        Sie können auch einzelne Objekte konvertieren. Um ein Objekt zu konvertieren, unabhängig davon, welche Objekte ausgewählt sind, mit der rechten Maustaste in des Objekts, und wählen Sie **Schema konvertieren**.  
  
        Wenn ein Objekt konvertiert wurde, wird es in der Access-Metadaten-Explorer fett formatiert angezeigt.  
  
    -   Zum konvertieren, laden und Migrieren von Schemas und Daten in einem Schritt, Maustaste Datenbanken, und wählen **konvertieren, laden und migrieren**.  
  
4.  Überprüfen Sie die Nachrichten in der **Ausgabe** Bereich und Fehler und Warnungen in der **Fehlerliste** Bereich.  
  
## <a name="altering-tables-and-indexes"></a>Ändern von Tabellen und Indizes  
Nachdem Sie die Metadaten zugreifen, um Konvertierung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten und vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure können Sie ändern [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bzw. SQL Azure-Tabellen und Indizes.  
  
**So ändern Sie Tabellen- oder Eigenschaften**  
  
1.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure Metadaten-Explorer, wählen Sie die Tabelle oder den Index, die Sie ändern möchten.  
  
2.  Auf der **Tabelle** Registerkarte, klicken Sie auf die Eigenschaft, die Sie verwenden möchten, ändern und eingeben, oder wählen Sie die neue Einstellung. Sie können z. B. nvarchar(15) in nvarchar(20) ändern, oder wählen Sie ein Kontrollkästchen, um eine Spalte NULL-Werte zulässt.  
  
    Bewegen des Cursors aus der geänderten eigenschaftenzelle an. Dies ist möglich, indem Sie auf eine neue Zeile oder die Tab-Taste drücken.  
  
3.  Klicken Sie auf **Anwenden**.  
  
Sie können jetzt die Änderungen im Code anzeigen, auf die **SQL** Registerkarte.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht [lädt die konvertierten Datenbankobjekte in SQL Server](http://msdn.microsoft.com/en-us/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
