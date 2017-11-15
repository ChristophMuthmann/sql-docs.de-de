---
title: Erstellen einer Tabelle zum Speichern von FILESTREAM-Daten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FILESTREAM [SQL Server], table storage
ms.assetid: 029c3059-5c83-43e2-a859-9027031b7de1
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 60dc386ed2635812a0abcc50801696611e9a2084
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-table-for-storing-filestream-data"></a>Erstellen einer Tabelle zum Speichern von FILESTREAM-Daten
  In diesem Thema wird erläutert, wie Sie eine Tabelle zum Speichern von FILESTREAM-Daten erstellen.  
  
 Wenn die Datenbank eine FILESTREAM-Dateigruppe aufweist, können Sie Tabellen zum Speichern von FILESTREAM-Daten erstellen oder ändern. Erstellen Sie eine **varbinary(max)** -Spalte und fügen das FILESTREAM-Attribut hinzu, um anzugeben, dass eine Spalte FILESTREAM-Daten enthält.  
  
### <a name="to-create-a-table-to-store-filestream-data"></a>So erstellen Sie eine Tabelle zum Speichern von FILESTREAM-Daten  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]auf **Neue Abfrage** , um den Abfrage-Editor zu öffnen.  
  
2.  Kopieren Sie den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code aus dem folgenden Beispiel in den Abfrage-Editor. Dieser [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code erstellt eine FILESTREAM-aktivierte Tabelle mit dem Namen Records.  
  
3.  Klicken Sie auf **Ausführen**, um die Tabelle zu erstellen.  
  
## <a name="example"></a>Beispiel  
 Das folgende Codebeispiel zeigt, wie eine Tabelle mit der Bezeichnung `Records`erstellt wird. Die `Id` -Spalte ist eine `ROWGUIDCOL` -Spalte, die zur Verwendung von FILESTREAM-Daten mit Win32-APIs erforderlich ist. Die `SerialNumber` -Spalte ist eine `UNIQUE INTEGER`-Spalte. Die `Chart` -Spalte ist eine `FILESTREAM` -Spalte, die verwendet wird, um `Chart` im Dateisystem zu speichern.  
  
> [!NOTE]  
>  Dieses Beispiel bezieht sich auf die Datenbank „Archive“, die unter [Vorgehensweise: Erstellen einer FILESTREAM-aktivierten Datenbank](../../relational-databases/blob/create-a-filestream-enabled-database.md)erstellt wird.  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../relational-databases/blob/codesnippet/tsql/create-a-table-for-stori_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
