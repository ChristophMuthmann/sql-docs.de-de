---
title: SetEncrypt-Methode (SQLServerDataSource) | Microsoft Docs
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
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 723c5c5402fb32f0ad74bf303dd7c682b88d1c84
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setencrypt-method-sqlserverdatasource"></a>setEncrypt-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt eine **booleschen** -Wert, der angibt, ob die Encrypt-Eigenschaft aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Verschlüsseln*  
  
 **"true"** , wenn die Secure Sockets Layer (SSL)-Verschlüsselung zwischen dem Client aktiviert ist und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Andernfalls lautet der Wert **false**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Encrypt-Eigenschaft, um festgelegt wird **"true"**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wird sichergestellt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] verwendet SSL-Verschlüsselung für alle Daten, die zwischen Client und Server gesendet werden, wenn der Server ein Zertifikat installiert ist. Der Standardwert ist **false**.  
  
 Bei der Initiierung eines SSL-Handshakes wird vom JDBC-Treiber die Java Virtual Machine (JVM) erkannt, auf der er ausgeführt wird.  
  
 Wenn die Encrypt-Eigenschaft, um festgelegt wird **"true"**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] verwendet JSSE-Standardsicherheitsanbieter der JVM zum Aushandeln der SSL-Verschlüsselung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Der Standardsicherheitsanbieter unterstützt möglicherweise nicht alle erforderlichen Funktionen zum erfolgreichen Aushandeln der SSL-Verschlüsselung. Beispielsweise unterstützt der Standardsicherheitsanbieter möglicherweise die Größe des öffentlichen RSA-Schlüssels verwendet wird, der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat. In diesem Fall löst der Standardsicherheitsanbieter möglicherweise einen Fehler aus, wodurch der JDBC-Treiber die Verbindung trennt. Führen Sie zum Beheben dieses Problems eine der folgenden Aktionen aus:  
  
-   Konfigurieren der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mit einem Serverzertifikat, das einen kleineren öffentlichen RSA-Schlüssel verfügt.  
  
-   Konfigurieren Sie die JVM Verwendung in einer anderen JSSE-Standardsicherheitsanbieter der "\<Java-Home > / lib/security/java.security" Sicherheitsdatei-Eigenschaften  
  
-   Verwenden Sie eine andere JVM.  
  
 Wenn die Encrypt-Eigenschaft nicht angegeben ist, oder legen Sie auf **"false"**, der Treiber erzwingt nicht die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Verschlüsselung unterstützt. Wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanz nicht zum Erzwingen der SSL-Verschlüsselung konfiguriert ist, eine Verbindung ohne Verschlüsselung hergestellt. Wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanz ist so konfiguriert, dass das Erzwingen der SSL-Verschlüsselung, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wird automatisch SSL-Verschlüsselung aktivieren, bei der Ausführung auf einer ordnungsgemäß konfigurierten JVM, da andernfalls die Verbindung wird beendet, und der Treiber löst einen Fehler.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
