---
title: Synchronize21-Methode (RDS) | Microsoft Docs
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize21 method [ADO]
ms.assetid: 6b35f136-9d9a-4bdd-8144-67decfd3c4e9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5ef3b68f46b81ae754a13f42047eda8d27ac32f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="synchronize21-method-rds"></a>Synchronize21-Methode (RDS)
Synchronisieren Sie das angegebene Recordset mit der Datenbank, die durch die Verbindungszeichenfolge für die Verwendung mit ADO 2.1 angegeben.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.Synchronize21(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray)  
```  
  
#### <a name="parameters"></a>Parameter  
 *ConnectionString*  
 Eine Zeichenfolge verwendet, um mit dem OLE DB-Anbieter hergestellt, in dem die Anforderung gesendet werden. Wenn ein Ereignishandler verwendet wird, kann der Handler bearbeiten oder Ersetzen Sie die Verbindungszeichenfolge.  
  
 *HandlerString*  
 Die Zeichenfolge identifiziert den Handler, die mit dieser Ausführung verwendet werden. Die Zeichenfolge besteht aus zwei Teilen. Der erste Teil enthält den Namen (ProgID) des Handlers verwendet werden. Der zweite Teil der Zeichenfolge enthält Argumente, die an den Ereignishandler übergeben werden. Wie die Argumentzeichenfolge interpretiert wird, ist bestimmten Handler. Die beiden Teile werden durch die erste Instanz eines Kommas in der Zeichenfolge getrennt. Die Argumentzeichenfolge kann zusätzliche Kommas enthalten. Die Argumente sind optional.  
  
 *lSynchronizeOptions*  
 Eine Bitmaske der Synchronisierungsoptionen.  
  
 1 =*UpdateTransact* Aktualisierungen der Datenbank in einer Transaktion zusammengefasst werden. Die Transaktion wird abgebrochen, wenn eines der Updates ein Fehler auftritt.  
  
 2 =*RefreshWithUpdate* Ursachen Zeile Status zurückgegeben werden, wenn weder *aktualisieren* noch *RefreshConflicts* festgelegt ist.  
  
 4 =*aktualisieren* das Recordset mit aktuellen Daten aus der Datenbank aktualisiert wird. Ausstehende Updates werden nicht auf die Datenbank übertragen. Wenn dieses Bit nicht festgelegt ist, wird das Recordset nicht aktualisiert, und alle ausstehenden Updates auf die Datenbank verschoben werden.  
  
 8 =*RefreshConflicts* keine Zeilen mit ausstehenden Änderungen zu aktualisieren. Die Fehler beim Aktualisieren der Zeilen werden mit aktuellen Daten aus der Datenbank aktualisiert.  
  
 *ppRecordset*  
 Ein Zeiger auf einen Zeiger auf das Recordset synchronisiert werden.  
  
 *pStatusArray*  
 Synchronisieren Sie eine Variante ein sicheren Arrays der Status der Zeile für die betroffenen Zeilen zurückgegeben. Nicht festgelegt, wenn keines der folgenden Synchronisierungsoptionen festgelegt werden: *RefreshWithUpdate*, *aktualisieren* und *RefreshConflicts*.  
  
## <a name="remarks"></a>Hinweise  
 Die *HandlerString* Parameter kann null sein. Was in diesem Fall geschieht, hängt davon ab, wie die RDS-Server konfiguriert ist. Eine Zeichenfolge Handler "MSDFMAP.handler" gibt an, dass der Microsoft bereitgestellter Handler (Msdfmap.dll) verwendet werden soll. Eine Zeichenfolge Handler "MASDFMAP.handler,sample.ini" gibt an, dass der Msdfmap.dll-Handler verwendet werden soll, und dass das Argument "sample.ini" an den Ereignishandler übergeben werden sollen. Msdfmap.dll interpretiert klicken Sie dann das Argument als eine Richtung, in der sample.ini verwenden, um die Verbindung und den Abfragezeichenfolgen zu überprüfen.  
  
> [!NOTE]
>  Die **Synchronize21** Methode ist einfach nur eine Version von den [synchronisieren Methode (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md). Sie verwenden, müssen die **Synchronize** Methode für die Kommunikation mit ADO 2.1, die **Synchronize21** Methode kann stattdessen aufgerufen werden. Die Funktionen des die **Synchronize** Methode in ADO 2.5 und höher stellen eine Obermenge der Funktionen für die gleiche Methode in ADO 2.1.  
  
## <a name="applies-to"></a>Gilt für  
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


