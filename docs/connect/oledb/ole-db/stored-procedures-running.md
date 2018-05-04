---
title: Ausführen von gespeicherten Prozeduren (OLE DB) | Microsoft Docs
description: Ausführen von gespeicherten Prozeduren (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 68f2298552a0dc6f313b54e357cecc2a6e7a855c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="stored-procedures---running"></a>-Ausgeführte, gespeicherte Prozeduren
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Wenn beim Ausführen von Anweisungen eine gespeicherte Prozedur in der Datenquelle ausgeführt wird (anstelle der Ausführung oder der Vorbereitung einer Anweisung direkt in der Clientanwendung), kann dies folgende Vorteile haben:  
  
-   Bessere Leistung  
  
-   Geringere netzwerkbelastung.  
  
-   Bessere Konsistenz  
  
-   Eine erhöhte Genauigkeit.  
  
-   Es wurden Funktionen hinzugefügt.  
  
 Der OLE DB-Treiber für SQL Server unterstützt drei der Mechanismen, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gespeicherte Prozeduren verwenden, um Daten zurückzugeben:  
  
-   Jede SELECT-Anweisung in der Prozedur generiert ein Resultset.  
  
-   Die Prozedur kann Daten über Ausgabeparameter zurückgeben.  
  
-   Die Prozedur kann einen ganzzahligen Rückgabecode besitzen.  
  
 Die Anwendung muss diese Ausgaben von gespeicherten Prozeduren verwenden können.  
  
 Die Rückgabe von Ausgabeparametern und Rückgabewerten erfolgt bei verschiedenen OLE DB-Anbietern zu unterschiedlichen Zeitpunkten während der Ergebnisverarbeitung. Im Falle der OLE DB-Treiber für SQL Server werden die Ausgabeparameter und Rückgabecodes nicht bis bereitgestellt, nachdem der Consumer abgerufen oder die von der gespeicherten Prozedur zurückgegebenen Resultsets abgebrochen hat. Die Rückgabecodes und die Ausgabeparameter werden im letzten TDS-Paket vom Server zurückgegeben.  
  
 Anbieter verwenden die DBPROP_OUTPUTPARAMETERAVAILABILITY-Eigenschaft, um die Rückgabe von Ausgabeparametern und Rückgabewerten zu melden. Bei dieser Eigenschaft handelt es sich um den DBPROPSET_DATASOURCEINFO-Eigenschaftensatz.  
  
 Der OLE DB-Treiber für SQL Server legt die DBPROP_OUTPUTPARAMETERAVAILABILITY-Eigenschaft auf dbpropval_oa_atrowrelease fest, um anzugeben, dass Rückgabecodes und Ausgabeparameter nicht zurückgegeben werden, bis das Resultset verarbeitet oder freigegeben wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren](../../oledb/ole-db/stored-procedures.md)  
  
  
