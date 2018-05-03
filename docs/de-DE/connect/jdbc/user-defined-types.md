---
title: Benutzerdefinierte Typen | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3873e2d05eab1fb7ce0ec26db73a78ce1c39b28e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="user-defined-types"></a>Benutzerdefinierte Typen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Benutzerdefinierte Typen (UDTs) wurden in eingeführt [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] , Ihnen können Entwickler das skalartypsystem des Servers erweitern, indem Sie das Speichern von common Language Runtime (CLR)-Objekte in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. UDTs können mehrere Elemente enthalten und Verhalten aufweisen, die im Gegensatz zu den herkömmlichen Aliasdatentypen, die aus einer einzelnen bestehen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Systemdatentyp. Vorher waren UDTs auf eine Dateigröße von maximal 8 Kilobyte beschränkt. In [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)], Unterstützung für UDTs über 64 Kilobyte hinzugefügt wurde. Ab Version 3.0 unterstützt JDBC Driver beim Festlegen des UserDefined-Formats auch UDTs, die größer als 64 KB sind.  
  
 UDTs mit genau oder weniger als 8.000 Byte verhalten sich also genau wie bisher. Größere UDTs werden aber unterstützt und zeigen ihre Größe als "unbegrenzt" an.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
