---
title: SupportsResultSetType-Methode (SQLServerDatabaseMetaData) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsResultSetType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aded734f-c96e-460f-afaa-8f64a92560d7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd5ede69a46e80e71b3beb8ee5a382f49ee200fe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617568"
---
# <a name="supportsresultsettype-method-sqlserverdatabasemetadata"></a>supportsResultSetType-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab, ob von dieser Datenbank der angegebene Resultsettyp unterstützt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean supportsResultSetType(int type)  
```  
  
#### <a name="parameters"></a>Parameter  
 *type*  
  
 Ein **ganzzahliger** Wert zum Angeben des Resultsettyps, bei dem es sich gemäß Definition in „java.sql.ResultSet“ oder „SQLServerResultSet“ um einen der folgenden Werte handeln kann:  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet-Typen  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet-Typen  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** unterstützt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Diese SupportsResultSetType-Methode wird von der SupportsResultSetType-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
