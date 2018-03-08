---
title: DataControl-Fehlercodes | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1933a555212045c157656a0ee46aba77dc9f699d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="datacontrol-object-error-codes"></a>RDS-Fehlercodes
Die folgende Tabelle enthält die [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Fehlercodes-Objekt. Die positive decimal Übersetzung der niedrigen zwei Bytes, die negative dezimale Übersetzung von der vollständigen Fehlercode und die hexadezimale Werte werden angezeigt.

|RDS. DataControl-Fehlercodes|Number|Description|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107 -2146824175 0x800A1011|Vorgang kann nicht ausgeführt werden, während ein asynchroner Vorgang aussteht.|
|**IDS_BadInlineTablegram**|4105 -2146824183 0x800A1009|Ungültiges Inline Tablegram.|
|**IDS_CantConnect**|4099 -2146824189 0x800A1003|Kann keine Verbindung zum Server hergestellt werden.|
|**IDS_CantCreateObject**|4100 -2146824188 0x800A1004|Business-Objekt kann nicht erstellt werden.|
|**IDS_CantFindDataspace**|4102 -2146824186 0x800A1006|Datenspeicher-Eigenschaft ist nicht gültig.|
|**IDS_CantInvokeMethod**|4101 -2146824187 0x800A1005|Methode kann nicht für Geschäftsobjekt aufgerufen werden.|
|**IDS_CrossDomainWarning**|4112 -2146824170 0x800A1016|Diese Seite greift auf Daten in einer anderen Domäne. Möchten Sie dies zulassen? Um diese Meldung in Internet Explorer zu vermeiden, können Sie eine sichere Website zu Zone vertrauenswürdiger Sites hinzufügen, auf die **Sicherheit** auf der Registerkarte die **Internetoptionen** (Dialogfeld).|
|**IDS_InvalidADCClientVersion**|4106 -2146824176 0x800A1010|Ungültige Version in einer RDS-Client – Client ist neuer als die Server.|
|**IDS_INVALIDARG**|5376 -2147019520 0x80071500|Ein oder mehrere Argumente sind ungültig.|
|**IDS_InvalidBindings**|4097 -2146824191 0x800A1001|Fehler in Bindungseigenschaft.|
|**IDS_InvalidParam**|4110 -2146824172 0x800A1014|Ein oder mehrere Argumente sind ungültig.|
|**IDS_NOINTERFACE**|5377 -2147019519 0x80071501|Schnittstelle nicht unterstützt wird.|
|**IDS_NotReentrant**|4111 -2146824171 0x800A1015|Anforderung kann nicht ausgeführt werden, während der Ereignishandler noch verarbeitet wird.|
|**IDS_ObjectNotSafe**|4103 -2146824185 0x800A1007|Die Sicherheitseinstellungen auf diesem Computer lassen Erstellung Geschäftsobjekts sein.|
|**IDS_RecordsetNotOpen**|4109 -2146824173 0x800A1013|**Recordset** ist nicht geöffnet.|
|**IDS_ResetInvalidField**|4108 -2146824174 0x800A1012|Spalte, die im angegebenen **SortColumn** oder **FilterColumn** ist nicht vorhanden.|
|**IDS_RowsetNotUpdateable**|4104 -2146824184 0x800A1008|Das Rowset ist nicht aktualisierbar.|
|**IDS_UnexpectedError**|4351 -2146823937 0x800A10FF|Unerwarteter Fehler.|
|**IDS_UpdatesFailed**|4098 -2146824190 0x800A1002|Datenbank kann nicht aktualisiert.|
|**IDS_URLMONNotFound**|4119 -2146824169 0x800A1017|DataControl **URL** Eigenschaft erfordert die Systemdatei Urlmon.dll, die nicht gefunden werden kann.|

## <a name="see-also"></a>Siehe auch
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)
