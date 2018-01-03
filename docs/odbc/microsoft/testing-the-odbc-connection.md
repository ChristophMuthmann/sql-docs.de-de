---
title: Testen der ODBC-Verbindung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cffb08b48128500b37c6f55e37a848be19c266a8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="testing-the-odbc-connection"></a>Testen der ODBC-Verbindung
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Bei der Problembehandlung der ODBC-Zugriff auf Oracle 7.x und 8 RDBMS-Server, ist es möglicherweise erforderlich, um zu überprüfen, ob die zugrunde liegende SQL * Net und Adapter für Oracle-Protokoll ordnungsgemäß installiert. Zu diesem Zweck verwenden Sie das Hilfsprogramm Oracle bereitgestellte Nettest.exe im Verzeichnis Orawin\Bin.  
  
 Nettest ist ein einfaches Utility, die versucht, melden Sie sich an den ausgewählten Server mit nur der installierten SQL * Net-Software, die Teil der Oracle-Client ist. Das Dienstprogramm fordert einen Anmeldenamen, verbinden Sie das Kennwort und TNS Zeichenfolge. Wenn der Oracle-Client ordnungsgemäß installiert ist, zeigt das Hilfsprogramm einfach "Ping erfolgreich." Wenn die Anmeldung nicht erfolgreich war, müssen Sie ein Datenbankadministrator konsultieren.
