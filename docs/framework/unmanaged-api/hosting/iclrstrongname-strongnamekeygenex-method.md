---
title: Метод ICLRStrongName::StrongNameKeyGenEx
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameKeyGenEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameKeyGenEx
helpviewer_keywords:
- ICLRStrongName::StrongNameKeyGenEx method [.NET Framework hosting]
- StrongNameKeyGenEx method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 1f8b59d0-5b72-45b8-ab74-c2b43ffc806e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b213285b3c533488cfa48198951275925c0e37ae
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33436190"
---
# <a name="iclrstrongnamestrongnamekeygenex-method"></a>Метод ICLRStrongName::StrongNameKeyGenEx
Создает новую пару открытого и закрытого ключей с указанным размером ключа, для использования строгого имени.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT StrongNameKeyGenEx (  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  DWORD     dwFlags,  
    [in]  DWORD     dwKeySize,  
    [out] BYTE      **ppbKeyBlob,  
    [out] ULONG     *pcbKeyBlob  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `wszKeyContainer`  
 [in] Имя запрашиваемый контейнер ключа. `wszKeyContainer` должен быть непустой строкой или null для создания временного имени.  
  
 `dwFlags`  
 [in] Значение, указывающее, следует ли оставить ключ зарегистрирован. Поддерживаются следующие значения:  
  
-   0x00000000 — используется, когда `wszKeyContainer` имеет значение null для создания временного имени контейнера ключа.  
  
-   0x00000001 (`SN_LEAVE_KEY`) — указывает, что ключ должен оставаться зарегистрированным.  
  
 `dwKeySize`  
 [in] Запрошенный размер ключа в битах.  
  
 `ppbKeyBlob`  
 [out] Возвращаемый открытого и закрытого ключей.  
  
 `pcbKeyBlob`  
 [out] Размер в байтах для `ppbKeyBlob`.  
  
## <a name="return-value"></a>Возвращаемое значение  
 `S_OK` Если метод успешно завершена; в противном случае — значение HRESULT, указывающее на сбой (в разделе [часто встречающихся значений HRESULT](http://go.microsoft.com/fwlink/?LinkId=213878) список).  
  
## <a name="remarks"></a>Примечания  
 Требуется платформа .NET Framework версии 1.0 и 1.1 `dwKeySize` 1024 бит для подписи сборки строгим именем; версии 2.0 добавлена поддержка 2048-разрядные ключи.  
  
 После извлечения ключа необходимо вызвать [ICLRStrongName::StrongNameFreeBuffer](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md) метод для освобождения выделенной памяти.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** MetaHost.h  
  
 **Библиотека:** включена как ресурс в MSCorEE.dll  
  
 **Версии платформы .NET framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Метод StrongNameKeyGen](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeygen-method.md)  
 [Интерфейс ICLRStrongName](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
