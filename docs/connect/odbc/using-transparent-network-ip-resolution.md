---
title: "Transparentes Netzwerk-IP-Auflösung mit | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cc3b7595b836544f3f7bcfd94f2bab83fac24b36
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-transparent-network-ip-resolution"></a>Mithilfe des transparenten Netzwerk-IP-Auflösung
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution ist eine Version der vorhandenen MultiSubnetFailover-Funktion, die in Microsoft ODBC Driver 13.1 für SQL Server, die die Verbindungssequenz des Treibers in die Groß-/Kleinschreibung auswirkt, in dem die erste aufgelöste IP-Adresse des Hostnamens nicht, verfügbar reagieren, und es sind mehrere IP-Adressen, die den Hostnamen zugeordnet. Er interagiert mit MultiSubnetFailover, um die folgenden drei Verbindung Sequenzen bereitzustellen:

* 0: eine IP versucht wird, gefolgt von allen IP-Adressen parallel
* 1: alle IP-Adressen werden parallel versucht
* 2: angestrebt, alle IP-Adressen nach dem anderen

|TransparentNetworkIPResolution|MultiSubnetFailover|Verhalten|
|:-:|:-:|:-:|
|(Standard)|(Standard)|0|
|(Standard)|Aktiviert|1|
|(Standard)|Disabled|0|
|Aktiviert|(Standard)|0|
|Aktiviert|Aktiviert|1|
|Aktiviert|Disabled|0|
|Disabled|(Standard)|2|
|Disabled|Aktiviert|1|
|Disabled|Disabled|2|

Die `TransparentNetworkIPResolution` Verbindungszeichenfolge und dem DSN-Schlüsselwort steuert diese Einstellung auf der Ebene der Verbindungszeichenfolge. Die Standardeinstellung ist aktiviert.

Schlüsselwort|Werte|Standardwert
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

Die `SQL_COPT_SS_TNIR` vorverbindungsattribut ermöglicht einer Anwendung, um diese Einstellung programmgesteuert zu steuern:

-Verbindungsattribut|   Größe/Type|  Standardwert| Wert| Description
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER`oder`SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Aktiviert oder deaktiviert TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>Weitere Informationen zu MultiSubnetFailover, finden Sie unter [ODBC-Treiber unter Linux und Mac OS - hohe Verfügbarkeit und Wiederherstellung im Notfall](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>Siehe auch  
* [Microsoft ODBC Driver for SQL Server unter Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server-Multisubnetzclustering (SQLServer)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)

