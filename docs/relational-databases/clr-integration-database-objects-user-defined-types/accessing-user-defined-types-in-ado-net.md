---
title: Zugreifen auf benutzerdefinierte Typen in ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
caps.latest.revision: 12
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7747896143f8ecb4d13c17d1f0ff36773b7583a9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="accessing-user-defined-types-in-adonet"></a>Zugreifen auf benutzerdefinierte Typen in ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Benutzerdefinierte Typen (UDTs) werden in einer beliebigen der vom unterstützten Sprachen die [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework common Language Runtime (CLR, die überprüfbaren Code generiert). Dazu gehören [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# und [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. UDTs ermöglichen das Speichern von Objekten und benutzerdefinierten Datenstrukturen in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank. Die Daten werden als öffentliche Elemente einer .NET Framework-Klasse oder -Struktur verfügbar gemacht. Das Verhalten wird durch die Methoden der Klasse oder Struktur definiert. Ein UDT als Spaltendefinition einer Tabelle, als Variable in verwendet werden kann eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch oder als Argument einer [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktion oder gespeicherten Prozedur.  
  
 In ADO.NET können die **System.Data.SqlClient** Anbieter macht UDTs auf folgende Weise:  
  
-   Über die **System.Data.SqlClient.SqlDataReader** als ein Objekt.  
  
-   Über die **SqlDataReader** als unformatierte Bytes.  
  
-   Als Parameter für eine **System.Data.SqlClient.SqlParameter** Objekt.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Abrufen von UDT-Daten](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 Beschreibt, wie UDT-Daten abgerufen und Parameter angegeben werden.  
  
 [Aktualisieren von UDT-Spalten mit "DataAdapters"](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Beschreibt das Arbeiten mit UDTs in **DataSets** und zum Aktualisieren von UDT-Daten mit **"DataAdapters"**.  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
