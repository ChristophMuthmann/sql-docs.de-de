---
title: Treiber Versionsschema | Microsoft Docs
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
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dafb9631a3031c60646e4a7c396fadc440e12bb3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="driver-version-scheme"></a>Treiber Versionsschema
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Die folgende Tabelle enthält alle veröffentlichte Versionen von Microsoft ODBC Driver für Oracle.  
  
|Treiberversion|Buildnummer|Verfügbarkeitsverlauf|  
|--------------------|------------------|--------------------------|  
|1,0|2.00.6235|Visual C++ 4.2 und Visual Basic 5.0, Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 und MDAC 1,5 a|  
|2.0 aktualisiert|2.73.7283.01|IIS 4.0|  
|2.0 aktualisiert|2.73.7283.03|MDAC 1.5b und 1.5 c|  
|2.0 aktualisiert|2.73.7356|ODBC 3.5-SDK|  
|2.5|2.573.2927|Visual Studio 6.0 und MDAC 2.0|  
|2.5 aktualisiert|2.573.3513|SQLServer 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 Build 2.00.6235 (Version 1) wurde der ersten Version von Microsoft ODBC-Treiber für Oracle. Nach der Freigabe der ersten Version wurde eine neue Benennungskonvention übernommen.  
  
 Beispielsweise können die folgenden unterschiedlichen Komponenten 2.73.7283.03 geteilt werden:  
  
-   2 = die Versionsnummer.  
  
-   73 = die Version des Oracle-Server für die der Treiber entworfen wurde.  
  
-   7283.03 = die Buildnummer des Treibers.  
  
> [!NOTE]  
>  2.573.2973 Version, die Benennungskonvention hat zu einer gewissen Verwirrung 2.573 ist eine frühere Version als 2,73, dass jeder Abschnitt der Buildnummer angesehen wird, einzeln geführt. Die Anzahl 573 übersteigt 73, daher ist es eine neuere Version. Außerdem gibt "2.5" Versionsnummer des Treibers an.
