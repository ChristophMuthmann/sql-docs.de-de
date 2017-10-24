---
title: "Mithilfe von ADO für Internet Publishing | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9b26261c83932005ba0852b67e4f246cea47b8e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-for-internet-publishing"></a>Mithilfe von ADO für Internet Publishing
[Der OLE DB-Anbieter für Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) zeigt ein Beispiel hierfür den Zugriff auf heterogene Daten mit ADO. Obwohl in den Beispielen in diesem Abschnitt spezifisch sind für die Verwendung die Publishing Internetanbieter ist, sollte die veranschaulichten Prinzipien ähnlich sein, bei Verwendung von ADO mit anderen Anbietern für heterogene Daten, z. B. einen Anbieter zu einem e-Mail-Store.  
  
## <a name="urls"></a>URLs  
 Uniform Resource Locators (URLs) können als Alternative zu Verbindungszeichenfolgen und Befehlstext verwendet werden, um Datenquellen und den Speicherort der Dateien und Verzeichnissen anzugeben. Sie können URLs verwenden, mit dem vorhandenen [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) und **Recordset** Objekte und mit der **Datensatz** und **Stream** Objekte.  
  
 Weitere Informationen zur Verwendung von URLs finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="record-fields"></a>Datensatzfelder  
 Die unterscheidende Unterschied zwischen heterogenen Daten und homogene Daten ist, dass für die erste, jede Datenzeile oder **Datensatz**, können Sie einen anderen Satz von Spalten oder **Felder**. Homogene Daten hat jede Zeile den gleichen Satz von Spalten. Weitere Informationen zu den Feldern, die spezifisch für die Publishing Internetanbieter finden Sie unter [Datensätze und vom Anbieter bereitgestellte zusätzliche Felder](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
### <a name="appending-new-fields"></a>Anfügen neuer Felder  
 Mehrere ADO-Objekte wurden verbessert, um arbeiten zusammen mit **Datensatz** und **Stream** Objekte.  
  
-   Die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung [Anfügen](../../../ado/reference/ado-api/append-method-ado.md) Methode, die erstellt und fügt eine [Feld](../../../ado/reference/ado-api/field-object.md) -Objekt in der Auflistung, können auch den Wert der angeben der **Feld**.  
  
-   Die [Update](../../../ado/reference/ado-api/update-method.md) Methode schließt ab, das Hinzufügen oder Löschen von Feldern in der Auflistung.  
  
-   Als Verknüpfung und Alternative zu den **Append** -Methode, können Sie durch Zuweisen eines Werts in ein Feld nicht definiert oder zuvor gelöschten Felder erstellen.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Der OLE DB-Anbieter für Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [Internet, die Publishing-Szenario](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [Absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [Datensätze und Felder Anbieter bereitgestellte](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Das Datensatzobjekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO-Verlauf](../../../ado/guide/ado-history.md)

