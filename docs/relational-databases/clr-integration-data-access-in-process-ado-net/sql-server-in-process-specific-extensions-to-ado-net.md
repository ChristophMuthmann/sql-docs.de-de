---
title: SQL Server In-Process-spezifische Erweiterungen für ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [CLR integration]
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], in-process extensions
- in-process data access providers [CLR integration]
- extensions [CLR integration]
ms.assetid: 781b812e-eb14-472a-85fa-aa4cdb929bee
caps.latest.revision: 33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4d26ee079f507db9aebbf613e401726dbca2872b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-in-process-specific-extensions-to-adonet"></a>Von SQL Server verwendete prozessinterne spezifische Erweiterungen für ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Es gibt vier Hauptfunktionserweiterungen für ADO.NET, die speziell der prozessinternen Verwendung dienen. Die folgenden Themen liefern detaillierte Informationen zu diesen Erweiterungen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [SqlContext-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
 Diese Klasse bietet Zugriff auf die anderen Erweiterungen, indem sie den Kontext des Aufrufers einer SQL Server-Routine abstrahiert, die verwalteten Code prozessintern ausführt.  
  
 [SqlPipe-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)  
 Diese Klasse enthält Routinen, mit denen Tabellenergebnisse und Nachrichten an den Client gesendet werden.  
  
 [SqlTriggerContext-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)  
 Diese Klasse stellt Informationen über den Kontext bereit, in dem ein Trigger ausgeführt wird.  
  
 [SqlDataRecord-Objekt](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)  
 Die SqlDataRecord-Klasse stellt eine einzelne Datenzeile einschließlich der zugehörigen Metadaten dar und ermöglicht es gespeicherten Prozeduren, benutzerdefinierte Resultsets an den Client zurückzugeben.  
  
  
