---
title: DROP SIGNATURE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SIGNATURE
- DROP_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting signatures
- dropping signatures
- DROP SIGNATURE statement
- removing signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 8a1fd8c5-0e75-4b2f-9d3c-c296bed56cc7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b6a83bfc8691e883b69ff88e93514a0819d9eb67
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777033"
---
# <a name="drop-signature-transact-sql"></a>DROP SIGNATURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Löscht eine digitale Signatur aus einer gespeicherten Prozedur, Funktion, Assembly oder einem Trigger.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP [ COUNTER ] SIGNATURE FROM module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | ASYMMETRIC KEY Asym_key_name  
```  
  
## <a name="arguments"></a>Argumente  
 *module_name*  
 Der Name einer gespeicherten Prozedur, einer Funktion, einer Assembly oder eines Triggers.  
  
 CERTIFICATE *cert_name*  
 Der Name eines Zertifikats, mit dem die gespeicherte Prozedur, die Funktion, die Assembly oder der Trigger signiert wird.  
  
 ASYMMETRIC KEY *Asym_key_name*  
 Der Name eines asymmetrischen Schlüssels, mit dem die gespeicherte Prozedur, die Funktion, die Assembly oder der Trigger signiert wird.  
  
## <a name="remarks"></a>Remarks  
 Informationen zu Signaturen werden in der sys.crypt_properties-Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für das Objekt und die CONTROL-Berechtigung für das Zertifikat oder den asymmetrischen Schlüssel. Falls ein zugeordneter privater Schlüssel mit einem Kennwort geschützt ist, muss der Benutzer zudem das Kennwort kennen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Signatur des Zertifikats `HumanResourcesDP` aus der gespeicherten Prozedur `HumanResources.uspUpdateEmployeeLogin` entfernt.  
  
```  
USE AdventureWorks2012;  
DROP SIGNATURE FROM HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.crypt_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [DROP SIGNATURE &#40;Transact-SQL&#41;](../../t-sql/statements/add-signature-transact-sql.md)  
  
  
