---
title: "Bildlauffähige Cursor und Transaktionsisolation | Microsoft Docs"
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
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6c9e38f4287a8832d8e794940093ce696ac0eaf7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>Bildlauffähige Cursor und Transaktionsisolation
Die folgende Tabelle enthält die Faktoren, die für die Sichtbarkeit der Änderungen.  
  
|Änderungen durch:|Sichtbarkeit abhängig:|  
|----------------------|----------------------------|  
|Cursor|Cursortyp, Cursor-Implementierung|  
|Andere Anweisungen in derselben Transaktion|Cursortyp|  
|Anweisungen in anderen Transaktionen|Cursortyp, die Isolationsstufe für Transaktionen|  
  
 Diese Faktoren werden in der folgenden Abbildung gezeigt.  
  
 ![Faktoren, die für die Sichtbarkeit der Änderungen](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 In der folgenden Tabelle sind die Fähigkeit der einzelnen Cursor allein durch andere Vorgänge in einer eigenen Transaktion und von anderen Transaktionen vorgenommenen Änderungen erkennen zusammengefasst. Die Sichtbarkeit der letzteren Änderungen hängt davon ab, der Cursor-Datentyp und die Isolationsstufe der Transaktion, die den Cursor enthält.  
  
|Cursor type\action|Self-Service|Besitzer<br /><br /> Überschreitungstransaktion|Adresszuweisungen<br /><br /> Überschreitungstransaktion<br /><br /> (RU[a])|Adresszuweisungen<br /><br /> Überschreitungstransaktion<br /><br /> (RC[a])|Adresszuweisungen<br /><br /> Überschreitungstransaktion<br /><br /> (RR[a])|Adresszuweisungen<br /><br /> Überschreitungstransaktion<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|STATIC-Cursor|||||||  
|Insert|Vielleicht [b]|nein|nein|nein|nein|nein|  
|Update|Vielleicht [b]|nein|nein|nein|nein|nein|  
|DELETE|Vielleicht [b]|nein|nein|nein|nein|nein|  
|Keysetgesteuerte|||||||  
|Insert|Vielleicht [b]|nein|nein|nein|nein|nein|  
|Update|ja|ja|ja|ja|nein|nein|  
|DELETE|Vielleicht [b]|ja|ja|ja|nein|nein|  
|Dynamic|||||||  
|Insert|ja|ja|ja|ja|ja|nein|  
|Update|ja|ja|ja|ja|nein|nein|  
|DELETE|ja|ja|ja|ja|nein|nein|  
  
 [a] der Buchstaben in Klammern geben die Isolationsstufe der Transaktion mit dem Cursor; die Isolationsstufe der anderen Transaktion (in dem die Änderung vorgenommen wurde) ist nicht relevant.  
  
 RU: Read uncommitted  
  
 RC: Read committed  
  
 RR: Repeatable read  
  
 Serialisierbare S:  
  
 [b] hängt wie der Cursor implementiert wird. Gibt an, ob der Cursor für solche Änderungen erkennen, kann über die SQL_STATIC_SENSITIVITY-Option in gemeldete ist **SQLGetInfo**.
