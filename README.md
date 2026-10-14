# J.A.R.V.I.S. Nova 1.2.0

Este repositório contém a configuração para validar e compilar o APK Android pelo GitHub Actions.

## Enviar a fonte e gerar o APK

1. Baixe o arquivo `JARVIS-NOVA-1.2.0-fonte.zip` disponibilizado no chat.
2. Na página principal deste repositório, escolha **Add file → Upload files** e envie o ZIP para a raiz do repositório.
3. Confirme o commit na branch `main`. O envio do ZIP inicia o workflow **Build e testes do J.A.R.V.I.S. Nova**.
4. Abra **Actions**, entre na execução e aguarde os testes e a compilação terminarem com sucesso.
5. Baixe o artefato `JARVIS-Nova-1.2.0-APK`. O ZIP do artefato contém `app-debug.apk` e seu checksum SHA-256.

O APK só será disponibilizado se os testes e a compilação terminarem com sucesso. O arquivo APK de depuração não é assinado para distribuição na Play Store. Teste-o no aparelho antes de confiar em recursos de voz, alarmes, notificações e segundo plano.
