---
title: Bekannte Probleme in dieser Version des Treibers | Microsoft Docs
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
- known issues
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f4202004a556479779d4884fc42d04ae540ed56d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="known-issues-in-this-version-of-the-driver"></a>Bekannte Probleme in dieser Version des Treibers
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)] Dieses Thema enthält eine Liste der bekannten Probleme mit Microsoft ODBC Driver 13 for SQL Server unter Linux und MacOS.

Weitere Probleme werden auf dem [Microsoft ODBC Driver-Teamblog](http://blogs.msdn.com/b/sqlnativeclient/)gepostet.  

- Windows, Linux und MacOS Konvertieren von Zeichen aus dem Bereich (PUA) oder EUDC-Zeichen (EUDC) unterschiedlich. Konvertierungen ausgeführt werden, auf dem Server in [!INCLUDE[tsql](../../../includes/tsql_md.md)] verwenden Sie die Microsoft Konvertierungsbibliothek. Konvertierungen im Treiber verwenden, die Bibliotheken für Windows, Linux oder MacOS Konvertierung. Jede Bibliothek möglicherweise unterschiedlichen Ergebnissen führen, wenn diese Konvertierungen ausführen. Weitere Informationen finden Sie unter [EUDC-Zeichen und Zeichen des benutzerdefinierten Bereichs](http://msdn.microsoft.com/library/dd317802.aspx).

- Wenn der Client, die Codierung UTF-8 ist, wird der Treiber-Manager nicht immer ordnungsgemäß aus UTF-8 in UTF-16 konvertiert. Derzeit Daten beschädigt, wenn 1 oder mehr Zeichen in der Zeichenfolge sind keine gültigen UTF-8-Zeichen. ASCII-Zeichen werden korrekt zugeordnet. Der Treiber-Manager wird versuchen, diese Konvertierung beim Aufruf der SQLCHAR-Versionen der ODBC-API (zum Beispiel SQLDriverConnectA) durchzuführen. Der Treiber-Manager wird nicht versuchen, diese Konvertierung beim Aufruf der SQLWCHAR-Versionen der ODBC-API (zum Beispiel SQLDriverConnectW) durchzuführen.  

- Die *ColumnSize* Parameter **SQLBindParameter** bezieht sich auf die Anzahl der Zeichen in der SQL-Typ, während *Pufferlänge* ist die Anzahl der Bytes in der Anwendungsverzeichnis Puffer. Allerdings ist der SQL-Datentyp `varchar(n)` oder `char(n)`, die Anwendung bindet den Parameter als SQL_C_CHAR oder SQL_C_VARCHAR, und die zeichencodierung des Clients UTF-8 ist, erhalten Sie möglicherweise einen Fehler "Zeichenfolgendaten, rechts abgeschnitten" aus die Treiber, selbst wenn die Wert des *ColumnSize* an die Größe des Datentyps auf dem Server ausgerichtet ist. Dieser Fehler tritt auf, da die Konvertierungen zwischen zeichencodierungen, die Länge der Daten ändern können. Z. B. ein Apostroph rechten Zeichen (U + 2019) codiert ist, in CP-1252 als 0 x 92 wird das einzelne Byte, sondern in UTF-8 mit der 3-Byte-Sequenz 0xe2 0x80 0x99.

Angenommen, Ihre Codierung UTF-8 ist, und geben Sie 1 für beide *Pufferlänge* und *ColumnSize* in **SQLBindParameter** für eine Out-Parameter, und klicken Sie dann versuchen, Abrufen der oben genannten Zeichen gespeichert, die einer `char(1)` Spalte auf dem Server (mit CP-1252), der Treiber versucht, auf die 3 Bytes bestehende UTF-8-Codierung zu konvertieren, aber nicht das Ergebnis in einen 1-Byte-Puffer passt. In der anderen Richtung vergleicht *ColumnSize* mit der *Pufferlänge* in **SQLBindParameter** vor dem Ausführen der Konvertierung zwischen den verschiedenen Codepages auf die Client und Server. Da ein *ColumnSize* von 1 kleiner ist als eine *Pufferlänge* von (z. B.) 3, generiert der Treiber einen Fehler. Um diesen Fehler zu vermeiden, stellen Sie sicher, die die Länge der Daten nach der Konvertierung in den angegebenen Puffer oder die Spalte passt. Beachten Sie, dass *ColumnSize* darf nicht größer als 8000 für die `varchar(n)` Typ.

## <a name="see-also"></a>Siehe auch  
[Programmierrichtlinien](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[Versionsanmerkungen](../../../connect/odbc/linux-mac/release-notes.md)  


