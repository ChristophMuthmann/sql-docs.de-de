---
title: ConvertToString-Methode (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b6866ee98b3d75006678265347914a3f71aa908
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="converttostring-method-rds"></a>ConvertToString-Methode (RDS)
Konvertiert eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) in eine MIME-Zeichenfolge, die die Recordsetdaten darstellt.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataFactory*  
 Objektvariable stellt eine [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt.  
  
 *Recordset*  
 Objektvariable stellt eine **Recordset** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Mit ASP-Dateien verwenden **ConvertToString** Einbetten der **Recordset** in einer HTML-Seite, die auf dem Server auf einem Clientcomputer zu transportieren generiert.  
  
 **ConvertToString** ersten Laden der **Recordset** in den Cursordienst-Tabelle aus, und generiert dann einen Datenstrom im MIME-Format.  
  
 Auf dem Client Remote Data Service die MIME-Zeichenfolge wieder in einen voll funktionsfähigen konvertieren **Recordset**. Es eignet sich für die Behandlung von weniger als 400 Datenzeilen mit nicht mehr als 1024 Byte Breite pro Zeile. Sie sollte nicht für das streaming von BLOB-Daten verwenden und große Resultsets über HTTP. Keine Komprimierung über das Netzwerk auf die Zeichenfolge erfolgt sehr großer Datasets sehr viel Zeit in Transport über HTTP im Vergleich zu das Format Wire optimiert Tablegram definiert und vom Remote-Datendienst als systemeigene Transport Protocol Format bereitgestellt dauert.  
  
> [!NOTE]
>  Wenn Sie Active Server Pages verwenden, die sich ergebende MIME-Zeichenfolge in eine Client-HTML-Seite eingebettet werden sollen, Bedenken Sie, dass VBScript-Versionen vor Version 2.0 die Größe der Zeichenfolge auf 32 KB beschränkt. Wenn dieses Limit überschritten wird, wird ein Fehler zurückgegeben. Berücksichtigen Sie bei der MIME-Einbettung über ASP-Dateien im Abfragebereich auch relativ klein ist. Um dieses Problem zu beheben, wird herunterladen Sie die neueste Version von VBScript aus der Microsoft Windows Script Technologies-Website.  
  
## <a name="applies-to"></a>Gilt für  
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ConvertToString-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString-Methode – Beispiel (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


