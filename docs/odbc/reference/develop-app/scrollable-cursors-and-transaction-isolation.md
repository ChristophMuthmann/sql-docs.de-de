---
title: Bildlauffähige Cursor und Transaktionsisolation | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbbcdf0c9ce2c7e37072502ae49b43dc20d15a9e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
|Insert|Vielleicht [b]|nein|Nein|Nein|Nein|nein|  
|Update|Vielleicht [b]|nein|Nein|Nein|Nein|nein|  
|Delete|Vielleicht [b]|nein|Nein|Nein|Nein|nein|  
|Keysetgesteuerte|||||||  
|Insert|Vielleicht [b]|nein|Nein|Nein|Nein|nein|  
|Update|ja|ja|ja|ja|Nein|nein|  
|Delete|Vielleicht [b]|ja|ja|ja|Nein|nein|  
|Dynamic|||||||  
|Insert|ja|ja|ja|ja|ja|nein|  
|Update|ja|ja|ja|ja|Nein|nein|  
|Delete|ja|ja|ja|ja|Nein|nein|  
  
 [a] der Buchstaben in Klammern geben die Isolationsstufe der Transaktion mit dem Cursor; die Isolationsstufe der anderen Transaktion (in dem die Änderung vorgenommen wurde) ist nicht relevant.  
  
 RU: Read uncommitted  
  
 RC: Read committed  
  
 RR: Repeatable read  
  
 Serialisierbare S:  
  
 [b] hängt wie der Cursor implementiert wird. Gibt an, ob der Cursor für solche Änderungen erkennen, kann über die SQL_STATIC_SENSITIVITY-Option in gemeldete ist **SQLGetInfo**.
