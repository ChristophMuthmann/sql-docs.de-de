---
title: SQLServerPreparedStatement-Klasse | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2494ebfffa6066988bdd979a55cf40d8cd68347e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverpreparedstatement-class"></a>SQLServerPreparedStatement-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt die grundlegende Implementierung der JDBC-Funktion für vorbereitete Anweisungen dar.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Erweitert:** SQLServerStatement  
  
 **Implementiert:** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Hinweise  
 Sqlserverpreparedstatement-Klasse enthält Methoden, mit die Sie Parameter als beliebige Java-Typen und viele Java-Objekttypen bereitstellen können. SQLServerPreparedStatement bereitet eine Anweisung vor, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **Sp_prepare** gespeicherte Prozedur, und klicken Sie dann verwendet das zurückgegebene Anweisungshandle zum jede nachfolgende Ausführen der Anweisung, in der Regel mit anderen vom Benutzer bereitgestellte Parameter.  
  
 SQLServerPreparedStatement unterstützt Batchverarbeitung, wobei eine Reihe von vorbereiteten Anweisungen sind in einer einzelnen Datenbank Roundtrip ausgeführt, um die laufzeitleistung zu verbessern.  
  
 Diese Klasse unterstützt das Entpacken in die SQLServerPreparedStatement-Klasse, ISQLServerPreparedStatement-Schnittstelle, java.sql.PreparedStatement-Schnittstelle, und die Klassen und Schnittstellen, die vom SQLServerStatement für das Entpacken unterstützt werden. Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
