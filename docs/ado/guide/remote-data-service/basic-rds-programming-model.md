---
title: Grundlegende RDS-Programmiermodell | Microsoft Docs
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
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed2123404be0728d69c6e31776e57c30750a41c0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="basic-rds-programming-model"></a>Grundlegende RDS-Programmiermodell
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS Adressen Anwendungen, die in der folgenden Umgebung vorhanden sind: eine Clientanwendung gibt ein Programm, das ausgeführt wird, auf einem Server und die Parameter erforderlich, um die gewünschten Informationen zurückzugeben. Das Programm wird auf dem Server verschafft sich Zugriff auf die angegebene Datenquelle aufgerufen, ruft die Informationen ab, optional die Daten verarbeitet und klicken Sie dann die resultierende Informationen an die Clientanwendung in ein Formular, das einfach zu verwendenden zurückgegeben. RDS bietet das bedeutet, dass Sie die folgende Sequenz von Aktionen ausführen:  
  
-   Geben Sie das Programm, auf dem Server aufgerufen werden soll, und rufen Sie eine Möglichkeit, die vom Client darauf verweisen. (Dieser Verweis wird manchmal bezeichnet eine *Proxy*. Die Remoteserver-Anwendung dar. Die Clientanwendung wird "den Proxy aufrufen" als ob ein lokales Programm jedoch nicht tatsächlich wird, die Remoteserver-Programm aufgerufen.)  
  
-   Rufen Sie die Server-Anwendung. Übergeben Sie Parameter an die Server-Anwendung, die die Datenquelle und den Befehl ausgeben zu identifizieren. (Die Server-Anwendung verwendet tatsächlich ADO, um Zugriff auf die Datenquelle. ADO stellt eine Verbindung mit einer der angegebenen Parameter, und stellt dann den Befehl in dem anderen Parameter angegeben ist.)  
  
-   Die Server-Anwendung erhält einen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt aus der Datenquelle. Optional, die **Recordset** Objekt auf dem Server verarbeitet wird.  
  
-   Des Programms gibt den endgültigen **Recordset** Objekt an die Clientanwendung.  
  
-   Auf dem Client die **Recordset** Objekt abgelegt eines Formulars, das einfach durch visuelle Steuerelemente verwendet werden kann.  
  
-   Änderungen an der **Recordset** Objekt gesendet werden, zurück an die Server-Anwendung, die sie zum Aktualisieren der Datenquelle verwendet.  
  
 Dieses Programmiermodell enthält bestimmte praktischer Features zur Verfügung. Wenn ein komplexe Serverprogramm den Zugriff auf die Datenquelle ist nicht erforderlich, und wenn Sie die erforderlichen Verbindungs- und Befehlsparameter bereitstellen, automatisch RDS werden werden rufen Sie die angegebenen Daten mit einem einfachen, Standardserverprogramm ab.  
  
 Wenn Sie eine komplexere Verarbeitung benötigen, können Sie eigene benutzerdefinierte Serverprogramm angeben. Z. B. da ein benutzerdefiniertes Serverprogramm die volle Leistung von ADO verfügbare hat, konnte es Herstellen einer Verbindung mit unterschiedlichen Datenquellen, kombinieren ihre Daten auf irgendeine Weise komplexe, und klicken Sie dann einen einfachen, verarbeiteten Ergebnis zurückgeben an die Clientanwendung.  
  
 Schließlich, wenn Ihre Anforderungen an einer Stelle in der Zwischenzeit sind, unterstützt ADO jetzt Anpassen des Verhaltens des das Standardprogramm für den Server.  
  
## <a name="see-also"></a>Siehe auch  
 [RDS-Programmiermodell im Detail](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS-Szenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS-Lernprogramm](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Verwendung und Sicherheit von RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


