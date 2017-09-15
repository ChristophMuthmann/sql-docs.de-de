---
title: InvokeService (RDS) | Microsoft Docs
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
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 20e7b09600a0ec96b089322a1bd4d55e75eb9acf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
Gibt einen Zeiger auf die angeforderte Schnittstelle auf einer leistungsfähigere Version des Objekts zurück.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>Parameter  
 *riid*  
  
 [in] Der Bezeichner der angeforderten Schnittstelle.  
  
 *punkNotSoFunctionalInterface*  
  
 [in] Das weniger leistungsfähige Quellobjekt.  
  
 *ppunkMoreFunctionalInterface*  
  
 [out] Die Adresse der Zeigervariablen, die den Schnittstellenzeiger in angeforderte empfängt *Riid*. Nach erfolgreicher Rückkehr die *PpunkMoreFunctionalInterface* Parameter enthält die angeforderte Schnittstellenzeiger auf das Objekt. Wenn das Objekt im angegebenen Schnittstelle nicht unterstützt *Riid*, *PpunkMoreFunctionalInterface* auf NULL festgelegt ist.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein HRESULT-Wert, der gibt an, wenn der Aufruf der **InvokeService** Methode war erfolgreich.  
  
## <a name="remarks"></a>Hinweise  
 Die RDS-Cursor Engine Implementierung von **InvokeService** nimmt das Eingaberowset (oder mehrere Ergebnisse-Objekt), füllt das Cursormodul aus dem Eingaberowset und gibt dann einen Zeiger auf sich selbst zurück.  
  
## <a name="applies-to"></a>Gilt für  
 [IRDSService-Schnittstelle (RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [RDS-Methoden](../../../ado/reference/rds-api/rds-methods.md)



