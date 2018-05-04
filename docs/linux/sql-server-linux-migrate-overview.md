---
title: Migrieren von Datenbanken zu SQL Server on Linux | Microsoft Docs
description: Dieser Artikel beschreibt die verschiedenen Optionen zum Migrieren von Datenbanken und die Daten in SQL Server unter Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.technology: database-engine
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.custom: sql-linux
ms.openlocfilehash: ec4078497d38d2a9898cff0b3338cefd744a4dfc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Migrieren von Datenbanken und strukturierte Daten zu SQL Server on Linux 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Sie können Ihre Datenbanken und die Daten zu SQL Server-2017 auf Linux laufende migrieren. Der Methode Ihrer Wahl verwenden, hängt von den Quelldaten und Ihr konkretes Szenario ab. Die folgenden Abschnitte enthalten bewährte Methoden für verschiedene Szenarien mit Migration.

## <a name="migrate-from-sql-server-on-windows"></a>Migrieren von SQLServer unter Windows
Wenn Sie SQL Server-Datenbanken unter Windows zu SQL Server-2017 unter Linux migrieren möchten, ist das empfohlene Verfahren zum Verwenden von SQL Server-Sicherung und Wiederherstellung.

1. Erstellen Sie eine Sicherung der Datenbank auf dem Windows-Computer.
2. Übertragen Sie die Sicherungsdatei an dem Ziel-SQL Server-Linux-Computer.
3. Stellen Sie die Sicherung auf dem Linux-Computer wieder her. 

Ein Lernprogramm zum Migrieren einer Datenbank durch Sichern und Wiederherstellen finden Sie im folgenden Thema:

- [Wiederherstellen eine SQL Server-Datenbank von Windows, Linux](sql-server-linux-migrate-restore-database.md).

Es ist auch möglich, exportieren Ihre Datenbank in eine bacpac-Datei (eine komprimierte Datei, die die Datenbankschema und Daten enthält). Wenn Sie eine bacpac-Datei verfügen, können Sie diese Datei auf den Linux-Computer übertragen und dann in SQL Server importieren. Weitere Informationen finden Sie in folgenden Themen:

- [Exportieren Sie und importieren Sie eine Datenbank mit SSMS oder SqlPackage.exe](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>Migrieren von anderen Datenbankserver
Sie können Datenbanken auf anderen Datenbanksystemen zu SQL Server-2017 unter Linux migrieren. Dies schließt Microsoft Access, DB2, MySQL, Oracle und Sybase-Datenbanken. Verwenden Sie in diesem Szenario die SQL Server Management Assistant (SSMA), um die Migration zu SQL Server on Linux zu automatisieren. Weitere Informationen finden Sie unter [verwenden SSMA zum Migrieren von Datenbanken zu SQL Server on Linux](sql-server-linux-migrate-ssma.md).  

## <a name="migrate-structured-data"></a>Migrieren Sie strukturierte Daten
Es gibt auch Verfahren zum Importieren von Rohdaten. Sie können Datendateien strukturiert haben, die von anderen Datenbanken oder Datenquellen exportiert wurden. In diesem Fall können Sie das Tool Bcp, Bulk Insert die Daten. Oder Sie können SQL Server Integration Services unter Windows zum Importieren der Daten in eine SQL Server-Datenbank unter Linux ausführen. SQL Server Integration Services können Sie komplexere Transformationen auf die Daten während des Imports ausführen. 

Weitere Informationen zu diesen Verfahren finden Sie unter den folgenden Themen:

- [Massenkopieren von Daten mithilfe von bcp](sql-server-linux-migrate-bcp.md)
- [Extrahieren, Transformieren und Laden von Daten für SQL Server on Linux mit SSIS](sql-server-linux-migrate-ssis.md) 
