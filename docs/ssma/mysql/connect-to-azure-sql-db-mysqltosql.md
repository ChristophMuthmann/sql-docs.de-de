---
title: Herstellen einer Verbindung mit Azure SQL-Datenbank (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
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
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f3f0572426b6c90aa7b56c1f81e077f05f01caae
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Herstellen einer Verbindung mit Azure SQL-Datenbank (MySQLToSQL)
Stellen Sie mithilfe der SQL Azure-Dialogfeld Verbindung mit SQL Azure-Datenbank, die Sie migrieren möchten.  
  
Zum Zugriff auf dieses Dialogfeld, in dem **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit SQL Azure**. Wenn Sie zuvor eine Verbindung hergestellt haben, wird der Befehl ist **eine erneute Verbindung mit SQL Azure.**  
  
## <a name="options"></a>Tastatur  
**Servername**  
  
Wählen Sie aus, oder geben Sie den Servernamen zum Herstellen einer Verbindung mit SQL Azure.  
  
**Datenbank**  
  
Wählen Sie aus, geben Sie ein oder **Durchsuchen** den Datenbanknamen.  
  
> [!IMPORTANT]  
> SSMA für die MySQL unterstützt keine Verbindung mit der master-Datenbank in SQL Azure.  
  
**User name**  
  
Geben Sie den Benutzernamen, den SSMA für die Verbindung mit der SQL Azure-Datenbank verwenden  
  
**Kennwort**  
  
Geben Sie das Kennwort für den Benutzernamen ein.  
  
**Verschlüsseln**  
  
SSMA empfiehlt verschlüsselte Verbindung zu SQL Azure.  
  
## <a name="create-azure-database"></a>Azure-Datenbank erstellen  
Wenn keine Datenbanken im SQL Azure-Konto vorhanden sind, können Sie die erste Datenbank erstellen.  
  
Führen Sie die folgenden Schritte aus, um eine neue Datenbank zum ersten Mal erstellen,  
  
1.  Klicken Sie auf die Schaltfläche zum Durchsuchen, die in Verbindung zu SQL Azure (Dialogfeld) vorhanden ist  
  
2.  Wenn keine Datenbanken vorhanden sind, werden die folgenden zwei Menüelemente angezeigt.  
  
    1.  **(keine Datenbanken gefunden.)**  beträgt deaktiviert und abgeblendet ständig  
  
    2.  **Erstellen Sie neue Datenbank** die ist nur aktiviert, wenn keine Datenbanken auf SQL Azure-Konto vorhanden sind. Wenn Sie auf dieses Menüelement, ist Azure-Datenbank erstellen (Dialogfeld) mit Datenbanknamen und Größe vorhanden.  
  
3.  Zum Zeitpunkt der Erstellung der Datenbank werden die folgenden zwei Parameter als Eingabe angegeben:  
  
    1.  **Datenbankname:** Geben Sie den Datenbanknamen ein.  
  
    2.  **Datenbankgröße:** wählen Sie die Größe der Datenbank, die in SQL Azure-Konto erstellen müssen.  
  
