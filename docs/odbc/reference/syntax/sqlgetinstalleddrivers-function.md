---
title: SQLGetInstalledDrivers Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d2cd00f7306c7c9b6d60ff71d051b4709d7b3889
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0  
  
 **Zusammenfassung**  
 **SQLGetInstalledDrivers** liest den Abschnitt [ODBC Drivers], Informationen und eine Liste mit Beschreibungen der installierten Treiber zurückgibt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszBuf*  
 [Ausgabe] Liste der Beschreibungen der installierten Treiber. Informationen über die richtigen Listenstruktur finden Sie unter "Kommentare".  
  
 *cbBufMax*  
 [Eingabe] Länge des *LpszBuf*.  
  
 *pcbBufOut*  
 [Ausgabe] Gesamte Anzahl der Bytes, die (mit Ausnahme der Null-Terminierung Byte) im zurückgegebenen *LpszBuf*. Wenn die Anzahl der Bytes, die für die Rückgabe verfügbar, größer als oder gleich ist *CbBufMax*, die Liste der Treiber Beschreibungen in *LpszBuf* auf abgeschnitten *CbBufMax* minus der NULL-Abschlusszeichen. Die *PcbBufOut* -Argument ein null-Zeiger sein.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetInstalledDrivers** gibt "false", ein zugehöriges * \*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die * \*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Ungültige Pufferlänge.|Die *LpszBuf* Argument war NULL oder ungültig, oder die *CbBufMax* Argument war kleiner oder gleich 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Komponente wurde nicht in der Registrierung gefunden.|Das Installationsprogramm den Abschnitt [ODBC Drivers] wurde in der Registrierung nicht gefunden.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 Die Beschreibungen der Treiber wird durch ein Nullbyte beendet, und die gesamte Liste wird mit null Byte beendet. (D. h. kennzeichnen zwei null-Bytes am Ende der Liste.) Wenn Sie der zugeordnete Puffer nicht groß genug für die gesamte Liste ist, wird die Liste ohne Fehler abgeschnitten. Ein Fehler wird zurückgegeben, wenn ein null-Zeiger, als übergeben wird *LpszBuf*.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Zurückgeben von Beschreibungen der Treiber-Attribute|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
