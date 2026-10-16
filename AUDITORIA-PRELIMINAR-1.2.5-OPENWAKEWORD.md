# Auditoria preliminar — J.A.R.V.I.S. Nova 1.2.5

**Data:** 2026-10-16  
**Escopo real desta etapa:** inspeção do workflow atual do repositório e da fonte 1.1.0 disponível no ambiente. Isto ainda não é uma auditoria integral da fonte 1.2.5, pois o arquivo `JARVIS-NOVA-1.2.5-fonte.zip` não está presente no repositório nem no ambiente desta execução.

## Resultado inicial

- A fonte 1.1.0 disponível passou em `npm run test:all`: verificações de sintaxe JavaScript, validação estrutural do projeto e compilação sintática dos scripts Python.
- A compilação Gradle/APK e os testes em aparelho continuam **não verificados**.
- O workflow do repositório espera `JARVIS-NOVA-1.2.5-fonte.zip` na raiz. A busca no repositório não encontrou esse arquivo.
- O workflow atual chama `patch_gradle.py` para aplicar a dependência Porcupine. Esse script não existe na fonte 1.1.0 disponível. Isso precisa ser reconciliado antes de considerar o pipeline pronto.
- O pipeline ainda está orientado ao Porcupine, enquanto a decisão de produto é testar primeiro uma alternativa local gratuita baseada em openWakeWord.

## Achado prioritário: ativação por voz atual

Na fonte 1.1.0, `JarvisBackgroundPlugin.java` implementa a detecção contínua por meio do `SpeechRecognizer` do Android, reiniciando sessões de reconhecimento. O modo explicitamente local depende de `somenteLocal=true`, Android 12/API 31 ou superior e disponibilidade do reconhecedor on-device. No modo normal, o código cria o reconhecedor genérico do Android. Portanto, a implementação atual não comprova uma detecção dedicada de palavra-chave inteiramente local e pode depender do serviço de reconhecimento do aparelho.

## Candidato a protótipo local

Foi identificado o projeto [msnilsen/openwakeword-android](https://github.com/msnilsen/openwakeword-android), um port Kotlin/Android que executa a inferência no aparelho, sem API ou serviço em nuvem, e oferece o modelo integrado `HEY_JARVIS`. A documentação indica Android API 26+ e permissão `RECORD_AUDIO`.

**Licença a respeitar:** o código da biblioteca está sob Apache-2.0; os modelos pré-treinados openWakeWord estão sob CC BY-NC-SA 4.0. Isso limita o uso comercial do modelo e exige cumprir atribuição e compartilhamento pela mesma licença. Antes de qualquer distribuição comercial, será necessário trocar o modelo ou obter autorização/licença adequada.

**Limitação de frase:** o modelo disponível é “Hey Jarvis” (voz de treinamento em inglês dos EUA), não apenas “Jarvis”. A detecção em português, com música e ruído, precisa de testes. Se a frase exata “Jarvis” for requisito, será necessário avaliar um modelo personalizado ou comparar com Porcupine.

## Próximas etapas

1. Recuperar ou gerar a fonte completa 1.2.5 e confirmar que todos os arquivos referenciados pelo workflow estão presentes.
2. Reexecutar os testes estáticos sobre a fonte exata 1.2.5.
3. Prototipar a integração openWakeWord no serviço Android, com controles explícitos para iniciar/parar, indicação visível de escuta e encerramento correto do microfone.
4. Verificar dependências, licenças, permissões e compatibilidade do serviço em segundo plano.
5. Executar o build Android no GitHub Actions; não declarar o APK pronto antes de um build bem-sucedido.
6. Testar em aparelho físico: falsos acionamentos, taxa de detecção, música em reprodução, tela bloqueada, consumo de bateria, reinício e pausa da escuta.

## Referências técnicas consultadas

- [openwakeword-android — integração Android e requisitos](https://github.com/msnilsen/openwakeword-android)
- [Modelo “Hey Jarvis” — idioma, métricas e licença](https://openwakeword.com/library/1502)
- [openWakeWord — licença do código e dos modelos](https://github.com/dscripka/openWakeWord)
- [Porcupine Android — AccessKey e permissões](https://github.com/Picovoice/porcupine/blob/master/binding/android/README.md)
