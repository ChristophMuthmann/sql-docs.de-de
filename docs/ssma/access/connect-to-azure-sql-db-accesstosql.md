---
title: Herstellen einer Verbindung mit Azure SQL-Datenbank (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 86a145cd23f40e41ef63b166e7536f91ee2129d9
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Herstellen einer Verbindung mit Azure SQL-Datenbank (AccessToSQL)
Stellen Sie mithilfe der SQL Azure-Dialogfeld Verbindung mit SQL Azure-Datenbank, die Sie migrieren möchten.  
  
Zum Zugriff auf dieses Dialogfeld, in dem **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit SQL Azure**. Wenn Sie zuvor eine Verbindung hergestellt haben, wird der Befehl ist **eine erneute Verbindung mit SQL Azure.**  
  
## <a name="options"></a>enthalten  
**Servername**  
  
Wählen Sie aus, oder geben Sie den Servernamen zum Herstellen einer Verbindung mit SQL Azure.  
  
**Datenbank**  
  
Wählen Sie aus, geben Sie ein oder **Durchsuchen** den Datenbanknamen.  
  
> [!IMPORTANT]  
> SSMA für Access unterstützt keine Verbindung mit der master-Datenbank in SQL Azure.  
  
**Benutzername**  
  
Geben Sie den Benutzernamen, den SSMA für die Verbindung mit der SQL Azure-Datenbank verwenden  
  
**Kennwort**  
  
Geben Sie das Kennwort für den Benutzernamen ein.  
  
**Verschlüsseln**  
  
SSMA empfiehlt verschlüsselte Verbindung zu SQL Azure.  
  
## <a name="create-azure-database"></a>Azure-Datenbank erstellen  
Führen Sie die folgenden Schritte aus, um einen neuen Azure-Datenbank zu erstellen,  
  
1.  Klicken Sie auf die Schaltfläche zum Durchsuchen, die in Verbindung zu SQL Azure (Dialogfeld) vorhanden ist  
  
2.  Wenn keine Datenbanken vorhanden sind, werden zwei Menüelemente angezeigt.  
  
    1.  **(keine Datenbanken gefunden.)**  beträgt deaktiviert und abgeblendet ständig  
  
    2.  **Erstellen Sie neue Datenbank** immer aktiviert, damit der Benutzer einen neue Azure-Datenbank auf SQL Azure-Konto zu erstellen. Wenn Sie auf dieses Menüelement, erstellen Sie im Dialogfeld Azure-Datenbank mit Datenbanknamen und Größe vorhanden ist.  
  
3.  Dieser Parameter wird zum Zeitpunkt der Erstellung der Datenbank als Eingabe angegeben.  
  
    1.  **Datenbankname:** Geben Sie den Datenbanknamen ein.  
  
    2.  **Datenbankgröße:** wählen Sie die Größe der Datenbank, die in SQL Azure-Konto erstellen müssen.  
  

