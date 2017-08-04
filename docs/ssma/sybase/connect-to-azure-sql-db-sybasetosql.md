---
title: Herstellen einer Verbindung mit Azure SQL-Datenbank (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 76a29a448dfbbba4b8fc0771edf352545d361cf9
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>Herstellen einer Verbindung mit Azure SQL-Datenbank (SybaseToSQL)
Stellen Sie mithilfe der Azure SQL-Datenbank (Dialogfeld), mit der Azure SQL-Datenbank-Datenbank herstellen, die Sie migrieren möchten.  
  
Zum Zugriff auf dieses Dialogfeld, in dem **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit Azure SQL-Datenbank**. Wenn Sie zuvor eine Verbindung hergestellt haben, wird der Befehl ist **eine erneute Verbindung mit der Azure SQL-Datenbank.**  
  
## <a name="options"></a>enthalten  
**Servername**  
  
Wählen Sie aus, oder geben Sie den Servernamen für die Verbindung mit Azure SQL-Datenbank.  
  
**Datenbank**  
  
Wählen Sie aus, geben Sie ein oder **Durchsuchen** den Datenbanknamen.  
  
> [!IMPORTANT]  
> SSMA für Sybase unterstützt keine Verbindung mit der master-Datenbank in Azure SQL-Datenbank.  
  
**Benutzername**  
  
Geben Sie den Benutzernamen, den SSMA für die Verbindung mit der Azure SQL-Datenbank-Datenbank verwenden  
  
**Kennwort**  
  
Geben Sie das Kennwort für den Benutzernamen ein.  
  
**Verschlüsseln**  
  
SSMA empfiehlt verschlüsselte Verbindung mit der Azure SQL-Datenbank.  
  
## <a name="create-azure-database"></a>Azure-Datenbank erstellen  
Wenn keine Datenbanken im Konto Azure SQL-Datenbank vorhanden sind, können Sie die erste Datenbank erstellen.  
  
Führen Sie die folgenden Schritte aus, um eine neue Datenbank zum ersten Mal erstellen,  
  
1.  Klicken Sie auf die Schaltfläche zum Durchsuchen, die in Verbindung zu Azure SQL-Datenbank (Dialogfeld) vorhanden ist  
  
2.  Wenn keine Datenbanken vorhanden sind, werden die folgenden zwei Menüelemente angezeigt.  
  
    1.  **(keine Datenbanken gefunden.)**  beträgt deaktiviert und abgeblendet ständig  
  
    2.  **Erstellen Sie neue Datenbank** die ist nur aktiviert, wenn keine Datenbanken auf Azure SQL-Datenbank-Konto vorhanden sind. Wenn Sie auf dieses Menüelement, ist Azure-Datenbank erstellen (Dialogfeld) mit Datenbanknamen und Größe vorhanden.  
  
3.  Zum Zeitpunkt der Erstellung der Datenbank werden die folgenden zwei Parameter als Eingabe angegeben:  
  
    1.  **Datenbankname:** Geben Sie den Datenbanknamen ein.  
  
    2.  **Datenbankgröße:** wählen Sie die Größe der Datenbank, die Sie in Azure SQL-Datenbank-Konto erstellen müssen.  
  

