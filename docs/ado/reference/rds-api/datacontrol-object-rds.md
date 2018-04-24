---
title: RDS (RDS) | Microsoft Docs
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
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88fa818b04e55e7d6ad8c8c1c8d984e5cd0680bf
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="datacontrol-object-rds"></a>RDS (RDS)
Bindet eine Datenabfrage [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) an eine oder mehrere Steuerelemente (z. B. ein Textfeld, ein Datenraster-Steuerelement oder ein Kombinationsfeld) zum Anzeigen der **Recordset** Daten auf einer Webseite.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>Hinweise  
 Die Klassen-ID für die **RDS. DataControl** Objekt ist BD96C556 65A3 - 11-d 0-983A-00C04FC29E33.  
  
> [!NOTE]
>  Wenn Sie eine Fehlermeldung, die erhalten eine [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) oder **RDS. DataControl** Objekt nicht geladen werden, stellen Sie sicher, dass Sie die ordnungsmäßige Klassen-ID verwenden Die Klasse wurden von Version 1.0 und 1.1-IDs für diese Objekte geändert. Darüber hinaus werden Beachten Sie, dass sogar enthaltene Spalten, die festgelegt werden müssen, bei der Verwendung der **RDS DataControl** Objekt.  
  
 Für ein grundlegendes Szenario müssen Sie nur die **SQL**, **verbinden**, und **Server** Eigenschaften von der **RDS. DataControl** -Objekt, das automatisch das Standardobjekt für Business angerufen, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md).  
  
 Alle Eigenschaften in der **RDS. DataControl** sind optional, da der benutzerdefinierten Geschäftsobjekte ihre Funktionalität ersetzen können.  
  
> [!NOTE]
>  Wenn Sie mehrere Ergebnisse Abfragen nur die ersten [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) zurückgegeben wird. Wenn mehrere Resultsets benötigt werden, weisen Sie jedes Element einen eigenen **DataControl**. Ein Beispiel für eine Abfrage für mehrere Ergebnisse kann Folgendes sein: `"Select * from Authors, Select * from Topics"`  
  
 Hinzufügen von "DFMode = 20;" zur Verbindungszeichenfolge bei der Verwendung der **RDS. DataControl** Objekt kann die Leistung Ihres Servers verbessern, bei der Aktualisierung von Daten. Mit dieser Einstellung wird die **RDSServer.DataFactory** Objekt auf dem Server verwendet einen Modus weniger ressourcenintensiv. Die folgenden Funktionen sind jedoch nicht in dieser Konfiguration verfügbar:  
  
-   Verwenden von parametrisierten Abfragen.  
  
-   Abrufen von Informationen von Parameter oder die Spalte vor dem Aufruf der **Execute** Methode.  
  
-   Festlegen von **Transact Updates** auf **"true"**.  
  
-   Abrufen des Zeilenstatus.  
  
-   Aufrufen der [Resync](../../../ado/reference/ado-api/resync-method.md) Methode.  
  
-   Aktualisieren (explizit oder automatisch) über die [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) Eigenschaft.  
  
-   Festlegen von **Befehl** oder [Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) Eigenschaften.  
  
-   Mit **AdCmdTableDirect**.  
  
 Die **RDS. DataControl** Objekt wird standardmäßig im asynchronen Modus ausgeführt. Wenn Sie die synchrone Ausführung für Ihre Anwendung benötigen, legen Sie die [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) Parameter gleich **AdcExecSync** und [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) gleichParameter**AdcFetchUpFront**, wie im folgenden Beispiel gezeigt.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="http://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 Verwenden Sie eine **RDS. DataControl** Objekt, das die Ergebnisse einer einzelnen Abfrage mit einer oder mehrerer visuelle Steuerelemente zu verknüpfen. Nehmen wir beispielsweise an Code Abfrage anfordernden Kundendaten wie Namen, Wohnort, Geburtsort, Alter und Prioritätsstatus der Kunden. Sie können ein einzelnes **RDS. DataControl** Objekt anzuzeigende Name, Alter und Region des Kunden in drei separate Textfelder; Status der Priorität Kunden in einem Kontrollkästchen; und alle Daten in einem Datenraster-Steuerelement.  
  
 Verwenden von unterschiedlichen **RDS. DataControl** -Objekten, die die Ergebnisse mehrerer Abfragen mit verschiedenen visuellen Steuerelementen zu verknüpfen. Angenommen Sie, Sie verwenden eine Abfrage zum Abrufen von Informationen zu einem Kunden und eine zweite Abfrage zum Abrufen von Informationen über waren, die der Kunde gekauft hat. Möchten die Ergebnisse der ersten Abfrage in drei Textfelder und ein Kontrollkästchen, und die Ergebnisse der zweiten Abfrage in einem Datenraster-Steuerelement anzuzeigen. Wenn Sie das Standard-Geschäftsobjekt verwenden (**RDSServer.DataFactory**), müssen Sie wie folgt vorgehen:  
  
-   Fügen Sie zwei **RDS. DataControl** Objekte zu einer Webseite.  
  
-   Schreiben Sie zwei Abfragen, eine für jede **SQL** Eigenschaft der beiden **RDS. DataControl** Objekte. Eine **RDS. DataControl** Objekt eine SQL-Abfrage, die Kundeninformationen enthält; das zweite enthält eine Abfrage, die eine Liste der Waren, die der Kunde gekauft hat anfordert.  
  
-   Geben Sie in den Tags Objekt jedes gebundenen Steuerelements den DATAFLD-Wert, um die Werte für die Daten festlegen, die in jedem visual Steuerelement angezeigt werden soll.  
  
 Es ist keine Einschränkung der Anzahl der auf der Anzahl der **RDS. DataControl** -Objekten, die Sie durch Objekttags auf einer einzelnen Webseite einbetten können.  
  
 Beim Definieren der **RDS. DataControl** Objekt auf einer Webseite, die ungleich null verwenden **Höhe** und **Breite** Werte wie z. B. 1 sein (um die Aufnahme zusätzlicher Speicherplatz zu vermeiden).  
  
 Remote Data Service-Clientkomponenten sind bereits als Bestandteil von Internet Explorer 4.0. aus diesem Grund, Sie müssen nicht enthalten einen CODEBASE-Parameter in Ihre **RDS. DataControl** object-Tag.  
  
 Mit Internet Explorer 4.0 oder höher, können Sie binden an Daten mithilfe von HTML-Steuerelementen und ActiveX® Steuerelemente nur, wenn sie als Apartment Modell Steuerelemente markiert sind.  
  
> [!NOTE]
>  **Microsoft Visual Basic-Benutzer** der **RDS. DataControl** ist sicher für Skripting und wird nur in webbasierten Anwendungen verwendet. Eine Visual Basic-Clientanwendung verfügt über keine Notwendigkeit für sie.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [DataControl-Objekt (RDS) – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DataControl-Objekt – Beispiel (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















