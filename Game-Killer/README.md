# Memória Root para Android

App Android para listar processos, buscar valores na memória, refinar resultados e gravar um valor em endereços encontrados. Acesso root é solicitado pelo `su` no próprio telefone.

## Tipos suportados

- Busca conjunta por valores Int8/UInt8, Int16/UInt16, Int32/UInt32, Int64/UInt64, Float32/Float64, texto UTF-8/UTF-16LE e bytes hex
- Texto UTF-8 e UTF-16LE
- Sequências de bytes em hexadecimal; `??` representa um byte variável (por exemplo, `A1 ?? 3F`)

Inteiros e bytes usam little-endian. Depois da primeira busca exata, informe o novo valor e toque em **Refinar** para reduzir os resultados. Toque em um endereço para editá-lo ou grave o novo valor nos resultados encontrados.
## Instalação

APK de depuração: `app/build/outputs/apk/debug/app-debug.apk`. Instale no telefone e autorize o pedido de root no gerenciador instalado no aparelho. O APK é assinado com uma chave de depuração local.

Para usar a janela sobre outros apps, abra **Abrir janela flutuante** e permita **Exibir sobre outros apps** nas Configurações do Android. Volte ao Memória Root e toque no botão novamente. Ela começa como um botão circular `MR`, que pode ser arrastado. Toque para expandir; a opção **Congelar app durante a busca** fica desligada por padrão. Ative-a somente se quiser suspender o alvo; desativá-la o retoma. Recolher a ferramenta também retoma o alvo. Use `×` para encerrar.

**Todos os formatos (número/texto)** tenta as representações numéricas e textuais do valor informado; bytes hex podem ser selecionados diretamente. Para refinar: faça a busca inicial, volte ao app alvo e altere o valor, abra a bolha, informe o novo valor e toque em **Refinar**. Repita para reduzir os endereços. Cada resultado mantém sua representação para que gravar o novo valor use o formato correto. Texto UTF-8, UTF-16LE e padrões hex continuam disponíveis como buscas específicas.

## Compilar

Abra esta pasta no Android Studio e execute `assembleDebug`, ou use Gradle 8.9 com Android Gradle Plugin 8.7.3. O projeto usa compile SDK 36.

## Limites

O acesso e a leitura de `/proc/<PID>/mem` variam conforme a versão do Android, SELinux e o gerenciador root. Algumas proteções do sistema ou do próprio app podem impedir leitura ou gravação. A busca percorre as regiões legíveis em blocos de 64 MiB e exibe até 500 endereços por formato. Se não houver resultados, o status informa quantos bytes foram lidos para diferenciar falta de correspondência de falta de acesso. Use apenas em processos e dispositivos para os quais você tem autorização.
