---
title: SQLXML ist in SQLServer nicht installiert. | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4dcf2cf4de62b4f63d37bf7bfd74def6b98cd2f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML ist in SQL Server nicht installiert
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Vor der Veröffentlichung von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wurde SQLXML 4.0 mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] veröffentlicht und war Bestandteil der Standardinstallation aller [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Versionen außer [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ist die neueste Version von SQLXML (SQLXML 4.0 SP1) nicht mehr in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthalten. Zum Installieren von SQLXML 4.0 SP1 Laden Sie es [Install Location for SQLXML 4.0 SP1](https://www.microsoft.com/en-us/download/details.aspx?id=30403).  
  
 Wenn eine Anwendung ausgeführt wird, auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und SQLXML 4.0 erfordert müssen Sie SQLXML 4.0 SP1 herunterladen und installieren.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Verhalten von SQLXML 4.0 SP1 mit neuen Datentypen, die SQLOLEDB und SQL Server Native Client-OLE DB-Anbieter verwenden  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] die folgenden Datentypen, die die Verwendung von SQLXML Entwickler ggf. nutzen möchte, eingeführt:  
  
-   **Datum**  
  
-   **Zeit**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 Bei Verwendung von SQLXML 4.0 SP1 mit SQLOLEDB oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB aus [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], diese Typen als Zeichenfolgen ein Entwickler angezeigt. SQLXML 4.0 SP1 aktiviert diese vier neuen Datentypen als integrierte skalare Typen, die bei Verwendung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter 11.0 oder höher. Wenn Sie SQLXML 4.0 SP1 noch nicht heruntergeladen haben, kann die Zuordnung dieser Typen zu anderen als Zeichenfolgentypen zum Abschneiden einiger Daten führen. Z. B. das zuordnen **DateTime2** auf **xsd: Date** zum Abschneiden von Daten führt dazu, dass die [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **"DateTime"** Genauigkeit von 3,33 Millisekunden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLXML 4.0-Programmierkonzepte](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
