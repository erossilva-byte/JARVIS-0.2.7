# J.A.R.V.I.S. Nova 1.2.5

Este repositório prepara e compila a fonte Android pelo GitHub Actions.

## Gerar o APK

1. Baixe no ChatGPT o arquivo **JARVIS-NOVA-1.2.5-fonte.zip**.
2. Na página inicial do repositório, escolha **Add file → Upload files** e envie esse ZIP para a raiz do repositório.
3. Faça o commit na branch `main`. O workflow **Build e testes do J.A.R.V.I.S. Nova** será iniciado.
4. Abra **Actions**, entre na execução e aguarde os testes e a compilação.
5. Se a execução terminar com sucesso, baixe o artefato **JARVIS-Nova-1.2.5-APK**. Ele contém `app-debug.apk` e o checksum SHA-256.

## Importante

- O APK só é publicado se os testes e a compilação terminarem com sucesso.
- Esta compilação é de depuração, não é assinada para publicação na Play Store.
- O build não comprova o funcionamento em um celular. Teste a ativação por voz, permissões, alarmes, notificações e segundo plano no dispositivo.
- Não envie AccessKeys ou chaves de provedores de IA ao repositório público.
- O detector Picovoice exige uma AccessKey configurada no aplicativo; não coloque a chave no código-fonte.
