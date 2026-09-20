<div align="center">

<img src="docs/assets/banner.png" alt="Run as a Service — ilustração de marca" width="100%">

# Run as a Service

### Processos com um ciclo de vida.

Referência documental sobre unidades `systemd` para processos executados em segundo plano. O repositório contém um guia, não uma aplicação, instalador ou coleção de serviços prontos.

[![Formato: Guia](https://img.shields.io/badge/Formato-Guia-34495e?style=flat-square)](#anatomia-de-uma-unidade) [![Ambiente: systemd](https://img.shields.io/badge/Ambiente-systemd-34495e?style=flat-square)](#antes-de-configurar)

[Antes de configurar](#antes-de-configurar) · [Anatomia de uma unidade](#anatomia-de-uma-unidade) · [Inspeção e diagnóstico](#inspeção-e-diagnóstico) · [Limites](#limites)

</div>

> O banner é uma ilustração conceitual de marca criada com IA; não é uma captura da aplicação nem comprovação de um resultado real.

| Entenda | Inspecione | Diagnostique |
| :--- | :--- | :--- |
| Separe Unit, Service e Install. | Consulte a configuração da unidade existente. | Relacione estado, logs e política de reinício. |

## Antes de configurar

Requer uma distribuição Linux que utilize systemd. Defina o executável, usuário de execução, diretório de trabalho, destino dos logs e política de reinício. Use caminhos absolutos e o menor conjunto de privilégios necessário ao seu serviço.

## Anatomia de uma unidade

| Seção | Responsabilidade |
| --- | --- |
| `[Unit]` | Descrição e ordenação em relação a outras unidades. |
| `[Service]` | Processo, diretório, identidade, logs e reinício. |
| `[Install]` | Associação utilizada quando a unidade é habilitada. |

`After=network.target` ordena a inicialização; não comprova conectividade com um destino remoto. `Restart=always` pode criar um ciclo de falhas se a configuração estiver incorreta. Avalie a política conforme o processo real.

## Inspeção e diagnóstico

Para uma unidade **já existente** chamada `meu-servico.service`:

```sh
systemctl status meu-servico.service
journalctl -u meu-servico.service -n 50
systemctl cat meu-servico.service
```

Substitua o nome pela unidade que administra. Esses comandos consultam estado, logs e configuração. Criar, habilitar, reiniciar ou alterar uma unidade é uma operação separada, que deve seguir o procedimento do serviço mantido.

## Limites

Não há código de aplicação ou testes neste repositório. O guia não instala dependências, não fornece autenticação e não torna um processo seguro por executá-lo como serviço. Exemplos ligados a ferramentas de segurança exigem laboratório autorizado e uma revisão própria de escopo e dados.
