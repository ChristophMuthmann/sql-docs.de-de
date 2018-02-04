---
title: Exportieren und importieren Sie eine Datenbank unter Linux | Microsoft Docs
description: 
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.custom: 
ms.workload: On Demand
ms.openlocfilehash: 6daf9f5293e30d5a42439920850b5abfe1ad83a0
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>Exportieren Sie und importieren Sie eine Datenbank unter Linux mit SSMS oder SqlPackage.exe unter Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Thema zeigt, wie [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) und [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) exportieren und importieren eine Datenbank auf SQL Server-2017 unter Linux. SSMS und SqlPackage.exe werden Windows-Anwendungen, verwenden daher diese Technik auf, wenn Sie einen Windows-Computer verfügen, der mit einer SQL Server-Remoteinstanz unter Linux eine Verbindung herstellen können.

Sie müssen immer installieren und verwenden Sie die neueste Version von SQL Server Management Studio (SSMS), wie in beschrieben [verwenden Sie SSMS unter Windows zur Verbindung mit SQL Server on Linux](sql-server-linux-develop-use-ssms.md)

> [!NOTE]
> Wenn Sie eine Datenbank von einer SQL Server-Instanz zu einem anderen migrieren, wird empfohlen, den verwenden [Sicherung und Wiederherstellung](sql-server-linux-migrate-restore-database.md).

## <a name="export-a-database-with-ssms"></a>Exportieren einer Datenbank mit SSMS

1. Starten Sie SSMS, geben Sie **Microsoft SQL Server Management Studio** in Windows-Suchfeld ein, und klicken Sie dann auf den desktop-app.

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png) 

2. Verbinden Sie mit der Quelldatenbank im Objekt-Explorer. Die Quelldatenbank kann in Microsoft SQL Server lokal oder in der Cloud unter Linux, Windows oder Docker und Azure SQL-Datenbank oder Azure SQL Data Warehouse sein.

3. Mit der rechten Maustaste im Objekt-Explorer der Quelldatenbank, zeigen Sie auf **Aufgaben**, und klicken Sie auf **Data-Tier-Anwendung exportieren...**

4. Klicken Sie im Exportassistenten auf **Weiter**, und klicken Sie dann auf die **Einstellungen** Registerkarte, konfigurieren Sie die exportieren, um die bacpac-Datei in entweder einen lokalen Speicherort oder in einem Azure-Blob gespeichert.

5. Standardmäßig werden alle Objekte in der Datenbank exportiert. Klicken Sie auf die **Registerkarte "Erweitert"** , und wählen Sie die Datenbankobjekte, die Sie exportieren möchten.

6. Klicken Sie auf **Weiter** und anschließend auf **Fertig stellen**.

Die *. Bacpac-Datei wurde erfolgreich erstellt, an der Position, die Sie ausgewählt haben, und Sie bereit sind, die sie in einer Zieldatenbank zu importieren.

## <a name="import-a-database-with-ssms"></a>Importieren Sie eine Datenbank mit SSMS

1. Starten Sie SSMS, geben Sie **Microsoft SQL Server Management Studio** in Windows-Suchfeld ein, und klicken Sie dann auf den desktop-app.

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png) 

2. Verbinden Sie mit dem Zielserver im Objekt-Explorer. Der Zielserver kann Microsoft SQL Server lokal oder in der Cloud unter Linux, Windows oder Docker und Azure SQL-Datenbank oder Azure SQL Data Warehouse.

3. Mit der rechten Maustaste die **Datenbanken** Ordner im Objekt-Explorer, und auf **Data-Tier-Anwendung importieren...**

4. Klicken Sie zum Erstellen der Datenbank auf Ihrem Zielserver, geben Sie eine bacpac-Datei aus dem lokalen Datenträger, oder wählen Sie das Azure-Speicherkonto und der Container, in dem Sie die bacpac-Datei hochgeladen.

5. Geben Sie den neuen Datenbanknamen für die Datenbank an. Wenn Sie eine Datenbank auf Azure SQL-Datenbank importieren, legen Sie die Edition von Microsoft Azure SQL-Datenbank (Dienstebene), maximale Datenbankgröße und Dienstziel (Leistungsebene).

6. Klicken Sie auf **Weiter** , und klicken Sie dann auf **Fertig stellen** die bacpac-Datei in eine neue Datenbank auf dem Zielserver zu importieren.

Die *. Bacpac-Datei wird importiert, um eine neue Datenbank auf dem Zielserver zu erstellen, die Sie angegeben haben.

## <a id="sqlpackage"></a>SqlPackage-Befehlszeilenoption

Es ist auch möglich, verwenden Sie das Befehlszeilentool von SQL Server Data Tools (SSDT) [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx), zum Exportieren und Importieren der bacpac-Dateien.

Der Befehl im folgenden Beispiel wird eine bacpac-Datei exportiert:

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

Verwenden Sie zum Importieren von Datenbank-Schema und die Benutzer Daten aus den folgenden Befehl ein. Bacpac-Datei:

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>Siehe auch
Weitere Informationen zum Verwenden von SSMS finden Sie unter [Verwenden von SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Weitere Informationen zu SqlPackage.exe, finden Sie unter der [SqlPackage-Referenzdokumentation](https://msdn.microsoft.com/library/hh550080.aspx).
