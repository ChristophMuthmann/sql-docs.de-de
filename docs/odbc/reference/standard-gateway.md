---
title: Standardgateway | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1e75f97ded8f999d5fa945e0aafb04322d51540
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="standard-gateway"></a>Standardgateway
Ein *Gateway* ist eine Softwarekomponente, die bewirkt, dass ein DBMS an, wie eine andere aussehen. D. h. das Gateway akzeptiert die Programmierschnittstelle, die SQL-Grammatik und Data stream-Protokoll von einem einzelnen DBMS und übersetzt sie in die Programmierschnittstelle, die SQL-Grammatik und Datenströme Protokoll des ausgeblendeten DBMS. Beispielsweise können Anwendungen mithilfe von Microsoft® SQL Server™ geschrieben auch DB2-Daten über das Gateway des Micro Decisionware DB2 zugreifen; Dieses Produkt wird DB2 Aussehen von SQL Server. Wenn Gateways verwendet werden, muss eine andere Gateway für jede Zieldatenbank geschrieben werden.  
  
 Gateways durch architektonische Unterschiede zwischen den DBMS eingeschränkt sind, sind jedoch ein guter Kandidat für die Standardisierung. Jedoch wenn allen DBMS sind, auf die Programmierschnittstelle zu standardisieren, SQL-Grammatik und Daten Protokolls stream von einer einzelnen DBMS, deren DBMS wird als Standard ausgewählt werden? Keine kommerziellen DBMS-Hersteller ist sicherlich wahrscheinlich zustimmen, um auf ein Produkt zu standardisieren. Und wenn ein standard-Programmierschnittstelle, die SQL-Grammatik und die Data Stream-Protokoll entwickelt werden, ist kein Gateway erforderlich.
