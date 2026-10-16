# J.A.R.V.I.S. Nova 1.2.6

Este repositório prepara e compila a fonte Android pelo GitHub Actions. A versão 1.2.6 está em desenvolvimento, baseada na fonte 1.2.5 e substituindo o detector Picovoice por um protótipo local openWakeWord.

## Gerar o APK

1. Baixe no ChatGPT o arquivo **JARVIS-NOVA-1.2.6-fonte.zip**.
2. Na página inicial do repositório, escolha **Add file → Upload files** e envie esse ZIP para a raiz do repositório.
3. Faça o commit na branch `main`. O workflow **Build e testes do J.A.R.V.I.S. Nova** será iniciado.
4. Abra **Actions**, entre na execução e aguarde os testes e a compilação.
5. Se a execução terminar com sucesso, baixe o artefato **JARVIS-Nova-1.2.6-APK**. Ele contém `app-debug.apk` e o checksum SHA-256.

## Estado e limitações

- A compilação só publica o APK se os testes e o Gradle terminarem com sucesso.
- Esta é uma compilação de depuração, não assinada para publicação na Play Store.
- O modelo openWakeWord integrado detecta **“Hey Jarvis” em inglês**, não apenas “Jarvis”. Falsos acionamentos, reconhecimento em português, uso com música, segundo plano e consumo de bateria precisam ser testados no aparelho.
- O código openWakeWord é Apache-2.0; os modelos pré-treinados são CC BY-NC-SA 4.0. Verifique as condições da licença antes de redistribuir, especialmente para uso comercial.
- Não coloque chaves de provedores de IA ou outras credenciais em repositório público.
- Compilar com sucesso não substitui os testes em um telefone real.
