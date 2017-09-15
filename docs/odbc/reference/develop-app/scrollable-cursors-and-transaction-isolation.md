---
title: "Bildlauffähige Cursor und Transaktionsisolation | Microsoft Docs"
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
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 192962491095f8c6b8fb212ab7789cb74b609897
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
|Insert|Vielleicht [b]|Nein|Nein|Nein|Nein|Nein|  
|Update|Vielleicht [b]|Nein|Nein|Nein|Nein|Nein|  
|DELETE|Vielleicht [b]|Nein|Nein|Nein|Nein|Nein|  
|Keysetgesteuerte|||||||  
|Insert|Vielleicht [b]|Nein|Nein|Nein|Nein|Nein|  
|Update|ja|ja|ja|ja|Nein|Nein|  
|DELETE|Vielleicht [b]|ja|ja|ja|Nein|Nein|  
|Dynamic|||||||  
|Insert|ja|ja|ja|ja|ja|Nein|  
|Update|ja|ja|ja|ja|Nein|Nein|  
|DELETE|ja|ja|ja|ja|Nein|Nein|  
  
 [a] der Buchstaben in Klammern geben die Isolationsstufe der Transaktion mit dem Cursor; die Isolationsstufe der anderen Transaktion (in dem die Änderung vorgenommen wurde) ist nicht relevant.  
  
 RU: Read uncommitted  
  
 RC: Read committed  
  
 RR: Repeatable read  
  
 Serialisierbare S:  
  
 [b] hängt wie der Cursor implementiert wird. Gibt an, ob der Cursor für solche Änderungen erkennen, kann über die SQL_STATIC_SENSITIVITY-Option in gemeldete ist **SQLGetInfo**.
