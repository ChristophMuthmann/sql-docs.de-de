---
title: Herstellen einer Verbindung mit der Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: fe9cf1f66a181f252e644a6e610eb102776dc27d
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-sybase-sybasetosql"></a>Herstellen einer Verbindung mit der Sybase (SybaseToSQL)
Verwenden der **Herstellen einer Verbindung mit der Sybase** Dialogfeld Verbindung mit der Sybase Adaptive Server Enterprise (ASE)-Instanz, die Sie migrieren möchten.  
  
Zum Zugriff auf dieses Dialogfeld, in dem **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit der Sybase**. Wenn Sie zuvor eine Verbindung hergestellt haben, wird der Befehl ist **eine erneute Verbindung zu Sybase**.  
  
## <a name="options"></a>enthalten  
**Provider**  
Wählen Sie einen der installierten Anbieter auf dem Computer für die Verbindung mit der Sybase-Server.  
  
**Mode**  
Wählen Sie entweder standard oder erweiterte Verbindungsmodus. Im Modus "standard" Geben Sie ein oder wählen Sie Werte für den Servernamen, Port, Benutzername und Kennwort. Im erweiterten Modus geben Sie eine Verbindungszeichenfolge an.  
  
**Servername**  
Geben Sie an, oder wählen Sie den Namen oder IP-Adresse des Adaptive Server. Der Standardservername entspricht dem Namen des Computers. Dies ist ein Modus "standard"-Option.  
  
**Serverport**  
Wenn Sie einen nicht standardmäßigen Port für Verbindungen mit ASE verwenden, geben Sie die Portnummer. Die Standardportnummer ist 5000. Dies ist ein Modus "standard"-Option.  
  
**Benutzername**  
Geben Sie den Benutzernamen ein, der zum Herstellen einer ASE verwendet wird. Dies ist ein Modus "standard"-Option.  
  
**Kennwort**  
Geben Sie das Kennwort für den Benutzernamen ein. Dies ist ein Modus "standard"-Option.  
  
**Verbindungszeichenfolge**  
Geben Sie die vollständige Verbindungszeichenfolge für die Verbindung zum ASE.  
  
Verbindungszeichenfolgen werden von Name-Wert-Paaren bestehen. Die Namen der Parameter hängt von den verwendeten Anbieter.  
  
**Verbindungsparameter für die verschiedenen Anbietern sind wie folgt aus:**  
  
1.  Verbindungsparameter für **OLE DB-Anbieter**  
  
    |Einstellung|Sybase 12,5-Parameter|Sybase 15-Parameter|  
    |-----------|-------------------------|-----------------------|  
    |Servername|Servername|Server|  
    |Port|Serverport-Adresse|Port|  
    |Benutzername|Benutzer-ID|Benutzer-ID|  
    |Kennwort|Kennwort|Kennwort|  
    |Anbieter|Anbieter|Anbieter|  
  
    Für Sybase ASE 12,5 sehen eine Beispielverbindungszeichenfolge wie folgt:  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    Für Sybase ASE 15 sehen eine Beispielverbindungszeichenfolge wie folgt:  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  Verbindungsparameter für **ODBC-Anbieter**  
  
    |Einstellung|Sybase 12,5/15-Parameter|  
    |-----------|-----------------------------|  
    |Treibername|Treiber|  
    |Servername|Server|  
    |Benutzername|UID|  
    |Kennwort|PWD|  
    |Portnummer|Port|  
  
    Für Sybase ASE 12,5 oder 15 weist eine Beispielverbindungszeichenfolge Folgendes:  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  Verbindungsparameter für **ADO.NET-Anbieter**  
  
    |Einstellung|Sybase 12,5/15-Parameter|  
    |-----------|-----------------------------|  
    |Servername|Server|  
    |Benutzername|UID|  
    |Kennwort|PWD|  
    |Portnummer|Port|  
  
    Ein Beispiel für die Verbindungszeichenfolge für den ADO.NET-Anbieter ist wie folgt:  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
Weitere Informationen finden Sie unter der ASE-Dokumentation.  
  
Dies ist eine Option im erweiterten Modus.  
  

