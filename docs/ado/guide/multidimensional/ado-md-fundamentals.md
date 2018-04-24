---
title: ADO MD-Grundlagen | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8160377b66ba6a781a92ef772795782eaa455478
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="ado-md-fundamentals"></a>ADO MD-Grundlagen
Microsoft® ActiveX® Data Objects (Multidimensional) (ADO MD) bietet einen einfachen Zugriff auf mehrdimensionale Daten aus Sprachen, z. B. Microsoft Visual Basic®, Microsoft Visual C++®. ADO MD erweitert Microsoft ActiveX® Data Objects (ADO), um Objekte, die spezifisch für mehrdimensionale Daten enthalten, z. B. die [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) und [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) Objekte. Mit ADO MD können Sie mehrdimensionales Schema durchsuchen, einen Cube Abfragen und Abrufen der Ergebnisse.  
  
 ADO MD verwendet wie ADO einen zugrunde liegenden OLE DB-Anbieter für den Zugriff auf Daten. Um mit ADO MD arbeiten, muss der Anbieter ein multidimensionaler Datenanbieter (MDP) sein, gemäß der Definition von der OLE DB-Spezifikation für OLAP. Ein MDP Testteamprojekt sind Daten in multidimensionalen Sichten nicht auf tabellarische Sichten, sondern ist wie ein tabellarischer Datenanbieter (TDP) Daten dargestellt. Finden Sie in der Dokumentation für den OLAP-OLE DB-Anbieter für Weitere Informationen zur spezifischen Syntax und Verhalten von Ihrem Anbieter unterstützt.  
  
 Dieses Dokument geht ausreichende Kenntnisse der Programmiersprache Visual Basic und eine allgemeine Kenntnisse im ADO und OLAP. Weitere Informationen finden Sie unter der [ADO-Programmiererhandbuch](../../../ado/guide/ado-programmer-s-guide.md) und [OLE DB für Online Analytical Processing (OLAP)](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Übersicht über multidimensionale Schemas und Daten](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [Arbeiten mit mehrdimensionalen Daten](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [Verwenden von ADO mit ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [Programmieren mit ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ADO MD-Objektmodell](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO Handbuch für Programmierer](../../../ado/guide/ado-programmer-s-guide.md)   
 [ADO-Erweiterungen für Datendefinitionssprache und Sicherheit (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [Übersicht über multidimensionale Schemas und Daten](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programmieren mit ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Verwenden von ADO mit ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Arbeiten mit mehrdimensionalen Daten](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
