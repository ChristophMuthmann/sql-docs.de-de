---
title: GetEncrypt-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9262c2fb18160f5072d21a71c082bd00d17fc302
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getencrypt-method-sqlserverdatasource"></a>getEncrypt-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt eine **booleschen** -Wert, der angibt, ob die Encrypt-Eigenschaft aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** Wenn verschlüsseln aktiviert ist. Andernfalls lautet der Wert **false**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Encrypt-Eigenschaft, um festgelegt wird **"true"**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wird sichergestellt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] verwendet SSL-Verschlüsselung für alle Daten, die zwischen dem Client und dem Server gesendet werden, wenn der Server ein Zertifikat installiert ist.  
  
 Wenn die Encrypt-Eigenschaft nicht angegeben ist, oder legen Sie auf **"false"**, der Treiber erzwingt nicht die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Verschlüsselung unterstützt. Wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanz nicht zum Erzwingen der SSL-Verschlüsselung konfiguriert ist, eine Verbindung ohne Verschlüsselung hergestellt. Wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanz ist so konfiguriert, dass das Erzwingen der SSL-Verschlüsselung, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wird automatisch SSL-Verschlüsselung aktivieren, bei der Ausführung auf einer ordnungsgemäß konfigurierten Java Virtual Machine (JVM), da andernfalls die Verbindung wird beendet, und der Treiber löst einen Fehler. Wenn die Verschlüsselungseigenschaft nicht festgelegt ist, die [GetEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) Methodenrückgabe den Standardwert von **"false"**.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
