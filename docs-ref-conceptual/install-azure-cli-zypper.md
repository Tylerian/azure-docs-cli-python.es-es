---
title: Instalación de la CLI de Azure en Linux con zypper
description: Cómo instalar la CLI de Azure con zypper
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/09/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-cli
ms.devlang: azure-cli
ms.openlocfilehash: 201cce81046d5039a313b918ac48b2849352995c
ms.sourcegitcommit: c4462456dfb17993f098d47c37bc19f4d78b8179
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2018
ms.locfileid: "47177681"
---
# <a name="install-azure-cli-with-zypper"></a>Instalación de la CLI de Azure con zypper

Para las distribuciones de Linux con `zypper`, como openSUSE o SLES, hay un paquete disponible para la CLI de Azure. Este paquete se ha probado con openSUSE 42.2 y SLES 12 SP 2.

[!INCLUDE [linux-install-requirements.md](includes/linux-install-requirements.md)]

## <a name="install"></a>Instalación

1. Instale `curl`:

   ```bash
   sudo zypper install -y curl
   ```

2. Importe la clave del repositorio de Microsoft:

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. Cree la información del repositorio `azure-cli` local:

   ```bash
   sudo zypper addrepo --name 'Azure CLI' --check https://packages.microsoft.com/yumrepos/azure-cli azure-cli
   ```

4. Actualice el índice del paquete `zypper` e instálelo:

   ```bash
   sudo zypper install --from azure-cli -y azure-cli
   ```

Después, ejecute la CLI de Azure con el comando `az`. Para iniciar sesión, use el comando [az login](/cli/azure/reference-index#az-login).

[!INCLUDE [interactive-login](includes/interactive-login.md)]

Para más información acerca de los diferentes métodos de autenticación, consulte [Inicio de sesión con la CLI de Azure](authenticate-azure-cli.md).

## <a name="update"></a>Actualizar

Puede actualizar el paquete con el comando `zypper update`.

```bash
sudo zypper refresh
sudo zypper update azure-cli
```

## <a name="uninstall"></a>Desinstalación

[!INCLUDE [uninstall-boilerplate.md](includes/uninstall-boilerplate.md)]

1. Elimine el paquete de su equipo.

    ```bash
    sudo zypper remove -y azure-cli
    ```

2. Si no tiene previsto volver a instalar la CLI, elimine la información del repositorio.

  ```bash
  sudo zypper removerepo azure-cli
  ```

3. Si ha eliminado la información del repositorio, elimine también la clave de la firma GPG de Microsoft.

  ```bash
  MSFT_KEY=`rpm -qa gpg-pubkey /* --qf "%{version}-%{release} %{summary}\n" | grep Microsoft | awk '{print $1}'`
  sudo rpm -e --allmatches gpg-pubkey-$MSFT_KEY
  ```
## <a name="next-steps"></a>Pasos siguientes

Ahora que ha instalado la CLI de Azure, dé un breve paseo por sus características y comandos más comunes.

> [!div class="nextstepaction"]
> [Introducción a la CLI de Azure](get-started-with-azure-cli.md)
