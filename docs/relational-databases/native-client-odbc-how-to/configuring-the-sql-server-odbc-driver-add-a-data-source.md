---
title: "Hinzufügen einer Datenquelle (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 69b2056a8d9b51f6e75eb68a3323665fcc956a92
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Konfigurieren des SQL Server-ODBC-Treibers - Hinzufügen einer Datenquelle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Vor der Verwendung von ODBC-Anwendungen mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höher müssen Sie wissen, wie so aktualisieren Sie die Version der gespeicherten Prozeduren für Kataloginformationen in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und hinzufügen, löschen und Testen von Datenquellen.  
  
  Hinzufügen einer Datenquelle können Sie mithilfe des ODBC-Administrators, programmgesteuert (mit [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)), oder indem Sie eine Datei erstellen.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>So fügen Sie eine Datenquelle mit dem ODBC-Administrator hinzu  
  
1.  Aus der **Systemsteuerung**, Zugriff **Verwaltung** , und klicken Sie dann entweder **ODBC-Datenquellen (64-Bit)** oder **ODBC-Datenquellen (32-Bit)**. Alternativ können Sie odbcad32.exe aufrufen.  
  
2.  Klicken Sie auf die Registerkarte **Benutzer-DSN**, **System-DSN**oder **Datei-DSN** , und klicken Sie dann auf **Hinzufügen**.  
  
3.  Klicken Sie auf **SQL Server**und dann auf **Fertig stellen**.  
  
4.  Führen Sie die Schritte in der **erstellen Sie eine neue Datenquelle mit SQL Server** Assistenten.  
  
### <a name="to-add-a-data-source-programmatically"></a>So fügen Sie eine Datenquellen programmgesteuert hinzu  
  
1.  Rufen Sie [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) mit auf entweder ODBC_ADD_DSN oder ODBC_ADD_SYS_DSN festgelegtem zweiten Parameter.  
  
### <a name="to-add-a-file-data-source"></a>So fügen Sie eine Dateidatenquelle hinzu  
  
1.  Rufen Sie [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) mit einem SAVEFILE = File_name-Parameter in der Verbindungszeichenfolge. Wenn die Verbindung erfolgreich ist, erstellt der ODBC-Treiber eine Dateidatenquelle mit den Verbindungsparametern an dem Speicherort, auf den der SAVEFILE-Parameter zeigt.  
  
## <a name="see-also"></a>Siehe auch  
[Löschen einer Datenquelle &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
