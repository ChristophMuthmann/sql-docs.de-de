---
title: DataSpace-Objekt (RDS) | Microsoft Docs
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
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c4ee2e71334998cd0d2cba1c0c52c67e3314619
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="dataspace-object-rds"></a>DataSpace-Objekt (RDS)
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Erstellt die clientseitige Proxys für benutzerdefinierte Geschäftsobjekte auf der mittleren Ebene an.  
  
 Remote Data Service benötigt Proxys für Geschäftsobjekte, damit die clientseitige Komponenten mit Geschäftsobjekte befindet sich auf der mittleren Ebene kommunizieren können. Proxys vereinfachen das Packen, entpacken und Transport (Marshallen) der Anwendung des [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Daten über Prozess- oder Computergrenzen hinweg.  
  
 Remote Data Service verwendet die **RDS. DataSpace** des Objekts [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) Methode zum Erstellen der Proxys für Business-Objekt. Das Business-Proxy-Objekt wird dynamisch erstellt werden, wenn eine Instanz der mittleren Ebene Objekt Entsprechung erstellt wird. Remote Data Service unterstützt die folgenden Protokolle: HTTP, HTTPS (HTTP Secure Sockets), DCOM und in-Process (Clientkomponenten und das Geschäftsobjekt auf demselben Computer befinden).  
  
> [!NOTE]
>  RDS verhält sich in einer "zustandslose" Weise bei der **RDS. DataSpace** Objekt verwendet das Protokoll HTTP oder HTTPS. Alle internen Informationen über eine Clientanforderung ist, also verworfen werden, nachdem der Server eine Antwort zurückgibt.  
  
> [!NOTE]
>  Obwohl das Geschäftsobjekt angezeigt wird, für die Lebensdauer des Proxys Business Objekt vorhanden ist, ist das Geschäftsobjekt tatsächlich vorhanden, nur verwendet werden, bis eine Antwort auf eine Anforderung gesendet wird. Wenn eine Anforderung ausgegeben wird (d. h. eine Methode für das Geschäftsobjekt aufgerufen wird), der Proxy öffnet eine neue Verbindung mit dem Server und der Server erstellt eine neue Instanz der das Geschäftsobjekt. Nachdem das Geschäftsobjekt auf die Anforderung reagiert, wird der Server das Geschäftsobjekt zerstört und schließt die Verbindung.  
  
> [!NOTE]
>  Dies bedeutet, dass Sie Daten aus einer Anforderung in eine andere mithilfe einer Business-Objekteigenschaft oder die Variable übergeben können. Sie müssen einen anderen Mechanismus, z. B. eine Datei oder Methodenargument, um Zustandsdaten beizubehalten nutzen.  
  
 Die Klassen-ID für die **RDS. DataSpace** Objekt ist BD96C556 65A3 - 11-d 0-983A-00C04FC29E36.  
  
 Die **DataSpace** Objekt für die Skripterstellung sicher ist.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [DataSpace-Objekt (RDS) – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DataSpace-Objekt und CreateObject-Methode – Beispiel (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


