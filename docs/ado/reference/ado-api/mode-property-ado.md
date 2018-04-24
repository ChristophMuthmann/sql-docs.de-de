---
title: Mode-Eigenschaft (ADO) | Microsoft Docs
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
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6ed032263810d32dd73d0e7356b8b3f30dbfecc
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="mode-property-ado"></a>Mode-Eigenschaft (ADO)
Gibt an, die verfügbaren Berechtigungen zum Ändern von Daten in einem [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md), [Datensatz](../../../ado/reference/ado-api/record-object-ado.md), oder [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) Wert. Der Standardwert für eine **Verbindung** ist **AdModeUnknown**. Der Standardwert für eine **Datensatz** Objekt **AdModeRead**. Der Standardwert für eine **Stream** einer zugrunde liegenden Datenquelle zugeordnet (mit einer URL als Quelle oder als Standard geöffnet **Stream** von einer **Datensatz**) ist  **AdModeRead**. Der Standardwert für eine **Stream** nicht zugeordnet, einer zugrunde liegenden Quelle (im Arbeitsspeicher instanziiert) ist **AdModeUnknown**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie die **Modus** Eigenschaft so festlegen oder die Zugriffsberechtigungen verwendet vom Anbieter für die aktuelle Verbindung zurückgeben. Sie können festlegen, die **Modus** Eigenschaft nur, wenn die **Verbindung** -Objekt ist geschlossen.  
  
 Für eine **Stream** -Objekt, falls der Zugriffsmodus nicht angegeben wird, aus der Quelldatenbank verwendet, um öffnen vererbt der **Stream** Objekt. Z. B. wenn ein **Stream** geöffnet wird eine **Datensatz** Objekt es im gleichen Modus als offen in der Standardeinstellung die **Datensatz**.  
  
 Diese Eigenschaft ist Lese-/Schreibzugriff auf, während das Objekt ist geschlossen und schreibgeschützt, während das Objekt geöffnet ist.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** bei Verwendung für eine clientseitige **Verbindung** -Objekt, das **Modus** Eigenschaft kann nur festgelegt werden, um **AdModeUnknown**.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Record-Objekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [IsolationLevel und Eigenschaften-Beispiel für Modus (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel und Modus Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
