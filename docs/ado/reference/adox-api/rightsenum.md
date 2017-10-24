---
title: RightsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac335398b4895e01ece3324488d30bfd670fd140
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="rightsenum"></a>RightsEnum
Gibt die Rechte oder Berechtigungen für eine Gruppe oder Benutzer auf ein Objekt an.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (& H4000)|Der Benutzer oder die Gruppe verfügt über die Berechtigung zum Erstellen neuer Objekte dieses Typs.|  
|**adRightDelete**|65536 (& H10000)|Der Benutzer oder die Gruppe verfügt über die Berechtigung zum Löschen von Daten aus einem Objekt. Für Objekte wie z. B. **Tabellen**, der Benutzer verfügt über die Berechtigung zum Löschen der Datenwerte aus Datensätzen.|  
|**adRightDrop**|256 (& H100)|Benutzer oder Gruppe verfügt über die Berechtigung zum Entfernen von Objekten aus dem Katalog. Beispielsweise **Tabellen** können durch eine DROP TABLE SQL-Befehl gelöscht werden.|  
|**adRightExclusive**|512 (& H200)|Der Benutzer oder die Gruppe verfügt über eine Zugriffsberechtigung für das Objekt ausschließlich aus.|  
|**adRightExecute**|536870912 (& H20000000)|Der Benutzer oder die Gruppe verfügt über die Berechtigung zum Ausführen des Objekts.|  
|**adRightFull**|268435456 (& H10000000)|Der Benutzer oder die Gruppe verfügt über alle Berechtigungen für das Objekt ein.|  
|**adRightInsert**|32768 (& H8000)|Der Benutzer oder die Gruppe berechtigt ist, das Objekt eingefügt. Für Objekte wie z. B. **Tabellen**, der Benutzer verfügt über die Berechtigung zum Einfügen von Daten in der Tabelle.|  
|**adRightMaximumAllowed**|33554432 (& H2000000)|Der Benutzer oder die Gruppe hat die maximale Anzahl von Berechtigungen, die vom Anbieter zulässig. Es sind spezielle Berechtigungen vom Anbieter abhängig.|  
|**adRightNone**|0|Der Benutzer oder die Gruppe verfügt über keine Berechtigungen für das Objekt aus.|  
|**adRightRead**|-2147483648 (& H80000000)|Der Benutzer oder die Gruppe verfügt über die Berechtigung zum Lesen des Objekts. Für Objekte wie z. B. [Tabellen](../../../ado/reference/adox-api/table-object-adox.md), der Benutzer verfügt über die Berechtigung zum Lesen der Daten in der Tabelle.|  
|**adRightReadDesign**|1024 (& H400)|Der Benutzer oder die Gruppe verfügt über die Berechtigung zum Lesen des Entwurfs für das Objekt.|  
|**adRightReadPermissions**|131072 (& H20000)|Der Benutzer- oder Gruppenberechtigungen kann angezeigt, jedoch nicht ändern, die bestimmten Berechtigungen für ein Objekt im Katalog.|  
|**adRightReference**|8192 (& H2000)|Der Benutzer oder die Gruppe berechtigt ist, das Objekt zu verweisen.|  
|**adRightUpdate**|1073741824 (& H40000000)|Der Benutzer oder die Gruppe verfügt über die Berechtigung zum Aktualisieren des Objekts. Für Objekte wie z. B. **Tabellen**, der Benutzer verfügt über die Berechtigung zum Aktualisieren der Daten in der Tabelle.|  
|**adRightWithGrant**|4096 (& H1000)|Der Benutzer oder die Gruppe verfügt über die Berechtigung erteilen von Berechtigungen für das Objekt.|  
|**adRightWriteDesign**|2048 (& H800)|Der Benutzer oder die Gruppe verfügt über die Berechtigung zum Ändern des Entwurfs für das Objekt.|  
|**adRightWriteOwner**|524288 (& H80000)|Benutzer oder Gruppe verfügt über die Berechtigung zum Ändern des Besitzers des Objekts.|  
|**adRightWritePermissions**|262144 ERFOLGT (& H40000)|Der Benutzer oder die Gruppe kann die spezifischen Berechtigungen für ein Objekt im Katalog ändern.|  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[GetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[SetPermissions-Methode (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|

