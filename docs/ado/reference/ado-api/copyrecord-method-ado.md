---
title: CopyRecord-Methode (ADO) | Microsoft Docs
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
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5acc04720b17df0c39203417633332a0f01c2890
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="copyrecord-method-ado"></a>CopyRecord-Methode (ADO)
Kopiert eine Entität, dargestellt durch eine [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) an einen anderen Speicherort.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Quelle*  
 Optional. Ein **Zeichenfolge** Wert, der eine URL, die Entität kopiert werden soll (z. B. eine Datei oder Verzeichnis) enthält. Wenn *Quelle* ausgelassen wird, oder gibt eine leere Zeichenfolge, die Datei oder das Verzeichnis, die vom aktuellen [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) kopiert werden.  
  
 *Ziel*  
 Optional. Ein **Zeichenfolge** -Wert enthält eine URL angeben des Speicherorts, in dem *Quelle* kopiert werden.  
  
 *UserName*  
 Optional. Ein **Zeichenfolge** Wert, der die Benutzer-ID, die enthält bei Bedarf den Zugriff auf autorisiert *Ziel*.  
  
 *Kennwort*  
 Optional. Ein **Zeichenfolge** Wert, der das Kennwort, die enthält bei Bedarf überprüft *Benutzername*.  
  
 *Optionen*  
 Optional. Ein [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md) -Wert, der einen Standardwert hat **AdCopyUnspecified**. Gibt das Verhalten dieser Methode.  
  
 *Async*  
 Optional. Ein **booleschen** -Wert, wenn **"true"**, gibt an, dass dieser Vorgang asynchron sein sollte.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** -Wert, der in der Regel den Wert des zurückgibt *Ziel*. Der genaue Wert zurückgegeben, ist jedoch vom Anbieter abhängig.  
  
## <a name="remarks"></a>Hinweise  
 Die Werte der *Quelle* und *Ziel* müssen nicht übereinstimmen, andernfalls tritt ein Laufzeitfehler auf. Mindestens eine der Server, Pfad oder einer Ressource muss sich unterscheiden.  
  
 Alle untergeordneten Objekte (z. B. Unterverzeichnissen) *Quelle* rekursiv kopiert werden, es sei denn, **AdCopyNonRecursive** angegeben ist. In einem rekursiven Vorgang *Ziel* muss einem Unterverzeichnis des *Quelle*ist, andernfalls der Vorgang kann nicht abgeschlossen.  
  
 Diese Methode schlägt fehl, wenn *Ziel* identifiziert eine vorhandene Entität (z. B. eine Datei oder ein Verzeichnis), es sei denn, **AdCopyOverWrite** angegeben ist.  
  
> [!IMPORTANT]
>  Verwenden der **AdCopyOverWrite** Umsicht option. Beispielsweise wird diese Option angeben, wenn eine Datei in ein Verzeichnis kopiert *löschen* das Verzeichnis, und Ersetzen Sie es mit der Datei.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Das Datensatzobjekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
