---
title: Jet ODBC-Fehlermeldungen | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b62b26425c1e9126ea5d6ad5a3a4c3d944a5b79a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-jet-error-messages"></a>Jet ODBC-Fehlermeldungen
Für Fehler, die in der Datenquelle auftreten, gibt der ODBC-Treiber eine Fehlermeldung zurückgegeben, von der ODBC-Datei-Bibliothek zurück. Für Fehler, die in der ODBC-Treiber oder der Treiber-Manager auftreten, zugeordnet ist der Treiber gibt eine Fehlermeldung den Text anhand der SQLSTATE.  
  
 Fehlermeldungen haben das folgende Format:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 Die Präfixe in Klammern ([]) identifizieren Sie den Speicherort des Fehlers. Tritt der Fehler im Treiber-Manager, *Datenquelle* nicht angegeben wird. Tritt der Fehler in der Datenquelle, die [*Hersteller*] und [*ODBC-Komponente*] Präfixe zu identifizieren, den Hersteller und den Namen der ODBC-Komponente, die den Fehler aus der Datenquelle.  
  
 Die folgende Tabelle zeigt die vom Treiber-Manager und ISAM-Treiber zurückgegebenen Fehlermeldungen:  
  
|Fehlermeldung|Fehler-Speicherort|  
|-------------------|--------------------|  
|[Microsoft] [ODBC-Treiber-Manager] *Meldungstext*|Treiber-Managers (Odbc32.dll)|  
|[Microsoft] [ODBC *Treibername*]*Meldungstext*|ISAM-Treiber (Siehe ISAMs-Treiber)|
