---
title: Verknüpfen von Access-Anwendungen mit SQLServer - Azure SQL-Datenbank | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases, linking to SQL Azure
- Access databases, linking to SQL Server
- auto-increment columns
- data types, unsupported
- hyperlink columns
- linking tables
- migrating databases, post-migration issues
- post-migration issues
- reference, post-migration issues
- refreshing linked tables
- slow performance
- unlinking tables
ms.assetid: 82374ad2-7737-4164-a489-13261ba393d4
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: f33165118c2d7143ba75944b6515eca1338cce09
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>Verknüpfen von Access-Anwendungen mit SQL Server - Azure SQL-Datenbank (AccessToSQL)
Wenn Sie die vorhandenen Access-Anwendungen mit verwenden möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können Sie die ursprünglichen Access-Tabellen verknüpfen, um die migrierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabellen. Verknüpfen die Access-Datenbank ändert, sodass Ihre Abfragen, Formulare, Berichte und Datenzugriffsseiten die Daten im Verwenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank nicht die Daten in der Access-Datenbank.  
  
> [!NOTE]  
> Die Access-Tabellen verbleiben in den Zugriff, jedoch nicht aktualisiert werden, zusammen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure aktualisiert. Nachdem Sie die Tabellen verknüpfen und überprüfen Sie die Funktionalität, empfiehlt es sich um die Access-Tabellen zu löschen.  
  
## <a name="linking-access-and-sql-server-tables"></a>Verknüpfen von Access und SQL Server-Tabellen  
Wenn Sie eine Access-Tabelle zu verknüpfen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabelle, die Jet-Datenbankmodul speichert, Verbindungsinformationen und Tabellenmetadaten, aber die Daten werden gespeichert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Diese Verknüpfung ermöglicht die Access-Anwendungen für die Access-Tabellen ausgeführt werden, obwohl in der tatsächlichen Tabellen und Daten sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
> [!NOTE]  
> Bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, Ihr Kennwort in Klartext auf verknüpften Access-Tabellen gespeichert ist. Es wird empfohlen, mithilfe der Windows-Authentifizierung.  
  
**Verknüpfen von Tabellen**  
  
1.  Wählen Sie in Access-Metadaten-Explorer die Tabellen, die Sie verknüpfen möchten.  
  
2.  Mit der rechten Maustaste **Tabellen**, und wählen Sie dann **Link**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) for Access sichert die ursprünglichen Access-Tabelle und eine verknüpfte Tabelle erstellt.  
  
Nachdem Sie die Tabellen verknüpft, werden die Tabellen in SSMA mit einem kleinen Linksymbol angezeigt. In Access erscheinen die Tabellen mit einem "verknüpfte"-Symbol, also eine Kugel mit einem Pfeil darauf zeigen.  
  
Wenn Sie eine Tabelle in Access öffnen, werden die Daten abgerufen, einen Keyset-Cursor verwenden. Daher bei großen Tabellen alle Daten werden abgerufen gleichzeitig. Wie Sie die Tabelle durchsuchen, ruft Zugriff jedoch nach Bedarf zusätzliche Daten ab.  
  
> [!IMPORTANT]  
> Um den Zugriff auf Tabellen mit einer Azure-Datenbank zu verknüpfen, die Sie benötigen SQL Server Native Client(SNAC) Version 10.5 oder höher.   
> Sie erhalten die neueste Version der SNAC aus [Microsoft® SQL Server® 2008 R2 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=196940).  
  
## <a name="unlinking-access-tables"></a>Aufheben der Verknüpfung den Zugriff auf Tabellen  
Wenn Sie die Verknüpfung aufheben einer Access-Tabelle aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabelle, SSMA stellt die ursprünglichen Access-Tabelle und seine Daten wieder her.  
  
**Verknüpfung von Tabellen**  
  
1.  Wählen Sie in Access-Metadaten-Explorer die Tabellen, die Sie aufheben möchten.  
  
2.  Mit der rechten Maustaste **Tabellen**, und wählen Sie dann **aufheben**.  
  
## <a name="linking-tables-to-a-different-server"></a>Verknüpfen von Tabellen mit einem anderen server  
Wenn Sie die Access-Tabellen, um eine SQL Server-Instanz verknüpft haben, und Sie später die Links in eine andere Instanz ändern möchten, müssen Sie die Tabellen erneut verknüpfen.  
  
**Zum Verknüpfen von Tabellen mit einem anderen server**  
  
1.  Wählen Sie in Access-Metadaten-Explorer die Tabellen, die Sie aufheben möchten.  
  
2.  Mit der rechten Maustaste **Tabellen** und wählen Sie dann **aufheben**.  
  
3.  Klicken Sie auf die **eine erneute Verbindung mit SQL Server** Schaltfläche.  
  
4.  Herstellen einer Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure Access-Tabellen verknüpft werden sollen.  
  
5.  Wählen Sie in Access-Metadaten-Explorer die Tabellen, die Sie verknüpfen möchten.  
  
6.  Mit der rechten Maustaste **Tabellen**, und wählen Sie dann **Link**.  
  
## <a name="updating-linked-tables"></a>Aktualisieren von verknüpften Tabellen  
Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabellendefinitionen geändert werden, können Sie aufheben und dann erneut verknüpfen die Tabellen in SSMA mit den Prozeduren weiter oben in diesem Thema. Sie können auch die Tabellen aktualisieren, mithilfe von Access.  
  
**So aktualisieren Sie verknüpfte Tabellen mithilfe von Access**  
  
1.  Öffnen Sie die Access-Datenbank.  
  
2.  In der **Objekte** auf **Tabellen**.  
  
3.  Mit der rechten Maustaste einer verknüpften Tabelle, und wählen Sie dann **verknüpfte Tabelle Manager**.  
  
4.  Wählen Sie das Kontrollkästchen neben jeder verknüpfte Tabelle, die Sie aktualisieren möchten, und klicken Sie dann auf **OK**.  
  
## <a name="possible-post-migration-issues"></a>Mögliche Probleme bei der nach der Paketmigration  
Die folgenden Abschnitte, die in vorhandenen Access-Anwendungen auftreten können, nach dem Migrieren von Datenbanken aus Zugriff auf Probleme mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure und verknüpfen Sie die Tabellen, zusammen mit den Ursachen und Lösungen.  
  
### <a name="slow-performance-with-linked-tables"></a>Langsame Leistung mit verknüpften Tabellen  
**Ursache:** einige Abfragen sind u. u. langsam nach Upsizing von den folgenden Gründen:  
  
-   Die Anwendung hängt von Funktionen, die nicht in vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, wodurch Jet, Tabellen, lokal zum Ausführen einer SELECT-Abfrage zu ziehen.  
  
-   Abfragen, die aktualisieren oder Löschen von vielen Zeilen, werden für jede Zeile von Jet als eine parametrisierte Abfrage gesendet.  
  
**Lösung:** konvertieren Sie Pass-Through-Abfragen, gespeicherten Prozeduren oder Sichten die langsam ausgeführte Abfragen. Konvertieren in Pass-Through-Abfragen weist folgende Probleme auf:  
  
-   Pass-Through-Abfragen werden nicht geändert. Neue Datensätze hinzufügen oder ändern das Ergebnis der Abfrage vorgenommen werden auf eine andere Weise, wie z. B. durch die Verwendung expliziter **ändern** oder **hinzufügen** Schaltflächen auf dem Formular, das an die Abfrage gebunden ist.  
  
-   Einige Abfragen eine Benutzereingabe erforderlich ist, aber Pass-Through-Abfragen unterstützen keine Benutzereingaben. Benutzereingaben kann abgerufen werden, indem Sie Visual Basic for Applications (VBA) Code, der für Parameter fordert oder ein Formular, das als eines Eingabesteuerelements verwendet wird. In beiden Fällen übermittelt der VBA-Code für die Abfrage mit der Benutzereingabe mit dem Server.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>Automatisch inkrementierte Spalten werden nicht aktualisiert werden, bis der Datensatz aktualisiert wurde  
**Ursache:** nach dem Aufruf von RecordSet.AddNew in Jet aus, die Auto-Inkrement-Spalte ist verfügbar, bevor der Datensatz aktualisiert wurde. Dies ist nicht in "true" [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Der neue Wert der neue Wert für die Identitätsspalte steht erst nach dem Speichern des neuen Datensatzes zur Verfügung.  
  
**Lösung:** führen Sie die folgenden Visual Basic for Applications (VBA)-Code vor dem Zugriff auf das Identitätsfeld:  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>Neue Datensätze sind nicht verfügbar  
**Ursache:** beim Hinzufügen eines Datensatzes zu einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabelle mit VBA, wenn die Tabellenfeld eindeutiger Index den Standardwert hat, und Sie keinen Wert zu diesem Feld der neue Datensatz wird nicht angezeigt weisen, bis Sie die Tabelle erneut öffnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder S SQL Azure. Wenn Sie versuchen, einen Wert aus der neue Datensatz abrufen, erhalten Sie die folgende Fehlermeldung angezeigt:  
  
`Run-time error '3167' Record is deleted.`  
  
**Lösung:** beim Öffnen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabelle, indem Sie VBA-Code verwenden, schließen Sie die `dbSeeChanges` auswählen, wie im folgenden Beispiel gezeigt:  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>Nach der Migration werden einige Abfragen nicht der Benutzer einen neuen Datensatz hinzufügen kann  
**Ursache:** , wenn eine Abfrage nicht alle Spalten enthalten, die in einem eindeutigen Index enthalten sind, können nicht Sie neue Werte hinzufügen, indem Sie mit der Abfrage.  
  
**Lösung:** stellen Sie sicher, dass alle im mindestens einen eindeutigen Index enthaltenen Spalten Teil der Abfrage sind.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>Eine verknüpfte Tabellenschema Zugriff kann nicht geändert werden.  
**Ursache:** nach der Migration von Daten und verknüpfen Tabellen kann nicht der Benutzer das Schema einer Tabelle in Access ändern.  
  
**Lösung:** ändern das Tabellenschema mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], und aktualisieren Sie dann auf den Link in Access.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>Hyperlinkfunktionalität ist nach der Migration verloren gehen Daten  
**Ursache:** nach der Migration der Daten, Hyperlinks in Spalten verlieren ihre Funktionalität und werden einfache **nvarchar(max)** Spalten.  
  
**Lösung:** None.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>Einige SQL Server-Datentypen werden von den Zugriff nicht unterstützt.  
**Ursache:** Wenn Sie später ein update Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabellen-Datentypen enthält, die von Access, nicht unterstützt werden nicht möglich, öffnen Sie die Tabelle in Access.  
  
**Lösung:** können Sie eine Access-Abfrage, die nur die Zeilen mit unterstützten Datentypen zurückgibt definieren.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
