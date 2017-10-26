---
title: Datenquellen-Beispiel | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85eae404d4fa0ab739c699c8f120c76122c8ba67
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-example"></a>Beispiel für Datenquellen
Quellinformationen wird auf Computern unter Microsoft® Windows NT® Server-Windows 2000 Server, Microsoft Windows NT Workstation/Windows 2000 Professional oder Microsoft Windows® 95-und Windows 98, Computerdaten in der Registrierung gespeichert. Je nach der Registrierung Schlüssel die Informationen in einem gespeichert ist, wird die Datenquelle als bezeichnet eine *Benutzerdatenquelle* oder ein *Systemdatenquelle*. Benutzerdatenquellen sind unter dem Schlüssel HKEY_CURRENT_USER gespeichert und stehen nur für den aktuellen Benutzer. System-Datenquellen werden unter dem Schlüssel HKEY_LOCAL_MACHINE gespeichert und können von mehr als ein Benutzer auf einem Computer verwendet werden. Sie können von systemweiten-Diensten, die dann an die Datenquelle zugreifen können, auch wenn kein Benutzer mit dem Computer angemeldet ist, auch verwendet werden. Weitere Informationen zu Benutzer- und Systemdatenquellen finden Sie unter [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Angenommen, ein Benutzer drei Benutzerdatenquellen hat: Mitarbeiter und Hardwareinventur, die eine Oracle-DBMS; verwenden und Payroll verwendet eine Microsoft SQL Server-DBMS. Die Registrierungswerte für Datenquellen möglicherweise:  
  
```  
HKEY_CURRENT_USER  
SOFTWARE  
          ODBC  
               Odbc.ini  
                    ODBC Data Sources  
                    Personnel : REG_SZ : Oracle  
                    Inventory : REG_SZ : Oracle  
                    Payroll : REG_SZ : SQL Server  
```  
  
 und die Registrierungswerte für die Datenquelle Payroll möglicherweise:  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```

