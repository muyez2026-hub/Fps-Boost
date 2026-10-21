# FPS Boost (Fabric 1.21.1)

Mod cliente que aumenta o FPS **aliviando CPU e GPU**, feito para
Minecraft Java 1.21.1 + Fabric Loader 0.19.5, e **compatível com Sodium**
(não toca em renderização de chunks — o Sodium segue fazendo o trabalho
pesado de otimização; este mod complementa ele cortando o que o Sodium
não corta: entidades, block entities, itens dropados e partículas).

## O que o mod faz

1. **Culling de entidades à distância** — entidades além de X blocos não são
   renderizadas (jogadores nunca são removidos).
2. **Culling de block entities** — baús, placas, armazémos etc. longe da
   câmera não são renderizados.
3. **Culling de itens dropados** — itens no chão longe da câmera são pulados.
4. **Limitador de partículas** — só uma fração das partículas é exibida.
5. **Otimizações gráficas do vanilla** (uma vez, ao iniciar): partículas em
   MINIMAL, nuvens desligadas, sombras de entidades desligadas e
   "Entity Distance" reduzido.

Tudo é configurável em `config/fpsboost.json`:

| Campo | Padrão | Descrição |
|---|---|---|
| `enabled` | `true` | Liga/desliga as otimizações por mixin |
| `entityRenderDistance` | `48.0` | Distância máxima de renderização de entidades (blocos) |
| `blockEntityRenderDistance` | `32.0` | Distância máxima de block entities (blocos) |
| `itemEntityRenderDistance` | `24.0` | Distância máxima de itens dropados (blocos) |
| `particleMultiplier` | `0.4` | Fração de partículas (0.0 = nenhuma, 1.0 = vanilla) |
| `applyVideoOptimizations` | `true` | Aplica as opções gráficas do vanilla ao iniciar |

## Como compilar

Pré-requisito: **JDK 21** instalado.

```bash
./gradlew genSources   # opcional, para ter os sources do Minecraft
./gradlew build
```

O arquivo do mod sai em `build/libs/fps-boost-1.0.0.jar`.
Jogue esse `.jar` na pasta `mods/` junto com o Fabric API e (recomendado) o Sodium.

## Avisos importantes

- As assinaturas dos métodos nos mixins seguem o **Yarn 1.21.1+build.3**. Se
  algum mixin falhar ao aplicar no seu ambiente (mensagem de erro no log
  mencionando `fpsboost.mixins.json`), ajuste a assinatura conforme o build do
  Yarn que estiver usando — os comentários nos mixins indicam o que procurar.
- `loader_version=0.19.5` pode ser ajustado em `gradle.properties` se o seu
  ambiente usar outra versão do Fabric Loader.
- Se o FPS ainda estiver baixo, o maior ganho vem do **Sodium** em si; este mod
  é um complemento e não substitui o Sodium.

## Licença

MIT — modifique e redistribua à vontade.
