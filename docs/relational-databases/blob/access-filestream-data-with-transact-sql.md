---
title: Zugreifen auf FILESTREAM-Daten mit Transact-SQL | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], Transact-SQL
ms.assetid: a6bf0ce7-7e5e-4a07-8917-ee526c9d0a05
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 45427055e31abac50860698b80c11ff3f0526f0a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="access-filestream-data-with-transact-sql"></a>ZUgreifen auf FILESTREAM-Daten mit Transact-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema erfahren Sie, wie Sie FILESTREAM-Daten mit den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen INSERT, UPDATE und DELETE verwalten.  
  
> [!NOTE]  
>  Für die Beispiele in diesem Thema sind die FILESTREAM-aktivierte Datenbank und die Tabelle erforderlich, die unter [Erstellen einer FILESTREAM-aktivierten Datenbank](../../relational-databases/blob/create-a-filestream-enabled-database.md) und [Erstellen einer Tabelle zum Speichern von FILESTREAM-Daten](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)erstellt werden.  
  
##  <a name="ins"></a> Einfügen einer Zeile mit FILESTREAM-Daten  
 Zum Hinzufügen einer Zeile in einer Tabelle, die FILESTREAM-Daten unterstützt, verwenden Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung INSERT. Wenn Sie Daten in eine FILESTREAM-Spalte einfügen, können Sie NULL oder einen **varbinary(max)** -Wert einfügen.  
  
### <a name="inserting-null"></a>Einfügen von NULL  
 Im folgenden Beispiel wird gezeigt, wie `NULL`eingefügt wird. Wenn der FILESTREAM-Wert `NULL`ist, erstellt [!INCLUDE[ssDE](../../includes/ssde-md.md)] keine Datei im Dateisystem.  
  
 [!code-sql[FILESTREAM#FS_InsertNULL](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_1.sql)]  
  
### <a name="inserting-a-zero-length-record"></a>Einfügen eines Datensatzes mit der Länge 0 (null)  
 Das folgende Beispiel veranschaulicht, wie mit `INSERT` ein Datensatz mit der Länge 0 (null) erstellt wird. Dies ist hilfreich, wenn Sie ein Dateihandle abrufen müssen, die Datei jedoch durch die Verwendung von Win32-APIs geändert wird.  
  
 [!code-sql[FILESTREAM#FS_InsertZero](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_2.sql)]  
  
### <a name="creating-a-data-file"></a>Erstellen einer Datendatei  
 Das folgende Beispiel veranschaulicht, wie mit `INSERT` eine Datei mit Daten erstellt wird. [!INCLUDE[ssDE](../../includes/ssde-md.md)] konvertiert die Zeichenfolge `Seismic Data` in einen `varbinary(max)` -Wert. FILESTREAM erstellt die Windows-Datei, falls diese noch nicht erstellt wurde. Die Daten werden dann der Datendatei hinzugefügt.  
  
 [!code-sql[FILESTREAM#FS_InsertData](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_3.sql)]  
  
 Wenn Sie alle Daten in der Tabelle `Archive.dbo.Records` auswählen, sollten ähnliche Ergebnisse wie in der folgenden Tabelle angezeigt werden. Die `Id` -Spalte enthält jedoch andere GUIDs.  
  
|ID|SerialNumber|Diagramm|  
|--------|------------------|------------|  
|`C871B90F-D25E-47B3-A560-7CC0CA405DAC`|`1`|`NULL`|  
|`F8F5C314-0559-4927-8FA9-1535EE0BDF50`|`2`|`0x`|  
|`7F680840-B7A4-45D4-8CD5-527C44D35B3F`|`3`|`0x536569736D69632044617461`|  
  
  
##  <a name="upd"></a> Aktualisieren von FILESTREAM-Daten  
 Sie können [!INCLUDE[tsql](../../includes/tsql-md.md)] zum Aktualisieren der Daten in der Dateisystemdatei verwenden. Dies ist jedoch nicht empfehlenswert, wenn Sie große Datenmengen in eine Datei streamen müssen.  
  
 Im folgenden Beispiel wird der gesamte Text im Dateidatensatz durch den Text `Xray 1`ersetzt.  
  
 [!code-sql[FILESTREAM#FS_UpdateData](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_4.sql)]  
  
  
##  <a name="del"></a> Löschen von FILESTREAM-Daten  
 Wenn Sie eine Zeile mit einem FILESTREAM-Feld löschen, löschen Sie auch die zugrunde liegenden Dateisystemdateien. Die einzige Möglichkeit zum Löschen einer Zeile, und somit der Datei, ist die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung DELETE.  
  
 Im folgenden Beispiel wird das Löschen einer Zeile und der entsprechenden Dateisystemdateien veranschaulicht.  
  
 [!code-sql[FILESTREAM#FS_DeleteData](../../relational-databases/blob/codesnippet/tsql/access-filestream-data-w_1_5.sql)]  
  
 Wenn Sie alle Daten aus der `Archive.dbo.Records`-Tabelle auswählen, ist die Zeile nicht mehr vorhanden, und Sie können die zugeordnete Datei nicht länger verwenden.  
  
> [!NOTE]  
>  Die zugrunde liegenden Dateien werden vom FILESTREAM Garbage Collector entfernt.  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Aktivieren und Konfigurieren von FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [Vermeiden von Konflikten mit Datenbankvorgängen in FILESTREAM-Anwendungen](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
